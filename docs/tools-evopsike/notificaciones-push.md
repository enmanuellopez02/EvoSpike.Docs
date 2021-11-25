# Notificaciones push

Emita notificaciones push con nuestra api de notificaciones de una manera muy fácil, adicione nuestra configuración publica a su projecto y siga las instrucciones de la documentación para crear su integración con nuestra api y luego emita notificaciones tanto web como a dispositivos moviles.

para generar notificaciones push, haga click sobre el botón `Crear notificaiones push`, luego haga click en el botón `Copiar` para copiar la configuración que debe agregar a su projecto.

## Configurar una app cliente en javascript

Las notificaciones solo son compatible con las páginas que se transmiten a través de HTTPS. Esto se debe a que usan service workers que solo están disponibles en sitios HTTPS

### Agregar un listener para notificar a los usuarios

Agrege el código a continuación en un archivo llamado `firebase-messaging-sw.js` en su carpeta public en caso de que este útilizando react o agregelo en un archivo independiente en caso de que sea una aplicación web MPA y registre el service worker, puede consultar la documentación de javascript si no sabe como realizarlo.

En `firebase.initializeApp` pegue el código que copio anterior mente en tools.evospike.com/notificaciones-push

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

// Estas notificaciones son en segundo plano, cuando el usuario esta fuera de la aplicación
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

### Obtener un token de registro de una instancia de app

En su javascript principal agregue el siguiente código para obtener un token de registro, el cual debera almacenar de forma segura, ya que sera utilizado posterior mente para emitir notificaciones a dicha instancia.

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

Para utilizar los métodos del código anterior importe este script en el archivo javascript que desea utilizar, *Recuerde que el tipo de archivo javascript debe contenter el atributo type=module*.

## Ejemplo

```javascript
import { getTokenAsync, onMessageListenner } from "{your file path}"

window.addEventListenner("load", () => {
    getTokenAsync().then(currentToken => {
        console.log(currentToken)
    })

    // Estas notificaciones son en primer plano, cuando el usuario este dentro de la aplicación
    onMessageListenner().then(payload => {
        new Notification(payload.notification.title, { body: payload.notification.body })
    })
})
```

Para emitir una notificación utilizando nuestra **API** realize una solicitud POST a la siguiente url https://tools-evospike-funtions.azurewebsites.net/api/notifications enviando el el body el siguiente **JSON**

```JSON
{
    "Title": "{titulo}",
    "Body": "{contenido}",
    "Token": "{el token a quien se le enviara la notificación}"
}
```

Luego recibira un mensaje con el siguiente formato

```JSON
{
    "Status": "{estatus del mensaje}"
}
```