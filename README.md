# Bot moderator for vk / Бот модератор для вк

### Created using the libraries' / Создано с использованием библиотек: [php-getting-started](https://github.com/heroku/php-getting-started), [vk-php-sdk](https://github.com/VKCOM/vk-php-sdk)

## Connection / Подключение

**Install [Git](https://git-scm.com/downloads), [Heroku ToolBelt](https://devcenter.heroku.com/articles/heroku-cli), and [Composer](https://getcomposer.org/)**

### For Heroku / Для Heroku
Сopy repository to server folder / Скопируйте репозиторий в папку сервера

`git clone https://github.com/kos234/Vk-bot-moderator.git` <br>
`cd vk-bot-moderator` <br>
`heroku login` <br>
`heroku create <Your project name>` <br>
`git push heroku master` <br>
`heroku addons:create cleardb:ignite` <br>

Now you need to create configs / Теперь вам нужно создать конфиги

`heroku config:set CONFIRMATION_TOKEN_VK_BOT=` String that the server should return (Group)/ Строка, которую должен вернуть сервер (Сообщество)<br>
`heroku config:set TOKEN_VK_BOT=` Access key (Group)/ Ключ доступа (Сообщество)<br>
`heroku config:set SECRET_KEY_VK_BOT=` Secret key (Group)/ Секретный ключ (Сообщество)<br>
`heroku config:set USER_TOKEN=` Access token (User)/ Токен (Пользователь) - **Required for methods of displaying information about a user, unless you want to specify your token, you can specify group token (TOKEN_VK_BOT) / Необходим для методов вывода информации о пользователе, если не хотите указывать свой токен, можете указать токен группы (TOKEN_VK_BOT)**<br>
`heroku config:set SERVICE_KEY=` Service access key (App)/ Сервисный ключ доступа (Приложение)<br>

### For another hosting service / Для другого хостинга
 
Create a Composer project in server folder / В папке сервера создайте проект Composer

`composer init`

Installing VK SDK / Устанавливаем VK SDK

`composer require vkcom/vk-php-sdk`

Copying the file `index.php` go to the server folder and change `require('../vendor/autoload.php');` on `require('vendor/autoload.php');`. In `index.php` instead of `getenv`, specify the values directly. Values are described in the settings for **Heroku**

Копируем файл `index.php` в папку сервера и меняем `require('../vendor/autoload.php');` на `require('vendor/autoload.php');`. В `index.php` вместо `getenv` укажите значения напрямую, описание значений есть в установки для **Heroku**

### Without hosting / Без хостинга

Invite the bot to a VK conversation / Пригласите бота в беседу вк https://vk.com/app6441755_-195541692?ref=group_menu

## List of commands / Список команд

✏**Команды:**<br>
📄`/` — информация о боте и команды<br>
👤`/User info|Информация пользователя {@Айди|@домен|Пересланое сообщение}` — информация пользователя в вк и чате<br>
🔗`/Сократить ссылку {ссылка} [Включить|выключить|on|off]` — сокращает ссылку через сервис вк, on - включает статистику<br>
📄`/Получить статистику {ссылка} {токен}` — выводит статистику переходов по сокращенный ссылке (желательно использовать эту команду в личных сообщениях)<br>
🔗`/Инвайт ссылка|Приглашение|Ссылка приглашение` - выводит ссылку на приглашение в этот чат<br>
👋`/Пригласить {@Айди|@домен|Пересланое сообщение} [Сообщение]` - отправляет приглашение пользователю в этот чат<br>
📃`/Список {Пользователей|забаненных|вышедших|модераторов|неактивных|онлайна}` - выводит указанный список пользователей<br>
📝`/Chat settings|настройки беседы|чата` - показывает текущий список настроек<br>
👿`/History punishment|/История наказаний [число]` - показывает историю последних наказаний, по умолчанию 100<br>
👼`/Лимит модераторов` - выводит лимит для модераторов<br>

👥**Модерация и Администрация:**<br>
👮`/Предупреждение|Пред|Pred {@Айди|@домен|Пересланое сообщение} [Количество] [Причина]` - Выдать предупреждение, по умолчанию 1 предупреждение<br>
☀`/Удалить предупреждение|пред {@Айди|@домен|Пересланое сообщение} [Количество] [Причина]` - Удалить предупреждения, по умолчанию всё предупреждения<br>
😢`/Кик|Исключить|Kick {@Айди|@домен|Пересланое сообщение} [Причина]` - Исключить пользователя из чата<br>
👿`/Временно забанить|temp ban {@Айди|@домен|Пересланое сообщение} {Время SS:MM:HH:DDD:MM:YY} [Причина]` - Временно забанить пользователя в беседе<br>
💀`/Бан|Ban {@Айди|@домен|Пересланое сообщение} [Причина]` - Забанить пользователя<br>
👼`/Разбанить|Пардон|Unban {@Айди|@домен|Пересланое сообщение} [Причина]` - Разбанить пользователя<br>
👪`/Мега кик|мега исключение {Неактивных|вышедших|пользователей}` - исключает пользователей из определённой группы<br>
👸`/Назначит ранг|Сет ранг {@Айди|@домен|Пересланое сообщение} {0|1|2|3|4|5|Модератор1 - Модератор4|пользователь|администратор}` - Выдать ранг пользователю<br>

⚙**Настройки:**<br>
🐣`/Лимит повышения рангов {Уровень: 1 - 3} {Количество предупреждений] {Количество киков] {Количество временных баннов]` - Устанавливает лимит повышение рангов модераторам, если указан только уровень, лимит для него сбрасывается<br>
🔫`/Наказание за предупреждения {От какого количества} {Тип: кик, временный бан, бан} {Время SS:MM:HH:DDD:MM:YY, если тип: временный бан]` - Установить наказание за достижение определенного количества предупреждений<br>
🍁`/Очистить таблицу {пользователей|забаненных|вышедших|модераторов|наказаний|лимита|настроек|всё}` - очищает указанную таблицу<br>
⏲`/Авто очистка предупреждений {Время SS:MM:HH:DDD:MM:YY}` - сбрасывает всё предупреждения через указанное время<br>
✋`/Приветствие {Текст}` - Устанавливает приветствие для новых пользователей, можете написать в сообщение {first_name} - чтобы указать имя, {last_name} - чтобы указать фамилию. Если текст был не указан, приветствие будет отключено<br>
🔗`/Установить инвайт ссылку {Ссылка}` - Устанавливает ссылку для подключение к беседе<br>
👮`/Сообщать о наказаниях {@Айди|@домен|Пересланое сообщение}` - люди, которым приходят уведомления о выдачи наказаний(если людей несколько, указывать через запятую, либо через пробел)<br>
😲`/Автокик|автоисключение {Вышедших|ботов} {Включить|выключить|on|off}` - Автоисключение вышедших пользователей или новых ботов<br>
`{}` - обязательный параметр, `[]` - необязательный параметр, `{]` - тип зависит от задачи<br>

📖**Информация о проекте:**<br>
👤Создатель: https://vk.com/i_love_python <br>
👀Исходные код проекта и гайд по подключению: https://github.com/kos234/Vk-bot-moderator