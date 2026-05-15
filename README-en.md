# Creating Your Own Repository for MEmarket
This is a guide on how to create your own repository for the great MEmarket. If you plan to host your repo on GitHub, you can fork it.

>[!IMPORTANT]
>The MEmarket architecture is currently under active development. Be prepared for frequent updates: additions, removals, and changes to the repository structure.

---

## List of current repositories:
```[WP8,1; W10M] MEmarket basic - http://millenniummarket.ru/properties.json```

```[W10M] Win10Markt - http://markt.hotsamsa.top/properties.json```

```[WP8,1; W10M] LegacyProjects - https://dvltvv.github.io/legacyprojects-apps/properties.json```

```[WP8,1] ReOpen Market - https://raw.githubusercontent.com/OpenGlebsur/WP8-MEMarketRepo/refs/heads/main/properties.json ```

---

## Hosting your repo
You can host your repository anywhere: on your personal server or GitHub Pages (like here).
>[!NOTE]
>It's recommended to host your server over HTTP for best performance with the WP8.1 client (to be honest, it works fine with HTTPS).

## 📂 Repository Structure
The most important thing is to **not stuff all the files into one shared folder**, otherwise you can get lost in your own repository when adding more apps. Here's an example of my repository structure:

```text
example-repo/
├── apps/
│     ├── app.example/
│     │    ├── app1.xap (or .appx)
│     │    ├── app2.xap (or .appx)
│     │    └── app-icon.png
│     └── game.example/
│          ├── game1.appx
│          ├── game-icon.png
│          ├── screen1.png
│          └── screen2.png
└── properties.json        <-- Main index file
```

> [!TIP]
> 1. I recommend naming folders containing app files the same as their IDs. This will make navigation easier.
>
> 2. Upload app icons in adequate quality! Not 8K, but not so lowest

---

## ⚙️ Properties.json structure
The most **important and integral** part of the repository. This file is needed so MEmarket clients can see apps and navigate to photos and files for installation:

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

### Repository field descriptions:
| Field | Description |
|---|---|
| repo_name | The name of your store, which will be visible to the user in the repository settings |
| creator | Your nickname as the repository creator |
| last_updated | Date of the last repository update |
| supported_os | Supported OS repositories: **only WP8.1 and W10M are supported for now** |
| apps | List of objects with application data |

### "apps" array description:
| Field | Description |
|---|---|
| id | Unique application identifier |
| base_url | Base path to the application data folder. This should contain the icon, file, and screenshots |
| os | Application OS: W10M or WP8.1 |
| min_ver | Needed **ONLY** for W10M apps: Informs the user of the minimum build/version of Windows 10. Can be written both like this (15063) and like this (1703) |
| title | Application name |
| screenshots | A list of screenshot names in the base_url folder for the application, in order. If none are present, you can leave this field blank: `[ ]` |
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

---

## 📄 List of currently sortable categories:
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
