**DevOps (DEVelopment OPeration)** – это набор практик для повышения эффективности процессов разработки (Development) и эксплуатации (Operation) ПО за счет их непрерывной интеграции и активного взаимодействия профильных специалистов с помощью инструментов автоматизации ([[Направления в IT]]).

**Цели DevOps:**
1) Сокращение времени для выхода на рынок
2) Снижение частоты отказов новых релизов
3) Сокращение времени выполнения исправлений
4) Уменьшение количества времени на восстановление при сбое новой версии или другиз случаях отключения текущей системы

**Задачи DevOps:**
1) Согласование процессов разработки и поставки ПО с эксплуатацией
2) Автоматизация процессов разработки, тестирования и развёртывания
3) Непрерывное тестирование качества приложений
4) Непрерывный мониторинг производительности приложений и состояния инфраструктуры

Таким образом, DevOps нацелен на предсказуемость, эффективность, безопасность и ремонтопригодность операционных процессов, а также регулярную поставку надежно работающего продукта, его обновлений и обслуживания.

ДевОпс (DevOps) инженеры - это специалисты, которые работают в области DevOps, методологии, направленной на автоматизацию и оптимизацию процессов разработки, тестирования и развертывания программного обеспечения. Эти инженеры играют ключевую роль в объединении разработки (Development) и эксплуатации (Operations) для достижения более быстрой и надежной поставки приложений.

**Обязанности и задачи DevOps-инженера:**
1) **Автоматизация процессов.** Создание скриптов и инструментов для автоматизации развертывания, тестирования и управления приложениями, чтобы уменьшить ручную работу и повысить эффективность
2) **Контейнеризация.** Использование контейнеров, таких как Docker, для обеспечения портабельности приложений и их более легкого развертывания
3) **Управление конфигурацией.** Создание и поддержка инфраструктуры как кода (Infrastructure as Code, IaC), чтобы управлять конфигурациями серверов и ресурсов с использованием кода
4) **Непрерывная интеграция и непрерывная доставка (CI/CD).** Разработка и настройка систем CI/CD для автоматической сборки, тестирования и развертывания кода в рамках непрерывного цикла разработки
5) **Мониторинг и журналирование.** Настройка инструментов мониторинга и журналирования для отслеживания производительности приложений и выявления проблем
6) **Обеспечение безопасности.** Забота о безопасности приложений и инфраструктуры, включая сканирование на уязвимости и настройку брандмауэров
7) **Резервное копирование и восстановление.** Разработка стратегий резервного копирования и восстановления данных, чтобы обеспечить надежность и доступность приложений
8) **Сотрудничество.** Работа в тесной связи с командами разработки, тестирования и операций для обеспечения согласованности и совместной работы
9) **Анализ и оптимизация.** Мониторинг производительности системы и поиск способов ее улучшения и оптимизации

Девопс инженеры играют важную роль в обеспечении непрерывной поставки приложений, ускоряя процессы разработки и улучшая качество и надежность программного обеспечения. Они обычно обладают знаниями в области автоматизации, системного администрирования, разработки и безопасности, а также способны работать в команде и быстро реагировать на изменения и проблемы.

Gitflow является методологией работы с Git. Это значит, она определяет, какие ветки нужно создать и как производить их слияние.

**Ключевые идеи, которые нужно запомнить о Gitflow:**
1) Данная модель отлично подходит для организации рабочего процесса на основе релизов
2) Gitflow предлагает создание отдельной ветки для исправлений ошибок в продуктовой среде

**Последовательность работы при Gitflow:**
1) Из master создаётся ветка develop
2) Из develop создаются ветки feature
3) Когда разработка новой функциональности завершена, она объединяется с веткой develop
4) Из develop создаётся ветка release
5) Когда ветка релиза готова, она объединяется с develop и master
6) Если в master обнаружена проблема, из неё создаётся ветка hotfix
7) Как только исправление на ветке hotfix завершено, она объединяется с develop и master

Каждая новая функциональность должна разрабатываться в отдельной ветке, которую можно отправлять в центральный репозиторий для создания резервной копии/для совместной работы команды. Ветки функций создаются не на основе master, a на основе develop. Когда работа над новой функциональностью завершена, она вливается назад в develop. Новый код не должен отправляться напрямую в master.

Когда в ветку develop уже слито достаточно нового кода для релиза (или подходит установленная дата предрелиза), от ветки develop создается ветка release. Создание данной ветки означает начало следующего цикла релиза, в ходе которой новая функциональность уже не добавляется, а производится только отладка багов, создание документации и решение других задач, связанных с релизом. Когда все готово, ветка release сливается в master, и ей присваивается тег с версией. Кроме этого, она должна быть также слита обратно в ветку develop, в которой с момента создания ветки релиза могли добавляться изменения с момента создания ветки релиза.

Использование отдельной ветки для подготовки релиза позволяет одной команде дорабатывать текущий релиз пока другая команда уже работает над функциональностью для следующего релиза. Это также позволяет разграничить этапы разработки (например, легко сказать: «На этой неделе мы готовимся к версии 4.0» и фактически увидеть это в структуре репозитория).

Ветки hotfix используются для быстрого внесения исправлений в рабочую версию кода. Ветки hotfix очень похожи на ветки release и feature, за исключением того, что они созданы от master, а не от develop. Это единственная ветка, которая должна быть создана непосредственно от master. Как только исправление завершено, ветка hotfix должна быть объединена как с master, так и с develop (или с веткой текущего релиза), а master должен быть помечен обновленным номером версии. Наличие специальной ветки для исправления ошибок позволяет команде решать проблемы, не прерывая остальную часть рабочего процесса и не ожидая следующего цикла подготовки к релизу. Можно говорить о ветках hotfix как об особых ветках relese, которые работают напрямую с master.

