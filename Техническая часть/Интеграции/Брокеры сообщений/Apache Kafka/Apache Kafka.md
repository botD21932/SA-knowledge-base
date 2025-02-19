**Apache Kafka** - распределённый опен-сорс брокер сообщений ([[Брокеры сообщений]]) в стриминговом режиме. Используется на платформах с высокими требованиями производительности, для интеграции данных различных платформ.

**Основные свойства Kafka:**
1) Распределённость
2) Отказоустойчивость
3) Высокая доступность
4) Надёжность и согласованность данных
5) Высокая производительность (пропускная способность)
6) Горизонтальное масштабирование
7) Интегрируемость

**Какую задачу решаем?** Хотим поставить данные от производителей к потребителям (причём нужно обеспечить широковещательный режим).

**Сложности:**
1) Надёжность и гарантия доставки
2) Подключение новых получателей
3) Отправители знают получателей
4) Техническая поддержка
5) Интеграции разных стеков

 **Основные сущности Kafka:**
 1) Broker
 2) Zookeper
 3) Message
 4) Topic/Partition
 5) Producer
 6) Consumer

**Функции брокера:**
1) Приём сообщений
2) Хранение сообщений
3) Выдача сообщений

Брокеры объединяются в кластеры для обеспечения масштабирования и репликации данных. За ними наблюдает Zookeper. В нём хранятся состояние кластера, конфигурация и адресная книга кластера. Также в кластере выбирается один брокер, назначаемый контроллером, который обеспечивает консистентность данных.

**Сообщения в Kafka имеют следующую структуру:**
1) **Key.** Ключ (опциональный) используется для распределения сообщений по кластеру
2) **Value.** Содержимое сообщения - массив байт
3) **Timestamp.** Время сообщения (от эпохи). Устанавливается при отправке или обработке внутри кластера
4) **Headers.** Набор key-value пар с пользовательскими атрибутами сообщения

**Топик** - очередь данных. Могут получаться из различных источников. При больших нагрузках делим топик на **партиции**. При этом порядок сохраняется на уровне партиций. Размещение топиков по кластеру регулируется самой Kafka (учитывается количество всех партиций всех топиков на брокер).

Хранение топиков ведётся в каждом брокере в папке ./logs.  В нём лежат папки по партициям, а там лежат три файла:
1) **.log.** Тут хранятся:
	1) **Offset.** Номер сообщения в партиции
	2) **Position.** Позиция смещения в байтах
	3) **Timestamp.** 
	4) **Message.**
2) **.index.** Тут происходит маппинг оффсета на позицию
3) **.timeindex.** Тут происходит маппинг timestamp на оффсет
Если топик работает долго, то появляются дополнительные группы из этих таких файлов (при превыщении объёма сегмента в 1гб, обычно). Имя нового сегмента строится исходя из первого оффсета этого сегмента. У сегментов есть свой timestamp, определяемый как максимум timestamp из сегмента.

**Важно: операции удаления данных нет!** Есть удаление по истечению TTL (time to live) по сегментам.

В Kafka реализована репликация партиций (регулируется настройка replication-factor). Работает по master-slave схеме, где на выбранном мастере лежат операции записи и чтения, а реплики просто копируют его (главные - в точности, остальные - с отставанием). Leader-реплики назначает controller. Схема master-slave устроена по принципу опрашивания leader-а со стороны follower-ов. Есть особые in-sync replicas (ISR), они в точности копируют leader.

**Как происходит отправка сообщений?** У Producer есть функция send message. Оно состоит из следующих шагов:
1) **Fetch metadata.** Тут идём к zookeper и смотрим состояние кластера и расположение топиков. Тут есть синхронность (блокируется на 60 секунд)
2) **Сериализация сообщения.** Тут указываются сериализатор для ключей и для значений
3) **Выбор партиции.** Тут есть варианты:
	1) **Отправка в конкретную партицию**
	2) **Отдать определение партиции Kafka (round-robin)**
	3) **Key-value.** Партиция определяется как остаток хэша ключа при делении на число партиций
	4) **Сжимание сообщений.** Компрессируется по выбранному кодеку (compression.codec)
	5) **Аккумулируем батч.** Тут настраиваются batch.size (копим батч до превышения этого параметра, потом отправляем) и linger.ms (отправляем батч по истечении этого времени, даже если мы его не накопили). Можно отправлять и без превышения этих параметров, если суммарные батчи на брокер превышают batch.size

**Параметры отправки сообщений:**
1) **acks:**
	1) 0. Не ждём подтверждение отправки сообщений
	2) 1. Ждём подтверждения только от leader-реплики
	3) -1 (all). Ждём подтверждения от всех ISR
2) **delivery sematic support:**
	1) **at most once**
	2) **at least once**
	3) **exactly once**

**Как происходит получение данных?** Происходит через poll message. Оно состоит из следующих шагов:
1) **Fetch metadata**
2) **Читаем данные**

Вообще, можно распараллелить consumer-ов по группам и заставить их читать различные партиции одного топика. Для предотвращения повторного чтения сообщений в случае падения в брокере ведётся -consumer-offsets, где пишутся:
1) Partition
2) Group
3) Offset
Это помогает предотвращать повторное чтение. При этом потребитель должен подтвердить прочтение сообщения (тут есть auto commit и manual commit, можно ещё custom commit). Иногда ещё оффсет пропадает для группы. Если группа не подключается к партиции больше чем offsets.retention.minutes, то оффсет удаляется. Если группа потом ожила, то считывание продолжается в соответствии с параметром auto.offsets.resets.