# SberIOS_Lesson2-GIT
Отличия Trunk-Based Development от Feature-подхода

Использование на проекте единого и стандартизированного подхода к разработке ПО необходимо для выстраивания эффективного командного взаимодействия, а так же чтобы проектный репозиторий не погрузился в полный хаос.
В настоящее время, для разработчиков использующих Git, самыми популярными подходами являются Trunk-based development и Feature-based development.

### Trunk-based development (TBD)
Основная идея этого подхода заключается в том, что разработка кода осуществляется на основе одной главной ветки «trunk» (или «master»). В любой момент эту ветку можно развернуть на проде, т.к. в ней лежит уже готовый к деплою код, прошедший стабилизацию.
Для разработки нового функционала создаются отдельные feature-ветки, которые живут не более двух дней.
#### Особенности Trunk-based development:
1. Feature Flags - некий рубильник для новых фич. Позволяет деплоить еще неготовый функционал, т.к. его можно просто «выключить» на проде и используется для проведения А/B тестов
2. Branch by abstraction - вместо создания веток для фич, создаются ветки на изменение одной абстракции. Разработка/доработка функционала происходит постепенно, небольшими «кусочками». Так же это позволяет быстро переключаться между задачами, работа над одной фичей не блокирует работу над другой, даже если первая не была закончена
3. Continuous Code Review - т.к. PR небольшие (благодаря концепции «Branch by abstraction»), их ревью занимает не более пары минут. Благодаря этой концепции происходит постоянный шаринг знаний между разработчиками команды - все понимают как меняется функционал, переиспользуют код, могут своевременно советовать друг другу лучшие практики
4. Все члены команды вливают свой код в trunk как минимум раз в день
5. В trunk ветке всегда находится код готовый к деплою на прод
6. Необходимо полное покрытие кода тестами, чтобы быть увереными в том, что весь функционал готов для релиза
7. Можно релизиться как можно чаще, в том числе несколько раз в день

### Feature-based development (FBD)
Основная идея Feature-based development заключается в том, что вся работа над новым функционалом производится в отдельной ветке, а не в ветке master. 
Такой подход позволяет избежать попадание нерабочего кода в master ветку, что делает разработку в большой команде безопаснее.

В основном выделяют следующие ветки:
- master - содержит стабильный протестированный код. Код в этой ветке всегда готов к деплою на прод.
- hotfix - на случай срочных исправлений на проде
- develop - основная ветка разработки
- release - ветка для подготовки сборки к релизу
- feature - создается под каждую новую фичу, когда разработка заканчивается мержится в ветку develop (после прохождения код ревью)

#### Особенности Feature-based development:
1. Все новые изменения делаются в отдельных feature ветках
2. Функционал из feature ветки попадает в master только после полного завершения работ над ним
3. Код ревью может занимать много времени, т.к. часто приходится ревьювить большие PR
4. Большие функции могут потратить дни на мерж и резолв конфликтов
5. Хорошо подходит для проектов, где релизы делаются раз в несколько недель

### Заключение
Feature-подход используется многими распределенными командами, которые имеют разные уровни квалификации. Сопровождающие проекта могут проводить код ревью и утверждать каждую строку кода в релизы. TBD же лучше всего работает когда команда состоит из опытных разработчиков, т.к. доступ к мержу в главную ветку есть у любого разработчика.

TBD позволяет релизить новый функционал быстрее, благодаря применяемым в разработке концепциям.  Feature-подход может замедлять работу, когда приходится ревьювить большие пулл реквесты. Релизы достаточно сложно делать чаще, чем раз в неделю.
Если проект относительно небольшой и над ним работает немногочисленная команда разработчиков, то применение FBD может только усложнить процесс разработки.
