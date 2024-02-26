# Highload TikTok
## Содержание
#### [1. Тема и целевая аудитория](#1-тема-и-целевая-аудитория)
#### [2. Расчет нагрузки](#2-расчет-нагрузки)

## 1. Тема и целевая аудитория

### Тема
TikTok - платформа для просмотра коротких видео. 

### Основной функционал сервиса
- Регистрация и авторизация
- Просмотр видео в ленте
    - Лента с рекомендованными видео    
    - Лента с видео авторов, на которых подписан пользователь
- Комментирование видео
- Лайки 
- Публикация видео
- Добавление в друзья
- Отправка/получение видео от друзей
- Подписки на других пользователей
- Поиск видео по ключевым словам (формирование ленты по результатам поиска)

### Основные продуктовые решения
- Ленты с видео формируются на основании предпочтений пользователя
- Ленты бесконечны, что должно сподвигнуть пользователя провести больше времени в приложении

### Целевая аудитория
- Весь мир.
- Пользователи:
    -  1.1 млрд. активыных пользователей в месяц \[[1](https://www.demandsage.com/tiktok-user-statistics/)]
    -  4.7 млрд. скачиваний \[[2]( https://www.omnicoreagency.com/tiktok-statistics/)]

- Распределение аудитории по странам \[[1](https://www.demandsage.com/tiktok-user-statistics/)]
  - Соединенные Штаты - 150 миллионов
  - Индонезия - 113 миллионов
  - Бразилия - 84.13 миллиона
  - Мексика - 62.44 миллиона
  - Россия - 51.24 миллиона
  - Вьетнам - 50.58 миллиона
  - Филиппины - 41.43 миллиона
  - Таиланд - 41.06 миллиона
  - Турция - 31.03 миллиона
  - Саудовская Аравия - 28.37 миллиона
  - Пакистан - 27.54 миллиона
  - Ирак - 25.51 миллиона
  - Египет - 25.5 миллиона

## 2. Расчет нагрузки

### Данные из открытых источников
- MAU - 1.1 млрд. пользователей \[[1](https://www.demandsage.com/tiktok-user-statistics/)]
- DAU - 750 млн. пользователей \[[3](https://www.businessofapps.com/data/tik-tok-statistics/)]
- Среднее время пользования приложением за день 90 мин. \[[4](https://inclient.ru/tiktok-stats/)]
- Средний размер 15 сек. видео 4мб. \[[5](https://blog.talkhome.co.uk/technology/how-much-data-does-tiktok-use/)]
- В день пользователи выкладывают 34 млн. видео \[[6](https://www.usesignhouse.com/blog/tiktok-stats)]
- Максимальный размер видео \[[6](https://wave.video/ru/blog/tiktok-video-size/)]

### Публикация видео
#### Продуктовые метрики
Средний месячный размер хранилища пользователя равен:
4 МБ * (34 млн видео / 750 млн пользователей) * 30 дней = 5.44 МБ.

Следовательно, средний размер хранилища пользователя:
5.44 МБ * 12 месяцев * 5 лет = 326 МБ (0.31 ГБ)

Среднее количество действий пользователя в день:
34 млн видео / 750 млн пользователей = 0.05 видео

#### Технические метрики
При публикации видео в 1 минуту пришлось около 400 запросов (7 МБ).

Таким образом, среднее количество запросов в секунду равно:
400 / 60 * 34000000 / (24 * 60 * 60) = 2623 RPS

Размер хранения публикаций видео:
0.31 ГБ * 750000000 / 1024 = 227050 Тб

Максимальный размер видео в тикток может быть 287.6 МБайт 6. Пиковое потребление в течении суток. Трафик по часам распределяется равномерно, потому что пользователи из разных часовых поясов, поэтому средний трафик от пикового не отличается, поэтому возьмем небольшой коэфицент k=1.5, на который умножим этот средний трафик, и получим пиковый:
(287.6 * 8 / 1000 / 1000) Тбит * 34 млн/д / (24 * 60 * 60) * 1.5 = 1.3581 Тбит/с

Суммарный суточный трафик (объем данных, передающихся через сети за сутки):
34 млн/д * 4 МБ / 1024 = 132812 Гбайт/д

### Просмотр ленты

#### Продуктовые метрики
Средний размер хранилища пользователя: 
Незначительный: требуется хранить id пользователя и что он смотрел. Не будем учитывать.

Средний размер видео 15 секунд, следовательно, при том что среднее время в приложении в день 90 минут, пользователь в среднем смотрит:
60 / 15 * 90 = 360 действий/день

#### Технические метрики
Размер хранения не учитываем из-за незначительных данных.

Среднее количество запросов в секунду равно, если при 5 минутном просмотре ленты отправляется около 1000 запросов:
1000 / (5 * 60) * 750000000 / (24 * 60 * 60) = 28935 RPS
За  5 минут постоянно листая в среднем получается 150 МБ на все запросы для просмотра ленты.

Пиковое потребление в течении суток. Трафик по часам распределяется равномерно, потому что пользователи из разных часовых поясов, поэтому средний трафик от пикового не отличается, поэтому возьмем небольшой коэфицент k=1.5, на который умножим этот средний трафик, и получим пиковый:
((((150 МБ / (5 * 60) секунд) Мбайт/с * 8 / 1000 / 1000) Тбит/с * (90 * 60) c) Тбит * 750 млн/д) Тбит/д / (24 * 60 * 60) Тбит/с * 1.5 = 281.25 Тбит/с

Суммарный суточный трафик:
((150 МБ / (5 * 60)) МБ/с / 1024 Гб/c * (90 * 60 c/д)) Гб/д * 750млн = 1977539062 Гбайт/день

### Итоговые таблицы

#### Продуктовые метрики:
| Действие         | Средний размер хранилища пользователя (ГБайт) | Среднее количество действий пользователя в день |
|------------------|-----------------------------------------------|-------------------------------------------------| 
| Публикация видео | 0.31                                          | 0.05                                            |
| Просмотр ленты   | Незначителен                                  | 360                                             |

#### Технические метрики
| Действие         | Размер хранения (Тб) | Пиковое потребление в течении суток (Тбит/с) | Суммарный суточный (Гбайт/д)  | RPS  |
|------------------|----------------------|----------------------------------------------|-----------------------------|------| 
| Публикация видео | 227050                 | 1.3581                                         | 132812 Гбайт/д           | 2623 |
| Просмотр ленты   | Незначителен         | 281.25                                          | 1977539062                 | 28935     |  


## Источники
1. https://www.demandsage.com/tiktok-user-statistics/
2. https://www.omnicoreagency.com/tiktok-statistics/
3. https://www.businessofapps.com/data/tik-tok-statistics/
4. https://inclient.ru/tiktok-stats/
5. https://blog.talkhome.co.uk/technology/how-much-data-does-tiktok-use/
6. https://www.usesignhouse.com/blog/tiktok-stats
7. https://wave.video/ru/blog/tiktok-video-size/