# Push notifications

Issue push notifications with our notifications api in a very easy way, add our public configuration to your project and follow the instructions in the documentation to create your integration with our api and then issue notifications to both web and mobile devices.

To generate push notifications, click the `Create push notifications` button, then click the `Copy` button to copy the settings to add to your project.

## Configure a client app in javascript

Notifications are only supported for pages that are streamed over HTTPS. This is because they use service workers that are only available on HTTPS sites.

### Add a listener to notify users

Add the code below in a file called `firebase-messaging-sw.js` in your public folder in case you are using react or add it in a separate file in case you are an MPA web application and register the service worker, you can refer to the javascript documentation if you don't know how to do it.

In `firebase.initializeApp` paste the code I copied earlier from tools.evospike.com/push-notifications

``` javascript
importScripts('https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js');
importScripts('https://www.gstatic.com/firebasejs/8.10.0/firebase-messaging.js');

firebase.initializeApp({
  apiKey: "{apiKey}",
  projectId: "{projectId}",
  messagingSenderId: "{messagingSenderId}",
  appId: "{appId}"
});

const messaging = firebase.messaging();

// These notifications are in the background, when the user is out of the application.
messaging.onBackgroundMessage((payload) => {
  // Customize notification here
  const notificationTitle = payload.notification.title;
  const notificationOptions = {
    body: payload.notification.body,
    icon: '{icon url}'
  };

  self.registration.showNotification(notificationTitle, notificationOptions);
});
```

### Get a registration token from an app instance

In your main javascript add the following code to obtain a registration token, which should be stored securely, since it will be used later to issue notifications to said instance.

```javascript
importScripts('https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js');
importScripts('https://www.gstatic.com/firebasejs/8.10.0/firebase-messaging.js');

const firebaseConfig = {
  apiKey: "{apiKey}",
  projectId: "{projectId}",
  messagingSenderId: "{messagingSenderId}",
  appId: "{appId}",
  vapidKey: "{vapidKey}"
}

firebase.initializeApp(firebaseConfig);

const getTokenAsync = async () => {
  let currentToken = ""
  const { REACT_APP_VAPID_KEY } = firebaseConfig.vapidKey
  
  try {
    currentToken = await getToken(messaging, { vapidKey: REACT_APP_VAPID_KEY })

    if(currentToken) {
      // Send the token to your server and update the UI if necessary
    }
    else {
      console.log('No registration token available. Request permission to generate one.');
    }
  }
  catch(err) {
    console.log('An error occurred while retrieving token. ', err);
  }

  return currentToken
}

const onMessageListenner = () => {
  return new Promise((resolve) => {
    onMessage(messaging, (payload) => {
      resolve(payload)
    })
  })
}

export { getTokenAsync, onMessageListenner }
```

To use the methods of the code above, import this script into the javascript file you want to use, *Remember that the type of the javascript file must contain the type=module* attribute.

## Example

```javascript
import { getTokenAsync, onMessageListenner } from "{your file path}"

window.addEventListenner("load", () => {
    getTokenAsync().then(currentToken => {
        console.log(currentToken)
    })

    // These notifications are in the foreground, when the user is inside the application
    onMessageListenner().then(payload => {
        new Notification(payload.notification.title, { body: payload.notification.body })
    })
})
```

To issue a notification using our **API** make a POST request to the following url https://tools-evospike-functions.azurewebsites.net/api/notifications by sending the body the following **JSON**

```JSON
{
    "Title": "{title}",
    "Body": "{content}",
    "Token": "{the token to whom the notification will be sent}"
}
```

Then you will receive a message with the following format

```JSON
{
    "Status": "{message status}"
}
```