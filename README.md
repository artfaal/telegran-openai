# WisdomWave. Generated by AI for AI. Телеграм-бот на основе OpenAI GPT

## Описание

Бот разработан для общения в Telegram, используя возможности модели GPT-3.5 от OpenAI. Он способен отвечать на вопросы пользователей, сохранять контекст диалога для более качественного общения и взаимодействовать в групповых чатах.

## Установка и запуск

Установите необходимые библиотеки:

`pip install openai aiogram`

Клонируйте репозиторий и перейдите в директорию проекта:

```bash
git clone https://github.com/artfaal/telegram-openai.git
cd telegram-openai
```

Укажите значения переменных окружения в вашей системе:

- `TELEGRAM_BOT_TOKEN`: токен вашего бота в Telegram.
- `OPENAI_API_KEY`: ваш ключ доступа к API OpenAI.
- `MODEL_NAME`: имя модели OpenAI, которую вы хотите использовать (по умолчанию gpt-3.5-turbo-16k).
- `MAX_TOKENS`: определяет максимальное количество токенов, которое модель может обрабатывать при одном запросе. Эта переменная важна для ограничения длины сообщений и для оптимизации стоимости API. Кроме того, MAX_TOKENS играет ключевую роль в поддержании контекста диалога, так как при ограничении количества токенов история диалога может быть обрезана, что в свою очередь может привести к потере контекста.
- `OPENAI_ORGANIZATION`: (необязательно) ID вашей организации в OpenAI. Если у вас есть организационный аккаунт на OpenAI и вы хотите использовать его, укажите здесь его ID. Если оставить пустым, будет использоваться ваш индивидуальный аккаунт.

Запустите бота:

`python main.py`

## Основные команды

- `/start` или `/help`: Выводит информацию о возможностях бота.
- `забудь`: Сбросить историю диалога с ботом.

## Особенности работы в группах

Бот способен взаимодействовать в групповых чатах. Чтобы обратиться к боту в группе, упомяните его, используя @username_bot или ответьте на его сообщение.

## База данных

Для сохранения контекста диалога бот использует SQLite. Сообщения пользователей и ответы бота сохраняются в базе данных, что позволяет модели отвечать, учитывая предыдущий контекст общения.

## Безопасность

Не забудьте хранить ваш TELEGRAM_BOT_TOKEN и OPENAI_API_KEY в безопасном месте и не разглашать их.

## TODO

- [ ] Разбивка сообщения для обработки telegram (как отправки, так и получения)
- [ ] Обработка markdown (?)
- [ ] Когда в групповой чат боту отправляешь- "забудь" без @ все боты в чате забывают историю
- [ ] Прикрутить мониторинг и хранение логов
- [ ] Прикрутить дешборды графаны, чтобы видеть текущее состояние ботов
- [ ] Рефакторинг и разбивка по отдельным файлам
- [x] Нормальное имя для проекта
- [x] Способы оркестрации несколькими ботами
- [x] Отдельные боты для работы с ГПТ
- [x] Автоматическое обновление ботов при пуше в ветку (+ уведомление о том, что бот перезапущен)
- [x] `Tokens used: 6954 (178.31% of 3900)` (не выполняется механизм удаления). Предварительно проверить пороговые значения

## Предложения от openai для доработки

### Первая версия улучшений

Обработка ошибок:

Хорошо было бы обрабатывать ошибки при запросах к OpenAI, например, когда превышен лимит токенов или нет соединения с интернетом.
Также, возможные ошибки при работе с базой данных следует обрабатывать.

Асинхронная работа с SQLite:

SQLite в вашем коде работает синхронно, что может вызвать замедления при большом числе запросов. Рассмотрите возможность использования aiosqlite для асинхронной работы с базой данных.

Повторное использование кода:

Можно создать отдельную функцию для добавления сообщений в базу данных и использовать ее вместо повторяющихся строк кода.
Аналогично можно поступить с логированием и отправкой сообщений.

Безопасность:

Ваш токен от Telegram и ключ API от OpenAI должны храниться в безопасном месте. Рассмотрите возможность использования, например, python-decouple для безопасного хранения секретов.

Настройка логирования:

Вместо простой настройки логирования можно создать файл конфигурации для более детальной настройки логирования.

Кэширование:

Если ваш бот станет популярным и будет получать много однотипных запросов, можно рассмотреть вариант кэширования ответов на часто задаваемые вопросы для уменьшения времени ожидания и экономии токенов.

Масштабирование:

Если у вас будут проблемы с производительностью из-за большого количества пользователей, подумайте о масштабировании вашего решения, возможно, с использованием других баз данных или развертыванием на мощных серверах.

Расширение функционала:

Можно добавить команды для управления настройками бота, например, выбор языка общения или тематики диалога.

Тестирование:

Подумайте о написании тестов для вашего бота. Это может помочь выявить потенциальные проблемы в будущем.

### Вторая версия улучшений

Версия 1.1 вполне функциональна, но есть несколько рекомендаций по улучшению:

1. **Оптимизация запросов к базе данных**: Вместо того чтобы отправлять запросы к базе данных при каждом сообщении, можно использовать кэширование и выполнять обновления базы данных пакетно. Но при этом необходимо учесть, что это может влиять на актуальность данных.

2. **Управление конфигурацией**: Вместо использования переменных окружения напрямую, можно использовать конфигурационный файл или инструменты, такие как `python-decouple`, чтобы делать код более читаемым и удобным для управления.

3. **Обработка ошибок**: Можно добавить дополнительные обработчики ошибок для разных типов ошибок, которые могут возникнуть во время работы с базой данных или с OpenAI.

4. **Оптимизация управления токенами**: Текущая система удаления сообщений может быть не совсем оптимальной. Вместо удаления фиксированного числа сообщений при достижении определенных порогов можно рассмотреть другие способы, такие как удаление сообщений до достижения безопасного уровня токенов.

5. **Повышение безопасности**: Если это веб-бот, можно добавить механизмы безопасности, такие как проверка подписи запроса от Telegram, чтобы убедиться, что запросы действительно исходят от Telegram.

6. **Логирование**: Можно использовать более продвинутые инструменты для логирования, такие как `loguru`, чтобы получить более детальное и структурированное логирование.

7. **Переход на асинхронную базу данных**: Вместо использования синхронной базы данных SQLite можно рассмотреть использование асинхронной базы данных (например, `aiosqlite`) для повышения производительности.

8. **Рефакторинг**: Рассмотрите возможность разделения кода на модули или пакеты для лучшей организации и читаемости.

9. **Дополнительные функции**: Можно добавить функции, такие как возможность пользователю настраивать, как часто ему будут отправляться предупреждения о количестве токенов или дать возможность администраторам групп управлять настройками бота.

10. **Тестирование**: Подумайте о добавлении юнит-тестов и интеграционных тестов для проверки корректности работы кода.

Эти рекомендации могут быть применены в зависимости от ваших потребностей и того, насколько вы планируете масштабировать и развивать своего бота в будущем.