**Continuous Integration (CI, Непрерывная интеграция)** - это практика, при которой код разработчиков регулярно интегрируется в общий репозиторий и автоматически проверяется с использованием тестов. Основная цель CI - обеспечить раннее выявление и устранение конфликтов и ошибок в коде. Короткоживущие функциональные ветки, команда сливает их с основной веткой разработки по несколько раз в день, процессы сборки и тестирования полностью автоматизированы, результат имеем в пределах 10 минут; развертывание выполняется вручную.

**Continuous Delivery (CD, Непрерывная доставка)** -  автоматизируется CI + весь процесс релиза ПО. Может состоять из нескольких этапов. Развертывание в продакшен выполняется вручную. Это позволяет быстро и безопасно выпускать новые версии приложения, готовые к продакшену.

**Continuous Deployment (CD, Непрерывное развертывание)** - CI + CD + полностью автоматизированное развертывание в продакшен. C Deployment является расширением C Delivery. В этом случае каждое успешное изменение автоматически развертывается в продукционную среду без необходимости вмешательства операторов. Это позволяет быстро доставлять новый функционал пользователям.

**Отличие CI/CD/CD:**
1) **CI** фокусируется на интеграции кода и его автоматической проверке
2) **Continious Delivery** включает в себя CI и добавляет автоматическое развёртывание в тестовое окружение
3) **Continious Deployment** идёт дальше и автоматически разворачивает код в продукционной среде после успешного прохождения тестов

Jenkins, TFS (Team Foundation Server), и TeamCity - это системы для автоматизации процессов сборки, тестирования и развертывания программного обеспечения. Вот краткое описание каждой из них:
1) **Jenkins:**
	1) **Цель.** Jenkins - это средство непрерывной интеграции (CI), которое используется для автоматизации процесса сборки и тестирования кода
	2) **Функции:**
		1) Интеграция с множеством инструментов и плагинов
		2) Автоматическое выполнение сборки и тестирования кода при каждом обновлении в репозитории
		3) Визуализация результатов сборки и уведомления о проблемах
		4) Планирование и управление задачами CI/CD
	3) **Гибкость.** enkins предоставляет высокую степень гибкости и настраиваемости благодаря обширной библиотеке плагинов
2) **TFS (Team Foundation Server):**
	1) **Цель.** TFS, разработанный Microsoft (в последующих версиях заменен Azure DevOps), предоставляет средства для управления исходным кодом, сборкой, тестированием и управлением задачами
	2) **Функции:**
		1) Хранение исходного кода и управление версиями
		2) Непрерывная интеграция и доставка (CI/CD)
		3) Отслеживание задач и управление проектами
		4) Встроенные инструменты для разработки, тестирования и отчетности
	3) **Интеграция.** TFS интегрирован с другими инструментами Microsoft, такими как Visual Studio и Azure, и может использоваться для разработки .NET-приложений и приложений на других платформах
3) **TeamCity:**
	1) **Цель.** TeamCity, разработанный JetBrains, также предоставляет средства для автоматизации процессов CI/CD
	2) **Функции:**
		1) Автоматическая сборка, тестирование и развертывание кода
		2) Уведомления и отчеты о состоянии сборок
		3) Поддержка множества языков и платформ разработки
		4) Интеграция с системами управления версиями, такими как Git и SVN
	3) **Производительность.** TeamCity известен своей производительностью и способностью поддерживать одновременную сборку и развертывание большого количества проектов

Kubernetes и Docker - это два популярных инструмента, используемых в сфере контейнеризации и управления контейнерами для приложений. Они выполняют разные, но взаимосвязанные функции:
1) **Docker:**
	1) **Контейнеризация приложений.** Docker позволяет упаковать приложение и все его зависимости (библиотеки, конфигурацию и другие ресурсы) в контейнер. Этот контейнер становится переносимым и может быть запущен на любой системе, поддерживающей Docker
	2) **Изоляция.** Docker контейнеры обеспечивают изоляцию между приложениями и их зависимостями, что упрощает управление конфликтами между разными версиями
	3) **Управление версиями.** Docker облегчает управление версиями приложения и его зависимостями, позволяя быстро переключаться между разными версиями
	4) **Легковесность.** Контейнеры Docker обладают небольшим объемом и быстрым временем запуска, что делает их идеальными для масштабируемых микросервисных архитектур
2) **Kubernetes:**
	1) **Оркестрация контейнерами.** Kubernetes предоставляет средства для автоматического развертывания, масштабирования и управления контейнерами Docker в крупных распределенных приложениях
	2) **Управление ресурсами.** Kubernetes позволяет распределять ресурсы (например, CPU и память) между контейнерами и автоматически масштабировать приложение в зависимости от нагрузки
	3) **Высокая доступность.** Kubernetes обеспечивает резервное копирование и высокую доступность приложений, позволяя им работать непрерывно даже в случае сбоев
	4) **Обновления приложений.** Kubernetes предоставляет инструменты для обновления приложений без простоя, что позволяет внедрять новые версии приложения без остановки текущей версии
Итак, Docker используется для контейнеризации приложений и их зависимостей, а Kubernetes - для управления и развертывания контейнеров в распределенных приложениях. Оба инструмента вместе обеспечивают мощное решение для создания, развертывания и масштабирования приложений в современных инфраструктурах.