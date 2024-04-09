Включите инструкции по настройке для руководства менторов по процессу инициализации приложения:

1. Скачайте приложение и запустите его через терминал
2. Если не видны нвоости то запустите webscraper.py чтобы он заново взял информацию  с сайте
3. Если даже так не видно то попробуйте сначала запустить server.py, потом webscraper.py и в конце сделайте npm start


Опишите процесс проектирования и разработки, выделив любые уникальные подходы или методологии, использованные в работе:

1. В этом проекте мне больше всего принес пользу MUI который мы прошли на курсах
2. Так же я использовал новые компоненты которые не были рассмотрены, например <Paper/>, <Header/>
3. Было очень интересно тяжело и интересно внедрять бэкэнд


Обсудите любые компромиссы, принятые во время разработки, и очертите известные ошибки или проблемы в приложении:
Все начало усложняться с внедрения веб-скрапинга на что я потратил 2 дня только изучая эту тему с нуля,
после чего это принесло новую волну сложностей:

1. На главной странице tengrinews не оказалось нужного количества статей (15) из за чего мне пришлось скрапить с отдела новостей
2. Каждая отедльная новость внутри отдела новостей имела одну категорию (Новости) из за чего их было не возможно отсортировать по категориям
Новости в главной странице имели категории но в добавок к первой проблеме, они были отличны от названий нижних кнопок отвечающих за категорий (Например вместо :Новости США: там было просто :США:)
Это означало что мне пришлось бы просматривать каждую категорию заново, чего мне не хватило времени
Тем не менее я оставил логику сортировки по категориям которая работала с статичными данными из массива где я задовал категории вручную 
3. Изначально я создал свой собственный компонент Article.js который открывался через Router,
Однако, я не смог ответить на вопрос "Как перейти в компонет Article.js одновременно передавая туда данные с нажатой карточки"
Поэтому я просто замеил ссылку на Route, настоящей ссылкой на статью которая была динамический взята с бэкэнда и передана как пропс
Тем не менее, я оставил свой Article.js чтобы вы могли открыть ее в браузере и оценить то как я хотел чтобы каждая статья выглядела
4. Последняя проблема заключалась в том что я смог сделать так чтобы веб-скрепинг делал запрос каждую минуту чтобы предоставлять свежие данные,
Однако при моем подходе JSON файл не обновлялся а лишь дополнялся, что привело к огромному количеству страниц с почти одинаковым новостями
Из за чего я убрал эту логику
5. Так же, в отделе новостей очень много данных, из за чего очень большое количество из них записаны как "Сегодня" или "Вчера"
Из за чего того количества новостей которыми я ограничелся не хватает чтобы увидеть работает ли сортировка по дате
Однако я так же оставил код которые успешно справлялся с этим работая с статичными данными


Если вы захотите удостовериться в работе некоторых функций, то вот массив с которым я рботал и затем удалил,
Спасибо большое за внимание!

const newsItems = [
    { 
        category: 'События',
        image: require('../images/photo_11758.jpeg.webp'),
        title: "In the footsteps of great Central Asian explorer",
        date: new Date("2014-09-02T18:12:00"),
        watches: "3001",
        comments: "1"
    },
    { 
        category: 'События',
        image: require('../images/photo_11125.jpg.webp'),
        title: "Consequences of mud flood near Almaty",
        date: new Date("2014-05-20T08:16:00"),
        watches: "3018",
        comments: "0"
    },
    { 
        category: 'События',
        image: require('../images/photo_10642.jpg.webp'),
        title: "My Kazakhstan photo exhibition",
        date: new Date("2014-05-30T14:00:00"),
        watches: "2426",
        comments: "0"
    },
    { 
        category: 'События',
        image: require('../images/photo_10212.jpg.webp'),
        title: "Kazakh village life",
        date: new Date("2014-05-20T14:42:00"),
        watches: "2832",
        comments: "1"
    },
    { 
        category: 'События',
        image: require('../images/photo_10498.jpg.webp'),
        title: "Geneva Motor Show 2014",
        date: new Date("2014-03-22T16:13:00"),
        watches: "2151",
        comments: "0"
    },
    { 
        category: 'Преступность',
        image: require('../images/3.jpeg'),
        title: "Прокурор - Бишимбаеву: Она умирала 6-8 часов, а вы позвонили гадалке",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },{ 
        category: 'Преступность',
        image: require('../images/photo_467720.jpeg'),
        title: "Суд над Бишимбаевым: трансляция 4 апреля",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'События',
        image: require('../images/2.jpeg'),
        title: "Аким Конаева ушел в отставку",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'Преступность',
        image: require('../images/3.jpeg'),
        title: "Прокурор - Бишимбаеву: Она умирала 6-8 часов, а вы позвонили гадалке",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },{ 
        category: 'Преступность',
        image: require('../images/photo_467720.jpeg'),
        title: "Суд над Бишимбаевым: трансляция 4 апреля",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'События',
        image: require('../images/2.jpeg'),
        title: "Аким Конаева ушел в отставку",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'Преступность',
        image: require('../images/3.jpeg'),
        title: "Прокурор - Бишимбаеву: Она умирала 6-8 часов, а вы позвонили гадалке",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },{ 
        category: 'Преступность',
        image: require('../images/photo_467720.jpeg'),
        title: "Суд над Бишимбаевым: трансляция 4 апреля",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'События',
        image: require('../images/2.jpeg'),
        title: "Аким Конаева ушел в отставку",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
    { 
        category: 'Преступность',
        image: require('../images/3.jpeg'),
        title: "Прокурор - Бишимбаеву: Она умирала 6-8 часов, а вы позвонили гадалке",
        date: "Сегодня в 09:51",
        watches: "83152",
        comments: "24"
    },
  ];
