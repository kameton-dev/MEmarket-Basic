For the english version, click [here](https://github.com/kameton-dev/MEmarket-Basic/blob/main/README-en.md).

# Создание своего собственного репозитория для MEmarket
ляляля я семён лобанов. это гайд как создать собственный репозиторий для великого MEmarket. если вы планируете хостить свой репо через гитхаб, можете сделать форк

## Список актуальных репозиторий:
```MEmarket basic - http://millenniummarket.ru/properties.json```

```Win10Markt - http://markt.hotsamsa.top/properties.json```

```LegacyProjects WP8 - https://dvltvv.github.io/legacyprojects-wp8/properties.json```

```ReOpen Market - https://raw.githubusercontent.com/OpenGlebsur/WP8-MEMarketRepo/refs/heads/main/properties.json ```

## Хостинг
Можете хостить репозиторий хоть на своем сервере, хоть в гитхабе, особого значения не имеет. Разве что:
>[!NOTE]
>Рекомендуется размещать свой сервер по протоколу http:// для лучшей работы с клиентом под WP8.1. Но с https оно тоже норм работает

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
│          ├── game1.appx
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
  "supported_os": ["WP8.1", "W10M"],
  "apps": [
    {
      "id": "app.example",
      "base_url": "http://domain.com/apps/app.example/",
      "os": "WP8.1",
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
      "os": "W10M",
      "title": "Game Name",
      "screenshots": ["screen1.png", "screen2.png"],
      "author": "Вася пупкин"
      "description": "ляляля",
      "icon_url": "game1-icon.png",
      "size": "1488 MB",
      "category": "game",
      "version": "0.9b",
      "download_url": "https://domain.com/files/game1.appx"
    }
  ]
}

```
### Описание полей репозитория:
| Поле | Описание |
|---|---|
| repo_name | Название вашего магазина, которое увидит пользователь в настройках репозиторий |
| creator | Ваш никнейм как создателя репозитория |
| last_updated | Дата последнего апдейта репозитория |
| supported_os | Поддерживаемые ОС репозитория: **В клиентах пока показываются только WP8.1 и W10M** |
| apps | Список объектов с данными о приложениях |

### Описание массива "apps":
| Поле | Описание |
|---|---|
| id | Уникальный идентификатор приложения |
| base_url | Базовый путь к папке с данными о приложении. Там должны храниться иконка, файл и скриншоты |
| os | ОС приложения: W10M или WP8.1 |
| title | Название приложения |
| screenshots | Перечисление по порядку названий скриншотов из папки base_url к приложению. Если их нет, можете отсавить поле пустым: [ ] |
| author | Создатель данного приложения |
| description | Описание приложения |
| icon_url | Название иконки приложения в папке base_url |
| size | Вес файла (для информирования пользователя. если что можете приколы там делать, я пока разрешаю) |
| category | Подходящее название категории для приложения / категория из списка ниже |
| version | Версия приложения |
| download_url | **Прямая** ссылка на файл. Нужна для получения и скачивания файла |

>[!TIP]
>Если вы хотите загрузить несколько версий одного приложения, используйте поле "versions".

### Описание "versions"
| Поле | Описание |
|---|---|
| version | Название данной версии приложения |
| download_url | **Прямая** ссылка на файл данной версии |

### 📄 Список актуальных сортируемых категорий:
| "category": "..." | Название |
|---|---|
| "games" | Игры |
| "store" | Др. магазины приложений |
| "entertaintment" | Развлечения |
| "music+video" | Музыка + Видео |
| "tools" | Инструменты |
| "livestyle" | Лайвстайл |
| "news+weather" | Новости + погода |
| "health+fitness" | Здоровье + фитнес |
| "photo" | Фото |
| "social" | Социальные |
| "sports" | Спорт |
| "business" | Бизнес |
| "education" | Обучение |

>[!NOTE]
>В колонке "category" вы можете писать абсолютно любые слова. Все прилодения с **нестандартными** категориями будут отправлять в одну общую - "Прочее".
