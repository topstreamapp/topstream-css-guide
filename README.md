# Изменение и создание скинов для TopStream App

## Информация
Для оформления виджета чата используется CSS. Здесь описана структура и классы HTML кода виджета чата.

Информация по CSS: https://developer.mozilla.org/ru/docs/Learn/CSS/Introduction_to_CSS


## Общий шаблон
Страница виджета чата по большей части содержит следующий HTML код:

```html
<body>
    <div class="widget">
        <div class="effect"></div>
        <div class="message-count"></div>
        <div class="messages"></div>
    </div>
</body>
```

* `.widget` - главный контейнер чата;
* `.effect` - пустой элемент, можно использовать для эффектов падения снега, дождя, туманов и прочего;
* `.message-count` - элемент с количеством сообщений в чате;
* `.messages` - элемент со всеми сообщениями чата.

К виджету чата уже подключены [Normalize.css](https://necolas.github.io/normalize.css/) и [Animate.css](https://daneden.github.io/animate.css/). Таким образом, виджет будет корректно отображаться в различных браузерах, и уже имеет анимации.

## Шаблон сообщений

Внутрь блока с классом `messages` будут добавляться сообщения чата. Код каждого сообщения примерно выглядит так:

```html
<div class="message">
    <div class="line">
        <span class="timestamp">15:55:23</span>
        <span class="service twitch"></span>
        <span class="badges">
            <img src="./img/twitch.png" class="badge-icon service service-twitch">
            <img src="https://static-cdn.jtvnw.net/badges/v1/75a2e8ff-9820-425c-b2b2-c21bca30c258/2" class="badge-icon">
        </span>
        <span class="nickname" style="color: rgb(255, 0, 0);">topstream</span>
        <span class="text">
            <img class="emote emote-twitch" src="https://static-cdn.jtvnw.net/emoticons/v1/698369/1.0">
        </span>
    </div>
</div>
```

Каждое сообщение добавляется элементом с классом `.message` в элемент с классом `.messages`. Структуру сообщения можно разобрать посмотрев на HTML код выше. Название класса соотвествует контенту. Обратите внимание, что иконки сервисов так же добавляются в `.badges`, но дополнительно предусмотрен еще один блок c `.service`, однако контента он не имеет.

Откройте виджет чата в вашем браузере и попробуйте исследовать его с помощью встроенных инструментов разработчика, это даст представление о контенте сообщений.

## Режим блоков и лимит сообщений
В обычном режиме (по умолчанию) виджет чата хранит на странице 100 сообщений, однако, чат можно перевести в режим блоков.

Для перевода чата в режим блоков в любом месте вашего CSS кода скина нужно добавить строчку:
```css
/*blocks*/
```

В режиме блоков чат автоматически отслеживает все сообщения в виджете, и начинает процедуру удаления, если сообщение подошло к верхнему краю виджета слишком близко, либо сработал таймер исчезновения сообщения.

Без режима блоков режим исчезновения сообщений **не работает**!

Чат добавляет к удаляемому сообщению класс `.fade`, в вашем скине должен быть такой класс с анимацией (!), затем чат дожидается окончания анимации от класса `.fade` и удаляет сообщение из виджета. Если класса не будет, либо у него не прописана анимация с `duration`, либо `iteration-count` будет бесконечным, то чат не дождется анимации и никогда не удалит сообщение.

## Использование и тестирование пользовательского скина в программе
Поместите ваш скин с именем файла `custom.css` в папку с приложением, там где находится `TopStream.exe` и выберите пользовательский скин в настройках. Для обновления скина просто обновите виджет чата.
