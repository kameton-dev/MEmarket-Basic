Читайте также на другом языке: [English](https://github.com/kameton-dev/MEmarket-Basic/blob/main/README-en.md).

# Создание своего собственного репозитория для MEmarket
ляляля я семён лобанов. это гайд как создать собственный репозиторий для великого MEmarket. если вы планируете хостить свой репо через гитхаб, можете сделать форк

>[!IMPORTANT]
>Aрхитектура MEmarket сейчас находится на стадии **активной разработки**. Будьте готовы к частым обновлениям: добавлением, удалением и изменениям структуры репозиторий

---

## Список актуальных репозиторий:
```[WP8,1; W10M] MEmarket basic - http://millenniummarket.ru/properties.json```

```[W10M] Win10Markt - http://markt.hotsamsa.top/properties.json```

```[WP8,1; W10M] LegacyProjects - https://dvltvv.github.io/legacyprojects-apps/properties.json```

```[WP8,1] ReOpen Market - https://raw.githubusercontent.com/OpenGlebsur/WP8-MEMarketRepo/refs/heads/main/properties.json ```

---

## Хост вашего репозитория
Размещать ваш репозиторий вы можете где угодно: будь это ваш личный сервер либо GitHub Pages (как здесь).
>[!NOTE]
>Рекомендуется размещать свой сервер по протоколу HTTP для лучшей работы с клиентом под WP8.1 (честно говоря с HTTPS оно адекатно работает)

## 📂 Структура репозитория
Самое главное - **не пихать все файлы в одну общую папку**, иначе можно потеряться в своем же репозитории при добавлении больше приложений. Вот мой пример структуры репозитория:

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
> 1. Советую именовать папки с файлами приложений также, как их id. Так будет лучше ориентироваться.
>
> 2. Загружайте иконки для приложений в адекватном качестве! Не 8к, но и не шакальное.

---

## ⚙️ Структура properties.json
Самая **важная и неотъемлемая** часть репозитория. Этот файл нужен, чтобы клиенты MEmarket видели приложения, могли прокладывать путь к фотографиям и файлам для установки:

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
      "min_ver": "1607",
      "title": "Game Name",
      "screenshots": ["screen1.png", "screen2.png"],
      "author": "Вася пупкин",
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
| supported_os | Поддерживаемые ОС репозитория: **пока поддерживаются только WP8.1 и W10M** |
| apps | Список объектов с данными о приложениях |

### Описание полей в "apps":
| Поле | Описание |
|---|---|
| id | Уникальный идентификатор приложения |
| base_url | Базовый путь к папке с данными о приложении. Там должны храниться иконка, файл и скриншоты |
| os | ОС приложения: W10M или WP8.1 |
| min_ver | Нужно **ТОЛЬКО** для приложений W10M: Информирует пользователю минимальную версию сборки/версии Windows 10. Можно писать и так (15063), и так (1703) |
| title | Название приложения |
| screenshots | Перечисление по порядку названий скриншотов из папки base_url к приложению. Если их нет, можете отсавить поле пустым: `[ ]` |
| author | Создатель данного приложения |
| description | Описание приложения |
| icon_url | Название иконки приложения в папке base_url |
| size | Вес файла |
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

---

## 📄 Список актуальных сортируемых категорий:
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
