# OrderBookScreener
Торгово-аналитический терминал на основе Finam Trade API

Программа разработана для участия в хакатоне, категория: «Неторговые разработки на основе Trade API»

Скринер стаканов - позволяет подписываться на большое количество стаканов и искать среди них крупные заявки.
При этом программа не требовательна к ресурсам компьютера.

При запуске программа подписывается на стаканы всех российских акций (TQBR), фьючерсов (FUT) и валют (CETS). В процессе обновления данных по стаканам идет поиск самых крупных заявок, расчет спреда.
В таблице колонка 'Крупная заявка' - отображает число во сколько раз найденная заявка больше средней заявки в стакане. Чем больше эта цифра, тем крупнее заявка.

Данная программа будет полезна трейдерам-скальперам, которые торгуют на основе стакана, для поиска крупных заявок, от которых возможен в дальнейшем отскок цены.
Также программа будет полезна высокочастотным алготрейдерам, для быстрого поиска крупных заявок, анализа поведения цен вокруг крупных заявок и на основе этого разработка торговых идей.

<img src="https://github.com/VozyakovAV/OrderBookScreener/blob/main/ReadmeResources/main.png" />

## Возможности
- Подписка на стаканы по акциям, фьючерсам, валютам
- Поиск крупных заявок среди всех подписанных стаканов
- Расчет спреда всех стаканов
- Фильтр по названию инструмента и по типу инструмента
- Просмотр портфеля: деньги, позиции, заявки
- Выставление и снятие заявки
- Бонус1: получение дополнительной информации по инструменту из API мосбиржи (оборот за день в деньгах и контрактах)

## Требования
- Операционная система Windows
- Фреймворк .Net 6

## Технические особенности
- Программа разработана на фреймворке .Net6, код на C#, визуальная часть на WPF
- Класс FinamClient реализует взаимодействие с Finam Api по протоколу gRPC
- Взаимодействие с клиентом (FinamClient) реализовано через интерфейс IConnector, что позволяет в дальнейшем легко подключить другой поставщик данных, например, криптобиржу
- При запуске программы идет подписка на все российские акции (TQBR), фьючерсы (FUT) и валюты (CETS). Данные поступают в очередь и обрабатываются без задержки в отдельном потоке, что не нагружает систему

## Запуск
### Скачать готовый релиз
- Скачать последний релиз https://github.com/VozyakovAV/OrderBookScreener/releases
- Распаковать zip файл
- Запустить OrderBookScreener.exe

Программа запустится с настройками по умолчанию, доступен только просмотр инструментов и заявок.

Чтобы указать свой токен смотрите настройку файла config.txt

### Запуск из Visual Studio
- Скачать проект
- Открыть OrderBookScreener.sln
- Запустить проект (F5)

## Настройка файла config.txt
В файле config.txt указывается токен к Trade Api и клиентский код.

По указанным настройкам программа будет получать инструменты и подписываться на стаканы.

Если токен имеет разрешение на работу с портфелем, то дополнительно в программе будет доступен просмотр баланса, позиций и заявок, a так же можно будет выставлять и снимать заявки

```json
{
  "Token": "<Токен от Trade API>",
  "ClientId": "<Торговый код клиента>"
}
```
