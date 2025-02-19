**Software requirements specification (SRS)** — один из самых важных документов ([[Документы]]) в разработке программного обеспечения. Он описывает работу ПО, его функции и нагрузки. Проще говоря, SRS предоставляет всем участникам дорожную карту для проекта. Спецификация требований программного обеспечения описывает функциональные и нефункциональные требования. Часто в документ включают варианты использования, которые иллюстрируют, как пользователь будет взаимодействовать с системой.

**Преимущества SRS:**
1) SRS является основой проекта. Документ закладывает базу, которой будут следовать все участники команды разработки.
2) Спецификации требований к программному обеспечению — это способ более четкой коммуникации. Этот инструмент помогает быть уверенным в том, что все участники процесса правильно понимают друг друга.
3) Написание SRS также может минимизировать общее время и затраты на разработку. Команды разработчиков встроенных систем особенно выигрывают от использования SRS.
4) Такая документация помогает избежать дальнейших улучшений и изменений в проекте, которые задерживают завершение или приводят к дополнительным расходам.

**Структура документа может включать в себя:**
1) Функциональные требования
2) Нефункциональные требования
3) Требования к интерфейсу
4) Модели данных
5) Зависимости (факторы, которые повлияют на srs. Например, в srs описано использование определенного ПО, и если это ПО окажется недоступно на стадии разработки, то потребуется внести соответствующие изменение в SRS)
6) Ограничения
7) Критерии приёмки
8) Глоссарии

**Пример типичной структуры документа SRS:**
1) **Введение.** Во введении объясняется значение SRS в целом, его возможности для вашей команды и его структура.
	1) **Цель.** Здесь объясните цель и структуру документации по программному обеспечению SRS: типы требований, которые будут рассмотрены, а также персонал, который будет ее использовать. Этот раздел должен быть коротким: достаточно 1-2 абзацев.
	2) **Целевая аудитория.** Вы можете углубиться и объяснить, как заинтересованные стороны и команды будут работать с SRS, а также участвовать в ее разработке.
	3) **Использование по назначению.** Опишите, в каких ситуациях ваша команда будет использовать SRS. Обычно его используют в следующих случаях:
		1) Проектирование и мозговой штурм новых функций
		2) Планирование продолжительности проекта, спринтов, оценка затрат
		3) Оценка рисков
		4) Мониторинг и измерение успеха команды
		5) Конфликтные ситуации, когда вовлеченные стороны имеют разное видение качественно выполненного продукта
	4) **Объём.** Рассматривается объем продукта, необходимо дать краткий обзор системы — её основное назначение, функции и положение. В этом разделе должны быть описаны:
		1) Ожидается, что все типы пользователей будут взаимодействовать с системой
		2) Все основные части архитектуры
	5) **Определения и сокращения**
2) **Общее описание.** Во второй части вы описываете читателям основные функции продукта, целевых пользователей и возможности системы. Это описание концентрируется только на ключевых функциях и архитектуре программного обеспечения, не вдаваясь в подробности о надстройках и соединениях.
	1) **Потребности пользователей.** Эта часть является вопросом выбора, поэтому некоторые организации предпочитают не включать ее в свою техническую документацию SRS. Потребности относятся к проблемам, которые пользователи смогут решить с помощью системы. Вы можете разделить эти потребности на подкатегории, если имеете дело с сильно сегментированной аудиторией
	2) **Допущения и зависимости.** Предположения — это предположения команды о продукте и его возможностях, которые будут правильными в 99% ситуаций. Естественно предположить, например, что платформа, помогающая водителям ориентироваться в ночное время, будет использоваться преимущественно в ночном режиме. Каково значение предположений? Они позволяют в первую очередь сосредоточиться на наиболее важных функциях приложения. Это предположение помогает понять, что дизайнеры должны разработать интерфейс, подходящий для видения в темноте, для помощника вождения в ночное время. Некоторые пользователи, безусловно, могут открыть приложение в течение дня, но это далеко не так, поэтому вам не нужно сразу включать связанные элементы в прототип.
