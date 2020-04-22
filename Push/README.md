# Push
The Push API gives web applications the ability to receive messages pushed to them from a server, whether or not the web app is in the foreground, or even currently loaded, on a user agent. This lets developers deliver asynchronous notifications and updates to users that opt in, resulting in better engagement with timely new content.

## Push concepts and usage
>  When implementing PushManager subscriptions, it is vitally important that you protect against CSRF/XSRF issues in your app.

For an app to receive push messages, it has to have an active service worker. When the service worker is active, it can subscribe to push notifications, using PushManager.subscribe().

The resulting PushSubscription includes all the information that the application needs to send a push message: an endpoint and the encryption key needed for sending data.

The service worker will be started as necessary to handle incoming push messages, which are delivered to the ServiceWorkerGlobalScope.onpush event handler. This allows apps to react to push messages being received, for example, by displaying a notification (using ServiceWorkerRegistration.showNotification().)

Each subscription is unique to a service worker.  The endpoint for the subscription is a unique capability URL: knowledge of the endpoint is all that is necessary to send a message to your application. The endpoint URL therefore needs to be kept secret, or other applications might be able to send push messages to your application.

Activating a service worker to deliver a push message can result in increased resource usage, particularly of the battery. Different browsers have different schemes for handling this, there is currently no standard mechanism. Firefox allows a limited number (quota) of push messages to be sent to an application, although Push messages that generate notifications are exempt from this limit. The limit is refreshed each time the site is visited. In comparison, Chrome applies no limit, but requires that every push message causes a notification to be displayed.

## Interfaces
#### PushEvent
Represents a push action, sent to the global scope of a ServiceWorker. It contains information sent from an application to a PushSubscription.
#### PushManager
Provides a way to receive notifications from third-party servers, as well as request URLs for push notifications. This interface has replaced the functionality offered by the obsolete PushRegistrationManager interface.
#### PushMessageData
Provides access to push data sent by a server, and includes methods to manipulate the received data.
#### PushSubscription
Provides a subcription's URL endpoint, and allows unsubscription from a push service.

### Service worker additions
The following additions to the Service Worker API have been specified in the Push API spec to provide an entry point for using Push messages. They also monitor and respond to push and subscription change events.

#### ServiceWorkerRegistration.pushManager | Read only
Returns a reference to the PushManager interface for managing push subscriptions including subscribing, getting an active subscription, and accessing push permission status. This is the entry point into using Push messaging.
#### ServiceWorkerGlobalScope.onpush
An event handler fired whenever a push event occurs; that is, whenever a server push message is received.
#### ServiceWorkerGlobalScope.onpushsubscriptionchange
An event handler fired whenever a pushsubscriptionchange event occurs; for example, when a push subscription has been invalidated, or is about to be invalidated (e.g. when a push service sets an expiration time.)

## Examples

#### Register event listener for the ‘push’ event.

 
Keep the service worker alive until the notification is created.

Show a notification with title ‘ServiceWorker Delca’ and body ‘Hi Delca’.
```js
self.addEventListener('push', function(event) {

  event.waitUntil(
    self.registration.showNotification('ServiceWorker Delca', {
      body: 'Hi Delca',
    })
  );
```