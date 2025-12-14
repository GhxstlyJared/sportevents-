# SportEvents Manager - GitHub Pages

Эта папка содержит веб-страницы для кликабельных ссылок на мероприятия и учебные заведения.

## Структура

- `index.html` - Главная страница приложения
- `e/index.html` - Редирект для мероприятий (events)
- `i/index.html` - Редирект для учебных заведений (institutions)

## Как работает

1. Пользователь кликает по ссылке типа `https://username.github.io/sportevents/e/?id=event-id`
2. Открывается веб-страница с редиректом
3. Страница автоматически пытается открыть deep link `sportevents://events/event-id`
4. Если приложение установлено → оно открывается
5. Если нет → показывается инструкция и ID для копирования

## Развертывание на GitHub Pages

1. Создайте новый репозиторий на GitHub (например, `sportevents`)
2. Загрузите эту папку `docs` в корень репозитория
3. Перейдите в Settings → Pages
4. В разделе "Source" выберите "Deploy from a branch"
5. Выберите ветку `main` и папку `/docs`
6. Нажмите "Save"
7. Через несколько минут сайт будет доступен по адресу `https://username.github.io/sportevents/`

## Обновление ссылок в приложении

После развертывания обновите базовый URL в файлах:
- `lib/core/utils/event_link_utils.dart`
- `lib/core/utils/institution_link_utils.dart`

Замените:
```dart
final base = baseUrl ?? 'https://yourusername.github.io/sportevents';
```

На ваш реальный GitHub Pages URL.

## Формат ссылок

- Мероприятия: `https://username.github.io/sportevents/e/?id=EVENT_ID`
- Учебные заведения: `https://username.github.io/sportevents/i/?id=INSTITUTION_ID`

Эти ссылки будут кликабельными в любых мессенджерах!

