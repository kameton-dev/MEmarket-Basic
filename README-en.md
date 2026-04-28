# Creating Your Own Repository for MEmarket
Lya-la-la, I'm Semyon Lobanov. This is a guide on how to create your own repository for the great MEmarket. If you plan to host your repo on GitHub, you can fork it.

## List of current repositories:
```MEmarket basic - http://millenniummarket.ru/properties.json```

```Win10Markt - http://markt.hotsamsa.top/properties.json```

## Hosting
You can host the repository on your own server or on GitHub; it doesn't really matter. Just a few things:
>[!NOTE]
>It's recommended to host your server using the http:// protocol. However, it works fine with https as well.

## 📂 Repository Structure
Generally, the application structure here is not strict. That is, you can create folders of any name. But for this example, I'll use my own structure:
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
> 1. I recommend naming folders containing app files the same as their IDs. This will make navigation easier.
>
> 2. Upload app icons in adequate quality! Not 8K, but not so high that the poor LumiAs won't be able to digest them.
>

## ⚙️ Properties.json structure
The most important part of the repository. This is where things get much more strict:
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
      "screenshots": ["1.png", "2.png", "3.png", "4.png"],
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
      "screenshots": [],
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

### Field Descriptions:
| Field | Description |
|---|---|
| repo_name | The name of your store, which the user will see in the repository settings |
| id | The app identifier. Must be unique, without 1 2 3 4 5 |
| apps | List of objects with app data |
| download_url | **Direct** link to the file. Needed for retrieving and downloading the file |
| size | File size (for user information. If you can do funny things there, I allow mocking) |
| versions | If you want to download different versions of the same app, use this field |
| version | If the app has one version, use the versions field |

### List of currently sortable categories:
| "category": "..." | Name |
|---|---|
| "games" | Games |
| "entertainment" | Entertainment |
| "music+video" | Music + Video |
| "tools" | Tools |
| "livestyle" | Lifestyle |
| "news+weather" | News + Weather |
| "social" | Social |
| "education" | Education |

>[!NOTE]
>You can enter absolutely any words in the "category" column. All apps with non-standard categories will be sorted into a single, general category: "Other."
