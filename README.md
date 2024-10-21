# HighLoadTechnoPark
Репозиторий работы по высоконагруженным системам Технопарка от ВК

# Тип сервиса
Онлайн кинотеатр, аналогом которого является Кинопоиск 
# MVP
1) Регистрация и авторизация пользователя.
Описание: Сервис будет предоставлять возможность регистрации и авторизации на сайте.
2) Поиск фильма или сериала в каталоге.
Описание: Поиск по описанию или по названию фильма/сериала.
3) Просмотр описания и комментариев видеоматериала.
Описание: Существует возможность до просмотра ознакомиться с контентом, а так же в случае покупки подписки можно прочитать комментарии профессиональных кинокритиков.
4) Просмотр видеоматериала.
Описание: Просмотр в 4k только для зрителей с платной подпиской и 1080p для остальных пользователей, с условием ограниченного доступа к видеоматериалам.
5) Выставление оценки видеоматериалу.
Описание: Для зарегистрированных пользователей существует возможность поставить оценку и написать комментарий после просмотра.
6) Подписка.
Описание: Подписка (1/6/12/24 месяцев) для просмотра в 4к, а также приобретение определенного видеоматериала.
# Целевая аудитория
Пользователями являются граждане России и СНГ возраста от 12 до 65 лет. Около 25 млн и 10 млн постоянных пользователей России и СНГ соответсвенно, а также около 3-4 млн и 2 млн пользователей ежедневно.

