# Telegram Message Notify Actions (TNA)

Это действие отправляет тестовое сообщение в Telegram с использованием заданных параметров.

## Использование

Добавьте следующий шаг в ваш workflow файл:

```yaml
name: Send Telegram Message
on: [push]

jobs:
  send-telegram-message:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Отправка тестового сообщения в Telegram
        uses: digital-life-71/tna@main
        with:
          TELEGRAM_TOKEN: ${{ secrets.TELEGRAM_TOKEN }}
          TELEGRAM_CHAT_ID: ${{ secrets.TELEGRAM_TO }}
          TELEGRAM_MESSAGE: |
            📝 Commit: ${{ github.event.head_commit.message }}
            ⚠️ Branch: ${{ github.ref_name }}
            👤 Author: ${{ github.actor }}
            📅 Date: ${{ github.event.head_commit.timestamp }}
            📂 Repository: ${{ github.repository }}
            🔗 Commit URL: ${{ github.event.head_commit.url }}
            🆔 Commit ID: ${{ github.sha }}
            🏷️ Repository Owner: ${{ github.repository_owner }}
            📛 Repository Name: ${{ github.event.repository.name }}
          BUTTON_TEXT: 'Посмотреть'
          BUTTON_URL: 'https://github.com/${{ github.repository }}/commit/${{ github.sha }}'
          DISABLE_NOTIFICATION: 'true'
```

## Параметры

- `TELEGRAM_TOKEN`: Токен Telegram (обязательно)
- `TELEGRAM_CHAT_ID`: ID чата Telegram (обязательно)
- `TELEGRAM_MESSAGE`: Сообщение для отправки (обязательно)
- `BUTTON_TEXT`: Текст кнопки (по умолчанию: 'Посмотреть')
- `BUTTON_URL`: URL кнопки (по умолчанию: 'https://github.com/${{ github.repository }}/commit/${{ github.sha }}')
- `DISABLE_NOTIFICATION`: Отключить уведомления (по умолчанию: 'true')
- `COMMIT`: Коммит (опционально)
- `BRANCH`: Ветка (опционально)
- `AUTHOR`: Автор (опционально)
- `DATE`: Дата коммита (опционально)
- `REPOSITORY`: Репозиторий (опционально)
- `COMMIT_URL`: URL коммита (опционально)
- `COMMIT_ID`: ID коммита (опционально)
- `REPOSITORY_OWNER`: Владелец репозитория (опционально)
- `REPOSITORY_NAME`: Имя репозитория (опционально)