3) **Особенности системы и требования.** В этой части подробно рассматриваются характеристики продукта и критерии исполнения. Поскольку предыдущие два раздела посвящены продукту в целом, здесь вы найдете более подробное описание.
	1) **Функциональные требования**
	2) **Требования к внешнему интерфейсу.** Описывают элементы страницы, которые будут видны конечному клиенту. Они могут включать в себя список страниц, элементы дизайна, ключевые стилистические темы, даже художественные элементы и многое другое, если они необходимы для продукта.
	3) **Системные требования.** Определяют условия, при которых он может использоваться. Обычно они относятся к аппаратным спецификациям и функциям. Требования к оборудованию SRS часто определяются минимальным и максимальным диапазонами, а также порогом оптимальной производительности продукта. Разработчики должны придерживаться требований к оборудованию, чтобы им не пришлось перезапускать проект позже. Мобильные приложения (с множеством переменных, которые необходимо учитывать) и приложения, требующие высокой реактивности (игры, любой продукт с VR/AR или IoT), особенно уязвимы.
	4) **Нефункциональные требования**

**Когда применять SRS?**
Наличие четкого набора требований гарантирует, что команда разработчиков создаст программное обеспечение, отвечающее потребностям клиента. SRS поможет оценить стоимость работ и охватить объем проекта. Он также дает программистам представление о технологическом стеке, который им понадобится, и помогает планировать работу. Дизайнеры получают представление о проекте через документы SRS, чтобы они могли адаптировать дизайн к варианту использования. Тестировщики получают рекомендации по созданию тестовых примеров, соответствующих потребностям бизнеса. На основании SRS можно составить содержательную презентацию для инвесторов: бизнес-процессы легко визуализировать для грамотной презентации проекта. Ещё SRS важен, потому что это единый источник информации, который предотвращает недопонимание как между менеджером проекта и командой, так и между заказчиком и аутсорс-компанией.

**В чём отличия SRS от других видов документации:**
1) **Специфичность.** SRS сосредотачивается исключительно на требованиях к программному продукту. Это документ, который формализует и подробно описывает, какие функции, характеристики и ограничения должны быть реализованы в программе. В отличие от других документов, SRS не включает в себя технические решения или архитектурные детали.
2) **Основное назначение.** SRS предназначено для создания единого понимания требований к программному продукту среди всех заинтересованных сторон, включая заказчика, менеджеров проекта, разработчиков и тестировщиков. Это служит основой для разработки, тестирования и управления рисками в процессе разработки программного продукта.
3) **Уровень детализации.** SRS обычно имеет высокий уровень детализации. Он описывает требования настолько подробно, чтобы разработчики могли понять, что именно нужно создать. Это в отличие от других видов документации, таких как концептуальные модели, которые могут быть менее подробными и абстрактными.
4) **Исключение технических деталей.** SRS не включает в себя технические детали реализации программы. Он описывает "что", но не "как". Технические решения и архитектурные детали обычно документируются в других видах документации, таких как технические спецификации или архитектурные диаграммы.
5) **Динамический характер.** SRS может подвергаться изменениям и обновлениям на протяжении всего жизненного цикла проекта. Это делается для адаптации к изменяющимся требованиям заказчика или среды проекта.
6) **Основа для контроля и тестирования.** SRS служит основой для контроля выполнения требований и разработки критериев тестирования. Он помогает убедиться, что программный продукт соответствует ожиданиям заказчика и функционирует корректно.

Что важно, SRS - это не священная корова, он может меняться и должен меняться в зависимости от методологии разработки, принятых в компании стандартов документации и прочего. Особенно выделяются два вида SRS: на основе [[RUP]] и на основе стандарта ISO/IEC/IEEE 29148.

**SRS на основе [[RUP]]:**
1) Описание требований будет интегрировано в этапы разработки RUP: инциализация, уточнение, построение и внедрение
2) Документация будет фокусироваться на преследовании итеративного и инкрементального подхода разработки
3) Разделение требований на варианты использования ([[Use Case]]), сценарии и более детальные спецификации
4) Уделение внимания описанию бизнес-процессов и архитектуры, поддерживая центральные принципы [[RUP]]

**SRS на основе стандарта ISO:**
1) Фокус на четкой структуре документа и форматировании
2) Уделение внимания классификации требований на функциональные и нефункциональные ([[Типы требований]])
3) Акцент на описании критериев успешности и верификации требований ([[Верификация требований]])
4) Особое внимание к идентификации и управлению изменениями в требованиях ([[Менеджмент требований]])