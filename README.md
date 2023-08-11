# Телеграм-бот на основе OpenAI GPT

## Описание

Бот разработан для общения в Telegram, используя возможности модели GPT-3.5 от OpenAI. Он способен отвечать на вопросы пользователей, сохранять контекст диалога для более качественного общения и взаимодействовать в групповых чатах.

## Установка и запуск

Установите необходимые библиотеки:

`pip install openai aiogram`

Клонируйте репозиторий и перейдите в директорию проекта:

```bash
git clone [ссылка_на_репозиторий]
cd [название_директории]
```

Укажите значения переменных окружения в вашей системе:

- `TELEGRAM_BOT_TOKEN`: токен вашего бота в Telegram.
- `OPENAI_API_KEY`: ваш ключ доступа к API OpenAI.
- `MODEL_NAME`: имя модели OpenAI, которую вы хотите использовать (по умолчанию gpt-3.5-turbo-16k).

Запустите бота:

`python [название_файла].py`

## Основные команды

- `/start` или `/help`: Выводит информацию о возможностях бота.
- `забудь`: Сбросить историю диалога с ботом.

## Особенности работы в группах

Бот способен взаимодействовать в групповых чатах. Чтобы обратиться к боту в группе, упомяните его, используя @username_bot или ответьте на его сообщение.

## База данных

Для сохранения контекста диалога бот использует SQLite. Сообщения пользователей и ответы бота сохраняются в базе данных, что позволяет модели отвечать, учитывая предыдущий контекст общения.

## Безопасность

Не забудьте хранить ваш TELEGRAM_BOT_TOKEN и OPENAI_API_KEY в безопасном месте и не разглашать их.
