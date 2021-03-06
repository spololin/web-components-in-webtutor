# WebTutor

Общая информация о WebTutor доступна на сайте WebSoft по [ссылке](http://websoft.ru/db/wb/root_id/webtutor/doc.html).

---

[Архитектура системы](http://www.websoft.ru/db/wb/root_id/webtutor_architecture/doc.html)

WebTutor работает на платформе [SP-XML](http://docs.datex.ru/article.htm?id=5620276905286592644).

**Серверная часть:** JavaScript, XQuery, XAML  
**Клиентская часть:** JQuery, Ext JS  
**База данных**: MS SQL, Oracle или файловая база из XML файлов  
**Управление сервером:** IIS, WebTutor Server, WebTutor Administrator, конфигурационные XML файлы

Это стандартный набор, который использован в WebTutor по умолчанию, но вовсе не обязательный для разработки, рассмотрим все по отдельности.

### Серверная часть

_JavaScript, XQuery, XAML_

**JavaScript**

Единственное, без чего обычно нельзя обойтись при разработке в WebTutor это серверный JavaScript.

У вас возможно сразу возник вопрос, что за серверный JavaScript, какая версия? ES6? это Node.js?

Помню наткнулся на форуме на один комментарий от Фирсова Андрея , который отлично дает ответ на вопросы по поводу серверной части:

_"здесь вам не тут". Товарищи, еще раз повторюсь - смотрите документацию. Это не браузерный JS, не обычный XQuery и не стандартный XML.  
Здесь все "самописное". В любой версии WT.  
И то, что это внешне похоже на то, что вы знаете, вовсе не означает, что оно это и есть..._

То есть, синтаксис будет напоминать стандартный JavaScript но это не он. В этом "JavaScript" и плюсы и минусы.

Плюсы в том, что в вашем распоряжении будет огромное количество готовых функций, которые заточены под задачи решаемые в WebTutor \(к примеру вот эти [функции](http://news.websoft.ru/view_doc.html?mode=doc_type&custom_web_template_id=6180275463021353212&doc_id=6181289497353023487) или [функции работы с массивами](http://docs.datex.ru/article.htm?id=5620203358492510991) и.т.п.\). С помощью этих функций удобно получать и обрабатывать массивы данных и выполнять различные операции не вникая, что там у них под капотом. А под капотом там очень много кода от написания которого вы избавляетесь.

Минусы в том, что будет отсутствие поддержки многих функций стандартного JavaScript + отсутствие возможности использовать модули и синтаксического сахара современных версий JavaScript. Придется постоянно натыкаться на отсутствие поддержки возможностей стандартного JavaScript и как-то решать проблемы с этими ограничениями.

Этот минус, и многие другие минусы WebTutor, решаются его плюсом, а именно его открытостью. То есть если WebTutor что-то не поддерживает и у вас в нем не получается что-то реализовать, всегда есть возможность запустить сторонний сервер и использовать его модули для взаимодействия с WebTutor. Я к примеру использую для этого Node.js и модули npm, можно на свое усмотрение использовать любой сервер и любой близкий вам язык\(PHP, Go, Python итп\) и его модули.

**XQuery**

Самописный XQuery\([список поддерживаемых функций](http://docs.datex.ru/article.htm?id=5620203358492510995)\). Нужен для получения данных из базы. Также позволяет осуществлять запросы в стандартном SQL формате.

**XAML**

Никогда его не использовал. Но как понимаю интерпретатор может различать код XAML и преобразовывать его в HTML+Ext JS. Никогда не использовал XAML в WebTutor и сейчас не вижу в нем необходимости.

### Клиентская часть

_JQuery, Ext JS_

На страницах WebTutor по умолчанию используется JQuery, Ext JS и очень много CSS.

Если вы умеете инкапсулировать свои модули от внешнего окружения \(к примеру используя веб-компоненты или iframe и.т.п.\), то вас не волнует, что там в WebTutor и у других разработчиков. Если не умеете, то научитесь это делать.

### База данных

_MS SQL, Oracle, база из XML файлов_

Про базу данных можете почитать [здесь](http://docs.datex.ru/article.htm?id=5665465792879477187).

Получить данные из базы можно с помощью серверного кода JavaScript и XQuery.

Записать данные в базу можно через серверный JavaScript.

### Управление сервером

_IIS, WebTutor Server, WebTutor Administrator, конфигурационные XML файлы_

**IIS**  - Хотя WebTutor может работать в режиме приложения и сервиса, используйте его только в режиме IIS. Только в режиме IIS, WebTutor может работать протоколу [HTTP/2](https://ru.wikipedia.org/wiki/HTTP/2).

**WebTutor Server** - нужен, чтобы подключить WebTutor к IIS и базе данных, после этого не используется.

**WeTutor Administrator** - админка WebTutor с удобным интерфейсом и огромным функционалом. Must Have во время разработки.

**Конфигурационные XML файлы** - существует много различных конфигурационных файлов, но возможно они вам никогда не понадобятся.

---

### Разрушаем мифы о WebTutor

Все ниже написанное лично мое "имхо".

Добавил данный подраздел, чтобы прояснить ситуацию разработчикам, у которых пока не было опыта работы с WebTutor и взаимодействия в корпоративном секторе, которые знакомы с WebTutor, только по слухам, среди которых встречаются и негативные.

На протяжении многих лет в сфере дистанционного обучения я частенько слышу, про сложности при работе с WebTutor. Некоторые разработчики даже не попробовав что-то сделать в системе, на основе этих слухов, страхов и хаоса в головах заказчика, отказываются что-то разрабатывать. Аналогичная ситуация происходит и при выборе компаниями LMS, на основе разговоров и услышанных "ужасов" идет выбор в пользу других систем \(у некоторых LMS это даже одно из главных конкурентных преимуществ, что-то вроде "выбирайте нас так как WebTutor очень сложный"\). Все эти слухи появились и продолжают появляться. Эти слухи формировались при определенных обстоятельствах, о которых я напишу ниже, таких при которых под раздачу попала бы любая система, а не только WebTutor.

Вот некоторые отрицательные слухи, которые можно услышать и которые мы рассмотрим:

* сложно понять как WebTutor работает
* сложно разрабатывать под WebTutor
* сложно найти разработчика для WebTutor

Когда я только начинал работать в сфере дистанционного обучения, мне сразу вбили в голову эти утверждения. После чего я и сам некоторое время придерживался подобной точки зрения. Но после взаимодействия с WebTutor, другими подобными системами, работы в корпоративном секторе и получения определенных навыков и опыта в веб-разработке, понял, что все не так как говорят и понял почему эти слухи зародились.

И так по порядку:

* **сложно понять как WebTutor работает**  
  Так сложилось, что обычно WebTutor внедряется с подачи HR подразделений и затем их же сотрудниками и поддерживается. Так сложилось, что в HR подразделениях обычно нет людей связанных с IT, а тем более веб-разработчиков, а тем более с реальным опытом разработки. В итоге с системой начинают взаимодействовать рядовые сотрудники HR, в большинстве случаев WebTutor становится их первой системой и первым опытом веб-разработки. По сути этим людям\(их обычно 2-3 человека\) приходится переучиваться на новую профессию. И они рады бы научиться программировать, понять как все устроено итп, но на этих людей падает столько задач, что в итоге, чтобы успевать, все приходится делать поверхностно. Для меня до сих пор загадка, кто вообще это придумал, что заниматься LMS системой, которая обучает и развивает тысячи сотрудников компании, должна кучка людей, которая в итоге ничего не успевает, но обычно так и выходит. На этих 2-3 сотрудников ложатся задачи 10-15 человек. Это "люди швейцарские ножи", которые делают все. Естественно при таких нагрузках у сотрудников по всем направлениям идет недоразвитие и результаты выполенных работ оставляют желать лучшего. В том числе в направлении "как подобные системы работают", "навыки программирования" итд итп. И это отсутствие понимания передается от одного поколения сотрудников к другим. Даже если системой изначально начинает заниматься человек более менее понимающий в веб-разработке, то после возложения на него обязанностей десяти человек, он ничего не успевает, происходит стагнация его навыков, так как веб не стоит на месте, а на развитие этих навыков не остается времени и в итоге сотрудник не поддерживает свои навыки на должном уровне и на протяжении многих лет продолжает делать свою работу на одном и том же низком уровне.  
  В реальности же WebTutor обычная система, коих много, ничего сверхъестественного и сложного в ней нет. Один нормальный разработчик без проблем может объяснить другому разработчику что и как. То есть проблема не в системе WebTutor и ее сложности, а проблема в том, что у людей не хватает опыта и знаний. А необходимые опыт и знания они получить не могут, так как они перегружены. Нанять человека с опытом и знаниями не могут, так как не могут определить у кого они есть, так как у самих нет ни того ни другого. Также частенько встречаются случаи полного безразличия сотрудников к своей деятельности и системой иногда занимаются совершенно незаинтересованные люди.

* **сложно разрабатывать под WebTutor**  
  Cложность разработки кроется в пункте выше. Сложность начиналась, когда сотрудники HR без опыта веб-разработки становились у руля WebTutor и начинали пробовать программировать. Опыта у них не было и они естественно пытались повторить то, что видели в коде WebTutor. Но то, что было написано в WebTutor и такой подход в разработке, это следствие развития системы на протяжении многих лет, адаптации под окружение, там многое заточено под свои нужды, так удобно разработчикам WebSoft, удобно поддерживать систему, обновлять итп. Действительно в этом тяжело разобраться, подобный вид разработки не подойдет для новичков. Но фишка в том, что никто ведь этого и не просит. Никто же не заставляет разрабатывать и использовать инструментарий WebSoft \(XML, XAML, ExtJS и все остальное\). Система полностью открыта, никаких ограничений, делайте все, что хотите. Единственное без чего действительно нельзя обойтись это серверный JavaScript WebTutor, все остальное необязательно использовать при разработке. Так сложилось, что люди без опыта веб-разработки выбирали самые сложные и запутанные пути разработки, и с учетом, что раньше было мало документации по разработке в WebTutor, люди столкнулись с непониманием и наступили на всевозможные грабли, на которые не должны были наступать.

* **сложно найти разработчика для WebTutor                    
  **Постоянно натыкаюсь на требования работодателей к кандидату на должность ~"Разработчик WebTutor". И каждый раз делаю facepalm. Суть в том, что не надо искать разработчиков именно для WebTutor, нужно искать просто full stack веб-разработчика с достаточным опытом, нормальному разработчику без разницы для какой системы разрабатывать, для него после нескольких консультаций  не составит труда разрабатывать и под WebTutor или под любую другую систему.

На мой взгляд реальность такая:

* WebTutor обычная система ничего сложного и сверхъестественного в ней нет
* как и в любой системе в ней есть свои особенности, но кроме использования серверного JavaScript \(для которого есть документация\), никто вас не заставляет вникать и использовать, инструменты и подходы в разработке компании WebSoft.
* любой среднестатистический full stack веб-разработчик без проблем разберется с WebTutor \(правда его должен проконсультировать такой же разработчик, который имел опыт работы с WebTutor\)

#### Итого

Большинство отрицательных слухов на мой взгляд появляются из-за недостатка знаний и опыта в веб-разработке со стороны сотрудников занимающихся разработкой и поддержкой WebTutor внутри компании. Этим людям просто не оставляют времени и возможностей, чтобы получить необходимые знания и опыт в веб-разработке, так как вешают на них все подряд. В итоге люди устают ничего не успевают, ищут причину. И под раздачу попадает WebTutor :D

Хотя на самом деле все просто и причина =&gt; отсутствие в штате достаточного количества соответствующих квалифицированных специалистов.

