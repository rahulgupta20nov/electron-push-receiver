# electron-push-receiver

A module to bring Web Push support to [Electron](https://github.com/electron/electron) allowing it to receive notifications from Firebase Cloud Messaging (FCM).

## Why and how ?


## Install

```
npm i -S electron-push-receiver
```

## Usage

- In `main.js` / in main process :

```javascript
const { setup: setupPushReceiver } = require('electron-push-receiver');

// Call it before 'did-finish-load' with mainWindow a reference to your window
setupPushReceiver(mainWindow.webContents);
```

- In renderer process :

```javascript
import { ipcRenderer } from 'electron';
import {
  START_NOTIFICATION_SERVICE,
  NOTIFICATION_SERVICE_STARTED,
  NOTIFICATION_SERVICE_ERROR,
  NOTIFICATION_RECEIVED as ON_NOTIFICATION_RECEIVED,
  TOKEN_UPDATED,
} from 'electron-push-receiver-v2/src/constants';

// Listen for service successfully started
ipcRenderer.on(NOTIFICATION_SERVICE_STARTED, (_, token) => // do something);
// Handle notification errors
ipcRenderer.on(NOTIFICATION_SERVICE_ERROR, (_, error) => // do something);
// Send FCM token to backend
ipcRenderer.on(TOKEN_UPDATED, (_, token) => // Send token);
// Display notification
ipcRenderer.on(ON_NOTIFICATION_RECEIVED, (_, notification) => // display notification);
// Start service
ipcRenderer.send(START_NOTIFICATION_SERVICE, {
  firebase: {
    apiKey: [YOUR_API_KEY],
    appID: [YOUR_APP_ID],
    projectID: [YOUR_PROJECT_ID]
  }
});
```

## Example

.