### Рисунок 1 (географическое расположение пользователей сервиса [1])
![image](https://github.com/user-attachments/assets/ebf25d48-de9a-46a1-917a-e1b4e0fcae6f)

# Продуктовые метрики

| Месячная аудитория  | Дневная аудитория |
| ------------- | ------------- | 
| 22 млн [2] | 2.5 млн [2] |

## Подсчет размера хранилища:
Из источника номер три следует, что всего 80 тысяч единиц контента. В среднем серия сериала 4k длительностью час весит 20 Гб, а полноценный фильм 4k длительностью 2,5 часа около 50 Гб следовательно 35 Гб в среднем для материала в разрешении 4к, а значит **3 петабайта для 4к** данных весит вся библиотека Кинопоиска. Однако на серверах будут храниться не только копии 4к, но и копии 1080р и 360р. Приблизительные коэффициенты уменьшения размера файла для различных разрешений: 1/4 от размера файла 4K для 1080р и 1/18 от размера файла 4K для 360р, таким образом получаются значения 7 Гб * 80000 = 560000 ГБ = 560 ТБ = **0,56 ПБ
для 1080р** и 1.75 Гб * 80000 = 140000 ГБ = 140 ТБ = **0,14 ПБ для 360р**. Соответственно **размер общего хранилища получается 3,7 Пб**. Некоторые тайтлы, выпущенные за долго до 2020-х и имеющие максимальное разрешение 360р, были искусственно улучшены нейросетями и доведены до качества 1080р или выше, что позволяет при вычислении объема хранилища пренебречь материалами, которые не изначально не имеют качетсво 1080 и выше.
Для того, чтобы хранить персональные данные пользователя нужно понимать, что он может включать текстовую информацию (имя, возраст, биография), а также фотографии. Текстовые данные занимают несколько килобайт, а фотографии могут варьироваться от 100 Кб до нескольких мегабайт. Так с верхней оценкой по этому параметру как 20 Мб, то **20 Мб** на пользователя в среднем.
Всего на храниение данных пользователя требуется выделить около **0,5 Тб**. 
Одна рецензия ограничена 2 тысячами символов, таким образом в ASCII одна рецензия весит не более 2 Кб, следовательно 2*827824 = 1655648 Кб = 1,6 Гб. Для запаса выделим **2 Гб** для того, чтобы там же хранить оценки от 1 до 10.
| Размер хранилища на человека | Размер хранилища на всех пользователей | Размер хранилища на весь видеоконтент | Размер хранилища на рецензии и оценок |
| ------------- | ------------- | ------------- | ------------- |
| 20 Мб | 0.5 Тб | 3,7 Пб | 2 Гб |


## Подсчет среднего количества действий пользователя по типам в день:
Регистрацию нет смысла считать, а авторизацию за день человек делает в среднем **1 раз**, так как в сервисе для просмотра **требуется авторизация как минимум**.
Покупает человек подписку раз в пару месяцев, значит **0.16 раз** в день. 
В 2023-м каждый подписчик в среднем увидел в онлайн-кинотеатре 34,5 тайтлов. Больше всего подписчики смотрели фильмы — в среднем по 22,6 фильма.) Таким образов в месяц это 2.9 тайтла (для простоты это будут фильмы [4] в месяц, значит 1/10 фильма в день или **16-18 минут**.
За 2023 год в среднем в месяц было 180 млн оценок [5], таким образом 6 млн оценок в день или **0.27 оценок** у одного пользователя в день.
Всего рецензий 827824, ежедневно публикуются сотни [6]. Таким образом пусть будет в среднем 400 рецензий в день, следовательно **0.000018** в день на человека.
Поиск контента пользователь использует около **3-4** раз в день.

## Таблица подсчетов
| Действие пользователя | Частота действий в день |
| ------------- | ------------- | 
| Регистрация и авторизация | 1 |
| Покупка подписки | 0.16 |
| Поиск видеоматериала | 4 |
| Оставление комментария | 0.000018 |
| Просмотр видеоматериала | 16-18 минут |
| Оценка видеоматериала | 0.27 |


# Технические метрики

## RPS в разбивке по типам запросов
| Действие  | Формула | RPS |
| ------------- | ------------- | ------------- |
| Регистрация и авторизация  | 1*2500000/86400  | 29  |
| Поиск фильма  | 4*2500000/86400  | 115 |
| Оставление комментария | 0.000018*2500000/86400 | 0.0005 |
| Просмотр видеоматериала  | (17*60)*2500000/84600 | 30141 |
| Платная подписка  | 0.16*2500000/86400 | 4.6 |
| Оценка видеоматериала | 0.27*2500000/86400 | 7.8 |

## Сетевой трафик:
Битрейт видео на КиноПоиске может варьироваться в зависимости от качества контента и конкретного фильма или сериала. Обычно для потокового видео в HD разрешении битрейт составляет от 3 до 5 Мбит/с, а для 4K — от 15 до 25 Мбит/с. Ввиду того, что с платной подпиской нашим сервисом пользуется только 50% пользователей, но при этом 80% из них потребляют контент либо с мобильного телефона, либо с ноутбука с разрешением 1080р, то целесообразно вычислить 10%-ный общий трафик, использующий формат 4к. Для этих **10% для расчета будут взяты 20 Мбит/c**. Остальные же **90% будут использовать 3 Мбит/c** с погрешностью на просмотр 360р при плохом интернет соединении. Дневная аудитория 2.5 млн и каджый проводит около 17 минут за просмотром контента. В результате расчета будет 43 млн минут в день. 
Расчет:
* Формула для 10%: (4.300.000*60)*20 = 5 160 000 000 Мбит за весь день или **0,645 как суммарный сетевой трафик на 4к видеоматериал**.
* Формула для 90%: (38.700.000*60)*3 = 6 966 000 000 Мбит за весь день или **0,871 как суммарный сетевой трафик на 1080р и 360р видеоматериал**.
  
Пиковые нагрузки на сервис ориентировочно будут по вечерам буднечных дней или будут на выходных (возможны стихийные изменения как, например, финал ЛЧ по футболу или релиз новой серии популярного сериала, но под такие случаи выделяется дополнительное железо на некоторое время). Это время, когда большинство людей заканчивают работу и начинают отдыхать. Люди могут иметь привычку использовать интернет в вечернее время для развлечения. В моменты пиковой нагрузки возрастать среднее значение сетевого трафика будет **примерно втрое** из-за вышеперечисленного паттерна. 
Для 10% таким образом получается **60 Гбит/с** как среднее значение (5160000/(24*60*60)=60 Гбит/c), а пиковое значение является средним, умноженным на 3, то есть **180 Гбит/с**.
Для 90% таким образом получается **80 Гбит/с** как среднее значение (6966000/(24*60*60)=80 Гбит/c), а пиковое значение является средним, умноженным на 3, то есть **240 Гбит/с**.
Остальные же три минуты в сервисе выполняются оставшиеся действия из мвп.


## Сетевой трафик 10% - обычный (78 Гбит/с)
| Действие  | Скорость трафика |
| ------------- | ------------- |
| Просмотр видеоматериала  | 60 Гбит/с |
| Регистрация и авторизация  | 3 Гбит/c | 
| Поиск фильма  | 8 Гбит/c | 
| Оставление комментария | 5 Гбит/c |
| Платная подписка  | 1 Гбит/c |
| Оценка видеоматериала | 1 Гбит/c|

## Сетевой трафик 10% - пиковый  (235 Гбит/с)
| Действие  | Скорость трафика |
| ------------- | ------------- |
| Просмотр видеоматериала  | 180 Гбит/с |
| Регистрация и авторизация  | 10 Гбит/c | 
| Поиск фильма  | 24 Гбит/c | 
| Оставление комментария | 15 Гбит/c |
| Платная подписка  | 3 Гбит/c |
| Оценка видеоматериала | 3 Гбит/c |


## Сетевой трафик 90% - обычный (98 Гбит/с)
| Действие  | Скорость трафика |
| ------------- | ------------- |
| Просмотр видеоматериала  | 80 Гбит/с |
| Регистрация и авторизация  | 3 Гбит/c | 
| Поиск фильма  | 8 Гбит/c | 
| Оставление комментария | 5 Гбит/c |
| Платная подписка  | 1 Гбит/c |
| Оценка видеоматериала | 1 Гбит/c|

## Сетевой трафик 90% - пиковый  (298 Гбит/с)
| Действие  | Скорость трафика |
| ------------- | ------------- |
| Просмотр видеоматериала  | 240 Гбит/с |
| Регистрация и авторизация  | 10 Гбит/c | 
| Поиск фильма  | 24 Гбит/c | 
| Оставление комментария | 15 Гбит/c |
| Платная подписка  | 3 Гбит/c |
| Оценка видеоматериала | 3 Гбит/c |

# Глобальная балансировка нагрузки
## Функциональное разбиение по доменам
Для примера доменное имя моего сервиса будет **FilmHub.ru**.
Сервис будет работать на домеенных зонах Казахстана и Беларуси: 
* **FilmHub.kz**
* **FilmHub.by**

Все версии, которые будут расмотренны далее, кроме comments.Filmhub.ru, будут иметь аналоги и в доменных зонах остальных двух стран.
Тогда для мобильных пользователей, которые составляют около 50% от общего числа пользователей, будет **m.FilmHub.ru**, который оптимизирован для работы с мобильными устройствами. Домен **passport.FilmHub.ru** выполняет аутентификацию пользователей. А также **api.Film.ru** для интеграции с сервисами оплаты или рекламы. **comments.Filmhub.ru** для комментариев. 

## Обоснования расположения ДЦ
Дата центры обязательно распологаются в столицах: Москва, Астана, Минск, как наибольшее скокпление ЦА. Ввиду огромной территории РФ и наличия большей части аудитории именно оттуда, то стоит расположить так же ДЦ по всей России в крупных городах, таких как: Санкт-Петербург, Краснодар, Казань, Екатеринбург, Новосибирск, Красноярск, Якутск, Хабаровск и Магадан и Новый Уренгой. Эти города наиболее лучшим образом покрывают всю территорию РФ. Еще добавим Алматы из Казахстана для более качественного покрытия Казахстана. 
### Рисунок 2 (схема распределения ДЦ)

![image](https://github.com/user-attachments/assets/852b3e4d-a198-41fb-8a8b-de87bad419b9)

Ссылка на Яндекс Карту: https://yandex.ru/maps/?um=constructor%3A503b82edec1e14fae8d2530b4f6322524f3c2279ef57a085767b4b01a5968f02&source=constructorLink

## Расчет распределения запросов из секции "Расчет нагрузки" по типам запросов по датацентрам
Каждый ДЦ хранит полный объем видеоматериала, доступного на сервисе, поэтому запрос на просмотр или поиск фильма отправляется на ближайший ДЦ. Однако регистрация и авторизация, а также запрос на оформление платной подписки пользователя доступны только в Москве, Питере, Минске, Астане и Красноярске (рисунок 3). Так что соседние ДЦ проксируют запросы на авторизацию, регистрацию и оформление платной подписки на ближайший ДЦ с менее загруженным сервером авторизации (Например: Краснодар - Минск, Новый Уренгой - Питер, Магадан - Красноярск). Для согласованности данных во всех ДЦ запрос на оставление комментария и на оценку видеоматериала возможен через ДЦ Москвы (рисунок 4). Запросы будут балансироваться на уровне DNS благодаря записям passport.FilmHub.ru, которая выполняет авторизацию и регистрацию, api.Film.ru, которая реализует для интеграции с сервисами оплаты или рекламы, а также 

### Рисунок 3  (красным выделены ДЦ с возможностью запросов на регистрацию, авторизацию и оформление платной подписки)
![image](https://github.com/user-attachments/assets/e1551d8b-e77f-4eab-b1b2-840680e3880d)


### Рисунок 4 (красным выделены ДЦ с возможностью запросов на оставление комментария и оценки)

![image](https://github.com/user-attachments/assets/64a3d868-215e-4285-b0cd-b8b13c5f684e)


## Схема DNS балансировки
**Latency-based DNS (GeoDNS)** позволит выдавать адрес ближайшего ДЦ с минимальным RTT, на что и рассчитано расположение наших ДЦ. 


## Механизм регулировки трафика между ДЦ
Если ближайший с физической точки зрения сервер перегружен, то запрос отправиться по **Based latancy balancing**, например человек из города Чита направляет запрос на ДЦ Красноярска, однако тот перегружен. В этом случае запрос пользователя будет направлен на сервер с минимальной задержкой, например это будет ДЦ Хабаровска. Этот пример иллюстрирует наглядно механизм регулировки трафика между ДЦ в критических случаях, который может продолжаться и более чем в две итерации.


# Локальная балансировка нагрузки

## Схема маршрута при локальной балансировке

![image](https://github.com/user-attachments/assets/6a7e33d4-8459-4420-9538-ebaef67e2d3d)


## L4
Был выбран VS IP tunneling, так как балансировщик инкапсулирует сообщения, после обработки которых не требуется возвращение через балансировщик. Что позволяет убрать лишний трафик в приложении и разгрузить балансировщик для выполнения полезной работы, что в общем повышает производительность системы. CARP (Common Address Redundancy Protocol) объединяет несколько устройств в группу, определяя master устройство, после чего начинают работу. Если master выходит из строя, то один из резервных берёт на себя его функции. Чаще всего в группе будет пара балансировщиков на случай выхода одного из строя. Проверка сервера на доступность будет происходить специальным запросом (health check) определенной кастомной пустой функции. L4 балансировщик выбирает наименее загруженный Nginx и отправляет запрос туда. 

## L7
Выбор пал на Nginx ввиду его универсальности и способности качественной работы с "медленными клиентами". Reverse-proxy выполняет следующие действия:

**Кэширование:** реверс прокси nginx может кэшировать ответы от серверов-источников, чтобы уменьшить количество запросов к серверам-источникам и ускорить время ответа.

**Сжатие:** реверс прокси nginx может сжимать ответы от серверов-источников, чтобы уменьшить объем передаваемых данных.

**Защита:** реверс прокси nginx может выполнять функции защиты, такие как проверка подлинности и авторизация, чтобы ограничить доступ к серверам-источникам. Защита от DDos.

**Мониторинг:** реверс прокси nginx может мониторить состояние серверов-источников и автоматически переключаться на другой сервер, если один из них становится недоступным.

**Работа с https/http:** расшифровывает https запросы и после передает серверам http запросы.

После Nginx проксирует запрос на соответсвующий кластер, определяемый по заголовку.

## Kubernetes
Для того, чтобы разворачивать многочисленные экземпляры программного обеспечения будет использоваться kubernetes. Основными сущностями, с которыми работает kubernetes:
* Pod: Это основная единица в Kubernetes, представляющая собой один или несколько контейнеров, которые совместно используют сетевые и хранилищные ресурсы. Чаще всего Pod содержит один контейнер.
* Node: Физический или виртуальный сервер, на котором запускаются Pods.
* Cluster: Набор узлов (Nodes), объединенных в единое целое для запуска контейнерных приложений. В кластере Kubernetes есть как минимум один мастер-узел и несколько рабочих узлов.

Kubernetes автоматически выполняет рутинные действия, запуская кластеры с определенными конфигурациями. А также имеется auto-scalling, что позволяет полноценно использовать ресурсы hardware. Kubernetes предоставляет возможности балансировки нагрузки, которые распределяют входящий трафик между несколькими репликами контейнера. Kubernetes может автоматически обнаруживать и перезапускать контейнеры, которые упали или становятся недоступными. Очень эффективно и удобно для реализации программного обеспечения сервиса.
Для реализации сервисов выполняющих авторизацию и регистрацию, сервисов выполняющих оформление платной подписки на соответсвующем дата-центре Москвы, Питера, Минска, Астаны и Красноярска будет развернут отдельный кластер с повышенной безопасностью. Кроме того московский ДЦ в отдельном кластере разворачивает сервис, позволяющий комментировать и ставить оценки, для того чтобы улучшить праметры безопасности и изоляции от других сервисов. k8s берет на себя распределение и перераспределение физических ресурсов, обеспечивая непрерывную работу сервисов, посредством их контейнеризации.

# Логическая схема БД

![image](https://github.com/user-attachments/assets/8e978be5-f399-44a9-987e-71caf6ba79a3)

### Схема связей

* Films (1) <--- (M) Reviews
* Films (1) <--- (M) Film_ Genres (M) ---> (1) Genres
* Films (1) <--- (M) Film_Actors (M) ---> (1) Actors
* Users (1) <--- (M) Reviews
* Users (1) <--- (1) Avatars
* Actors (1) <--- (M) Photos
* User (1) <--- (M) Session

### Расчет размера данных и нагрузки на чтение/запись

| Таблица |	Размеры данных |	Консистентность | Нагрузка на чтение (RPS) | Нагрузка на запись (RPS) |
|--------------| ----------------| --------------|----------------| --------------|
| Films | ~500 байт на 1 фильм * 80 тысяч единиц контента * 4 разрешения = **0.148 ГБ**| при удалении фильма удаляются все film_actors и film_geners, reviews | 30141/18/60=28 | 10 |
| Actors |  ~480 байт * 80 000 человек = **0.0373 GB** | при удалении удаляются все photos и Film_Actors | 30141/18/60=28 | 10 |
| Users | ~500 байт * 22 млн = **10.24 GB** | при удалении удаляются все avatars и rewies, session | 29 | 29 |
| Reviews | ~400 байт * 180 млн оценок = **67.11 GB** | - | 30141/18/60=28 | 0.0005 |
| Genres | ~150 байт * 100 =  **0.000014 GB** | удаляюся все Film_Genres | 30141/18/60=28 | 0 |
| Photos | ~250 байт * 22 000 * 1/3 = **000.1705 GB**| - | 30141/18/60=28 | 3 |
| Avatars | ~250 байт * 100 000 = **0.0233 GB**| - | 29 | 0.5 |
| Film_Actors | ~16 байт * 200 000 записей = **0.00298 GB**  | - | 30141/18/60=28 | 10+10=20 |
| Film_Geners | ~12 байт * 160 тысяч единиц контента * 3 = **0.00534 GB**| - | 30141/18/60=28 | 10 |
| Session |  ~324 байта * 365 * 2 500 000 = **275.6 ГБ** | - | 29 | 145 |

Кинопоиск существует с 7 ноября 2003, то есть 7650 дней. Всего 80 000 тайтлов => добавляется примерно 10 тайтлов в день. Всего актеров около 80 000 => 10 новых актеров в день. Новые жанры не придумываются почти никогда => 0. 22 000 фоток => 3 фотки в день.
Avatars нагрузка на запись примерные значения, исходя из поведения пользователей.
При авторизации пользователь получает jwt-token, срок действия которого ограничен 12-тью часами. Поэтому каждый пользователь в среднем раз в день авторизуется. Если таких пользователей 2.5 млн, то в результате вычисления получим 28.9351851852~29 rps на запись. Чтение jwt-token'а будет происходить каждый раз при потыке просмотра контента, просмотра профиля, оставления комментария и других действий, требующих авторизации. Таким образом таких действий пользователь совершает около 5 за один день.  
## Физическая схема БД
### Выбор СУБД
* Для поиска фильмов по названию и описанию будет использоваться **Elasticsearch**.
* Для хранения таблиц Films, Genres, Actors, Films_Actors, Users будет использоваться **PostgreSQL**.
* Для выдаче данных о фильме или актере на соответствующих страницах будет использоваться **Tarantool**, который с некоторой переодичностью производит обновление кеша, нагружая postgreSQL.
* Для хранения таблиц Reviews использоваться будет Cassandra, так как ввиду особенности записи данных в Cassandra она является наиболее удобной для быстрого чтения комментариев пользователей.
* Для Avatars, Photos и видеоконтента использоваться будет **S3**.
* Для рекомендаций на основе рейтинга и кол-ва просмотров фильма, а также хранения сессионных данных будет использоваться **Redis**.
Redis используется для управления временными данными сессий. 
* Для статистики будет использоваться **ClickHouse**.
* Для мониторинга будет использоваться **Prometheus**.
Prometheus тесно интегрируется с Kubernetes, что делает оптимальным выбором для мониторинга контейнеризованных приложений. Он может автоматически обнаруживать сервисы и поды в кластере K8s.
* Для хранения конфигурации K8s будет использоваться **etcd**. Он может использоваться как центральное хранилище конфигурации для распределённых систем, где важно иметь единое, согласованное представление конфигурации.
* И **kafka** будет использоваться для первоначальной обработки данных.
Для первоначального анализа данных о просмотрах видео в фоновом режиме используется kafka, после чего результаты будут записаны в ClickHouse для долговременного хранения. Аналогично будут обработаны такие данные как начало и окончание просмотра видео, комментарии, приостановка видео, авторизация пользователей и другие действия. Эти события отправлены в Kafka, чтобы их можно было обрабатывать асинхронно, не влияя на производительность основного приложения. Также Kafka может служить связующим звеном между микросервисами внутри k8s, обеспечивая надежную и масштабируемую передачу сообщений. Это позволяет микросервисам взаимодействовать друг с другом асинхронно и без блокировок. Используя шины сообщений в обе стороны.

### Физическая схема СУБД

![image](https://github.com/user-attachments/assets/e13a7e45-ccc8-47fc-b4c8-84c3b5821946)

В поле genres Films записаны id соответсвующих жарнов
```
[
  124,
  233,
  ....
]
```


В поле films Actors записаны id соответсвующих Actor_films
```
[
  124,
  233,
  ....
]
```

В поле actors Films записаны id соответсвующих значений Actors_Films
```
[
  123,
  123,
  ....
]

```

В поле photo_urls Actors записано
```
[
  "url_1",
  "url_2",
  ....
]
```

В поле video_url Films (4k, 720p, 1080p, 360p)
```
[
  {"url": "https://example.com/film1.mp4", "quality": "4k"}
  ....
]
```
Остальные типы данных атрибутов всех сущностей являются примитивными типами данных. Такие как: Int, date, text.

Tarantool будет хранить результаты выполнения join Genrs, Actors_Films, Actors к Films, после чего кешировать все результаты ответов для всех запросов. Получаемые таблицы будут весить менее 10 Гб, что подойдет для храения данных в tarantool. Полная денормализация повысила бы сложность записи новых данных, поэтому было принято решение в postgreSQL хранить данные как на схеме для того, чтобы повысить эффективности записи новых значений в СУБД, а также в последствии передовать результаты сложных запросов в tarantool. Передача данных tarantool обосновано тем, что у нас для обычного юзера в приоритете именно чтение, а не запись. Так как любой человек заходя на страницу фильма получает данные об актерах, их ролях и фотографию, а также заходя на страницу актера получает все его фотографии и фильмы. Такое кеширование данных ощутимо снизит нагрузку на СУБД postgreSQL и позволит повысить эффективность всей системы.

### Шардирование и резервирование СУБД 

#### Реплицировать будем:
* **Postgres**:
PostgreSQL Streaming Replication: Позволяет настраивать репликацию данных между мастером и репликами. Для многодатацентровой архитектуры можно настроить реплики в каждом датацентре для обеспечения отказоустойчивости и локального чтения.
WAL (Write-Ahead Logging) для передачи изменений на реплику в реальном времени. Мастер - ДЦ Москвы.

* **Elasticsearch**:
Cross-Cluster Replication (CCR): Позволяет реплицировать данные между кластерами Elasticsearch. Реплики во всех ДЦ от ДЦ Мосвкы.

* **Tarantool**:
Replication Protocol: Tarantool поддерживает асинхронную репликацию между экземплярами, что позволяет синхронизировать данные. Создаем мастер и реплику на каждом ДЦ для обеспечения отказоустройчивости.

* **S3 хранилище**:
Будут использоваться мульти-региональные бакеты в AWS S3. Это позволит повысить отказоустойчивость системы и повысить скорость доступа. Cross-Region Replication (CRR) - автоматически реплецируем данные из бакетов Москвы в другие ДЦ. 

#### Шаридировать будем:

* **Redis**:

Используем Redis Cluster и создадим в каждом из ДЦ собственный узел, который будет обслуживать пользователей исходя из региона пользователя. В сервисе авторизации пользователю выдают jwt-token, после чего он сохраняется в сессию на локальом ДЦ.
```
SET session:12345 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCIsImV4cCI6MTYxNjI0MjYyMn0.eyJuYW1lIjoiTmlraXRpbiBBbGV4IiwiaXNfc3ViIjoxNTE2MjM5MDIyLCJ1c2VyX2lkIjo0NDUzNTU2MzU1MjU0NTV9.Mn4iaITlMH8BNZE8tw9TytJQz47z3FjFyux6RWfoL2E' EX 43200

{
  "alg": "HS256",
  "typ": "JWT",
  "exp": 1616242622
}
{
  "name": "Nikitin Alex",
  "is_sub": 1516239022,
  "user_id": 445355635525455
}
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

* **Cassandra**:

Automatic Sharding: Cassandra использует механизм распределения данных по узлам на основе хэширования ключей. Данные автоматически распределяются по кластеру. Ключ партиционирования в Cassandra — это film_id, чтобы централизованно хранить reviews и быстро их получать для фильмов. NetworkTopologyStrategy - для создания реплик на каждом из ДЦ. EACH_QUORUM: Запись подтверждается большинством узлов в каждом ДЦ. Это гарантирует, что данные будут синхронизированы во всех ДЦ при записи нового review. Это увеличит время запроса оставления нового комментария, однако позовлит иметь во всех ДЦ одинаково новые данные.

* **Clickhouse**:

Мы храним данные о просмотрах пользователей, статистику пауз и наиболее частых просмотров каких-то сцен фильмов в ДЦ Москвы.

```
user_views (
       user_id UUID,
       film_id UUID,
       scene_id UUID,
       timestamp DateTime,
       duration UInt32,
       PRIMARY KEY (user_id, timestamp)
)

CREATE TABLE pause_stats (
       film_id UUID,
       user_id UUID,
       pause_count UInt32,
       total_pause_duration UInt32,
       PRIMARY KEY (film_id, user_id)
   ) 

CREATE TABLE popular_scene (
      scene_id UUID
      film_id UUID
      start Time
      end Time
      view_count UInt32,
      PRIMARY KEY (scene_id)
)
```

Distributed Tables, которая маршрутизирует запросы к таблицам по шардам, обращаться к данным в которых можно также и напрямую.
Запрос на запись или чтение в шард может быть отправлен на любую его реплику (реплики для отказоустойчивости). Для данных user_views ключ партиционирования - user_id, для pause_stats - user_id, для popular_scene - film_id. 


### Клиентские библиотеки / интеграции

**Elasticsearch**: Go - olivere/elastic

**PostgreSQL + Citus**: Go - lib/pq (for PostgreSQL), jackc/pgx (for async applications)

**Tarantool**: Go - tarantool/go-tarantool

**Cassandra**: Go - gocql/gocql

**Minio**: Go - minio/minio-go

**Redis**: Go - go-redis/redismq

**ClickHouse**: Go - clickhouse/clickhouse-go

**Prometheus**: Go - prometheus/client_golang

**Kafka**: Go - confluentinc/confluent-kafka-go

**etcd**: Go - etcd-io/etcd/client/v3


### Балансировка запросов / мультиплексирование подключений

Odyssey будет мультиплексировать запросы в Cassandra для увеличения эффективности взаимодействия с Cassandra, уменьшая накладные расходы, связанные с несколькими соединениями, которые на большом количестве пользователей будут достаточно ощутимы. Odyssey поможет улучшить масштабируемость системы Cassandra, позволяя им обрабатывать большее количество одновременных запросов.
С помощью Postgres Driver Odyssey может мультиплексировать соединения с Postgres, используя стандартный протокол взаимодействия с базой данных. В случае, если в tarantool закешированных данных нет, пользователь направит запрос в Postgres напрямую, поэтому обязательно нужно использовать Odyssey в этом соединении. Мультиплексирование соединений между Tarantool и Postgres может улучшить производительность системы, уменьшив накладные расходы, связанные с несколькими соединениями. Odyssey может увеличить эффективность системы, позволяя ей обрабатывать большее количество одновременных запросов. А также мультиплексирование соединений между Tarantool и Postgres может помочь улучшить масштабируемость системы, позволяя ей обрабатывать более высокие нагрузки.

### Схема резервного копирования

Поскольку все остальные ДЦ по сути своей являются копией Московского, за исключением пары сервисов (комментирования и авторизации), то есть смысл хранить еженедельные backup'ы главного ДЦ, делая их на магнитной ленте и храня одну копию в самом ДЦ, а вторую в главном офисе компании. Backup'ы будут храниться от 1 до 1.5 лет.

# Источники 

[1] https://web.archive.org/web/20181201005421/https://www.alexa.com/siteinfo/kinopoisk.ru 

[2]  https://web.archive.org/web/20231129184042/https://radar.yandex.ru/yandex?month=2022-05

[3] https://www.rbc.ru/technology_and_media/16/11/2023/65548b529a7947815e93d67b

[4] https://www.buro247.ru/news/culture/14-dec-2023-kinopoisk-results-of-the-year.html

[5] https://www.kinopoisk.ru/votes/

[6] https://www.kinopoisk.ru/reviews/
