For the english version, click [here](https://github.com/kameton-dev/MEmarket-Basic/blob/main/README-en.md).

# Создание своего собственного репозитория для MEmarket
ляляля я семён лобанов. это гайд как создать собственный репозиторий для великого MEmarket. если вы планируете хостить свой репо через гитхаб, можете сделать форк

## Список актуальных репозиторий:
```MEmarket basic - http://millenniummarket.ru/properties.json```

```Win10Markt - http://markt.hotsamsa.top/properties.json```

```LegacyProjects WP8 - https://dvltvv.github.io/legacyprojects-wp8/properties.json```

## Хостинг
Можете хостить репозиторий хоть на своем сервере, хоть в гитхабе, особого значения не имеет. Разве что:
>[!NOTE]
>Рекомендуется размещать свой сервер по протоколу http://. Но с https оно тоже норм работает

## 📂 Структура репозитория
Вообще, структура для прилодения тут не строгая. То есть, вы можете создавать папки любых наименований. Но в пример я буду писать свою придуманную структуру:
```text
example-repo/
├── apps/
│     ├── app.example/
│     │    ├── app1.xap (или .appx)
│     │    ├── app2.xap (или .appx)
│     │    └── app-icon.png
│     └── game.example/
│          ├── game1.xap (или .appx)
│          ├── game-icon.png
│          ├── screen1.png
│          └── screen2.png
└── properties.json        <-- Главный индексный файл
```
> [!TIP]
> 1. Советую именовать папки с файлами приложений также, как их id. Так будет лучше ориентироваться
>
> 2. Загружайте иконки для приложений в адекватном качестве! Не 8к, но и не шакальное, чтобы бедные люмии переварили картинки
>

## ⚙️ Структура properties.json
Самая важная часть репозитория. Вот тут уже все намного строже:
```json
{
  "repo_name": "Example Repo",
  "creator": "Repo Developer's Nickname",
  "last_updated": "2026-04-15",
  "apps": [
    {
      "id": "app.example",
      "base_url": "http://domain.com/apps/app.example/",
      "title": "App Name",
      "screenshots": [],
      "author": "Dev Name",
      "description": "App Description",
      "icon_url": "app1-icon.png",
      "size": "0,1 MB",
      "category": "tools",
      "versions": [
        {
            "version": "0.5",
            "download_url": "http://domain.com/apps/app.example/app1.xap"
        },
        {
            "version": "1.0",
            "download_url": "http://domain.com/apps/app.example/app2.xap"
        }
      ]
    },
    {
      "id": "com.example.game",
      "base_url": "http://domain.com/apps/game.example/",
      "title": "Game Name",
      "screenshots": ["screen1.png", "screen2.png"],
      "author": "Вася пупкин"
      "description": "ляляля",
      "icon_url": "game1-icon.png",
      "size": "1488 MB",
      "category": "game",
      "version": "0.9b",
      "download_url": "https://domain.com/files/game1.xap"
    }
  ]
}

```
### Описание полей:
| Поле | Описание |
|---|---|
| repo_name | Название вашего магазина, которое увидит пользователь в настройках репозиторий |
| id | Идентефикатор приложения. Должен быть индивидуален, без 1 2 3 4 5 |
| apps | Список объектов с данными о приложениях |
| base_url | путь к папке приложения для лого и скриншотов |
| download_url | **Прямая** ссылка на файл. Нужна для получения и скачивания файла |
| size | Вес файла (для информирования пользователя. если что можете приколы там делать, я мока разрешаю) |
| versions | Если вы хотите загрузить разные версии одного приложения, используйте это поле |
| version | Если у приложения одна версия / поле для versions |

### Список актуальных сортируемых категорий:
| "category": "..." | Название |
|---|---|
| "games" | Игры |
| "entertaintment" | Развлечения |
| "music+video" | Музыка + Видео |
| "tools" | Инструменты |
| "livestyle" | Лайвстайл |
| "news+weather" | Новости + погода |
| "social" | Социальные |
| "education" | Обучение |


>[!NOTE]
>В колонке "category" вы можете писать абсолютно любые слова. Все прилодения с **нестандартными** категориями будут отправлять в одну общую - "Прочее".
