# Creating Your Own Repository for MEmarket
This is a guide on how to create your own repository for the great MEmarket. If you plan to host your repo on GitHub, you can fork it.

## List of current repositories:
```MEmarket basic - http://millenniummarket.ru/properties.json```

```Win10Markt - http://markt.hotsamsa.top/properties.json```

```LegacyProjects WP8 - https://dvltvv.github.io/legacyprojects-wp8/properties.json```

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
│     │    ├── app1.xap (or .appx)
│     │    ├── app2.xap (or .appx)
│     │    └── app-icon.png
│     └── game.example/
│          ├── game1.xap (or .appx)
│          ├── game-icon.png
│          ├── screen1.png
│          └── screen2.png
└── properties.json        <-- Main index file
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
      "author": "John Doe"
      "description": "xddcc",
      "icon_url": "game1-icon.png",
      "size": "1488 MB",
      "category": "game",
      "version": "0.9b",
      "download_url": "https://domain.com/files/game1.xap"
    }
  ]
}

```
### Repository field descriptions:
| Field | Description |
|---|---|
| repo_name | The name of your store, which will be visible to the user in the repository settings |
| creator | Your nickname as the repository creator |
| last_updated | Date of the last repository update |
| apps | List of objects with application data |

### "apps" array description:
| Field | Description |
|---|---|
| id | Unique application identifier |
| base_url | Base path to the application data folder. This should contain the icon, file, and screenshots |
| title | Application name |
| screenshots | A list of screenshot names in the base_url folder for the application, in order. If none are present, you can leave this field blank: [] |
| author | Creator of this application |
| description | Application description |
| icon_url | Name of the app icon in the base_url folder |
| size | File size (for user information. If you can do anything funny there, I'll allow it for now) |
| category | A suitable category name for the app / a category from the list below |
| version | App version |
| download_url | **Direct** link to the file. Needed to retrieve and download the file |

>[!NOTE]
>If you want to download multiple versions of the same app, use the "versions" field.

### Description of "versions"
| Field | Description |
|---|---|
| version | Name of this app version |
| download_url | **Direct** link to the file for this version |

### List of currently sortable categories:
| "category": "..." | Name |
|---|---|
| "games" | Games |
| "store" | Alt app stores |
| "entertainment" | Entertainment |
| "music+video" | Music + Video |
| "tools" | Tools |
| "livestyle" | Lifestyle |
| "news+weather" | News + Weather |
| "health+fitness" | Health + Fitness |
| "photo" | Photo |
| "social" | Social |
| "sports" | Sports |
| "business" | Business |
| "education" | Education |

>[!NOTE]
>You can enter absolutely any words in the "category" column. All apps with non-standard categories will be sorted into a single, general category: "Other."
