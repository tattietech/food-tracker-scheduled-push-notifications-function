# 🔔 Food Tracker - Scheduled Push Notifications Function

An Appwrite serverless function repository for the Food Tracker app that sends push notifications to users when their food items are about to expire. This function runs on a schedule to proactively notify users about items expiring the next day.

## 📋 Overview

This repository contains an Appwrite function designed to work with the Food Tracker app. The function queries the database for food items expiring tomorrow, identifies the households and users associated with those items, and sends targeted push notifications to alert users before their food goes bad.

**Note**: This implementation is designed for development use. The notification delivery mechanism may be refactored in future versions.

## 🚀 Quick Start

### Prerequisites

- [Appwrite CLI](https://appwrite.io/docs/command-line) installed
- Appwrite project set up
- Node.js 22.0 or higher

### Deployment

1. Clone this repository:
   ```bash
   git clone https://github.com/tattietech/food-tracker-scheduled-push-notifications-function.git
   cd food-tracker-scheduled-push-notifications-function
   ```

2. Login to Appwrite CLI:
   ```bash
   appwrite login
   ```

3. Deploy the function:
   ```bash
   appwrite deploy function
   ```

4. Configure the schedule in Appwrite Console for daily execution

## 📁 Repository Structure

```
.
├── functions/
│   └── ftnotifications/        # Scheduled push notification function
│       ├── src/
│       │   └── main.js         # Function implementation
│       ├── package.json        # Node.js dependencies
│       └── README.md           # Detailed function documentation
├── appwrite.json               # Appwrite project configuration
└── README.md                   # This file
```

## 🔧 Configuration

This repository uses `appwrite.json` to define:
- Database schema (collections: food_space, users, household, item)
- Function configuration and permissions
- Messaging topics

For detailed function configuration, see [functions/ftnotifications/README.md](functions/ftnotifications/README.md).

## 📦 Functions

### Scheduled Expiry Notification

Located in `functions/ftnotifications/`, this function:
- Runs on a schedule (configured in Appwrite Console)
- Queries for items expiring tomorrow
- Groups items by household and user
- Sends personalized push notifications

For more details, see the [function-specific README](functions/ftnotifications/README.md).

## 🛠️ Development

### Working with the Function

Navigate to the function directory:
```bash
cd functions/ftnotifications
```

Install dependencies:
```bash
npm install
```

Format code:
```bash
npm run format
```

### Testing Locally

You can test the function locally using the Appwrite CLI:
```bash
appwrite run function --functionId=<your-function-id>
```

## 🔒 Environment Variables

The function requires the following environment variables (automatically provided by Appwrite):

- `APPWRITE_FUNCTION_API_ENDPOINT` - Appwrite API endpoint
- `APPWRITE_FUNCTION_PROJECT_ID` - Appwrite project ID
- `DATABASE` - Database ID for food tracker
- `ITEM_COLLECTION` - Collection ID for food items
- `HOUSEHOLD_COLLECTION` - Collection ID for household data

## 📄 License

This project is part of the Food Tracker application ecosystem.

## 🔗 Related Projects

- Food Tracker App (main application repository)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
