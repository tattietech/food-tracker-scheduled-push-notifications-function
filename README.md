# 🔔 Food Tracker - Scheduled Push Notifications Function

An Appwrite serverless function that sends push notifications to users of the Food Tracker app when their food items are about to expire. This function runs on a schedule to proactively notify users about items expiring the next day.

## 📋 Overview

This function is designed to work with the Food Tracker app, which is built on Appwrite (Backend as a Service platform). It queries the database for food items expiring tomorrow, identifies the households and users associated with those items, and sends targeted push notifications to alert users before their food goes bad.

**Note**: This implementation is designed for development use. The notification delivery mechanism may be refactored in future versions.

## 🚀 How It Works

1. **Query Expiring Items**: Fetches all food items from the database with an expiry date matching tomorrow's date
2. **Retrieve Household Information**: For each expiring item, retrieves the associated household and its users
3. **Get Push Notification Targets**: Identifies push notification targets for each user in the household
4. **Aggregate Notifications**: Groups multiple expiring items per user into a single notification
5. **Send Push Notifications**: Delivers customized push notifications with item details

### Notification Messages

- **Single item**: "{Item name} is expiring tomorrow!"
- **Two items**: "{First item} and one other item is expiring tomorrow!"
- **Multiple items**: "{First item} and {count} other items are expiring tomorrow!"

## ⚙️ Configuration

| Setting           | Value                          |
| ----------------- | ------------------------------ |
| Runtime           | Node (22.0)                    |
| Entrypoint        | `src/main.js`                  |
| Build Commands    | `npm install`                  |
| Permissions       | See scopes below               |
| Timeout (Seconds) | 15                             |
| Schedule          | Configured in Appwrite Console |
| Specification     | s-0.5vcpu-512mb                |

### Required Scopes

- `users.read` - Read user information
- `databases.read` - Read database records
- `documents.read` - Read document details
- `targets.read` - Read push notification targets
- `providers.read` - Read messaging providers
- `messages.write` - Send push notifications

## 🔒 Environment Variables

The following environment variables are required and automatically provided by Appwrite:

| Variable                         | Description                      |
| -------------------------------- | -------------------------------- |
| `APPWRITE_FUNCTION_API_ENDPOINT` | Appwrite API endpoint            |
| `APPWRITE_FUNCTION_PROJECT_ID`   | Appwrite project ID              |
| `DATABASE`                       | Database ID for food tracker     |
| `ITEM_COLLECTION`                | Collection ID for food items     |
| `HOUSEHOLD_COLLECTION`           | Collection ID for household data |

**Note**: The function also requires an API key passed via the `x-appwrite-key` header when triggered.

## 📦 Dependencies

- `node-appwrite` (^12.0.1) - Official Appwrite SDK for Node.js

## 🛠️ Development

To format the code:

```bash
npm run format
```

This uses Prettier to maintain consistent code style across the project.

## 📊 Response Format

The function returns a JSON array of notifications that were sent:

```json
[
  {
    "target": "target-id-1",
    "items": ["Milk", "Eggs", "Cheese"]
  },
  {
    "target": "target-id-2",
    "items": ["Bread"]
  }
]
```

## 🔮 Future Improvements

This is a development implementation. Future versions may include:

- Alternative notification delivery mechanisms
- Customizable notification timing (e.g., 2 days, 3 days before expiry)
- User preference management for notification frequency
- Support for multiple notification channels (email, SMS, etc.)
