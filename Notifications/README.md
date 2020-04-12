# Notifications
The Notifications API allows web pages to control the display of system notifications to the end user. These are outside the top-level browsing context viewport, so therefore can be displayed even when the user has switched tabs or moved to a different app. The API is designed to be compatible with existing notification systems, across different platforms.

> Secure context :lock:
This feature is available only in secure contexts (HTTPS), in some or all supporting browsers.

## Requesting permission
Before an app can send a notification, the user must grant the application the right to do so. This is a common requirement when an API tries to interact with something outside a web page — at least once, the user needs to specifically grant that application permission to present notifications, thereby letting the user control which apps/sites are allowed to display notifications.

Because of abuses of push notifications in the past, web browsers and developers have begun to implement strategies to help mitigate this problem. You should only request consent to display notifications in response to a user gesture (e.g. clicking a button). This is not only best practice — you should not be spamming users with notifications they didn't agree to — but going forward browsers will explicitly disallow notification permission requests not triggered in response to a user gesture. Firefox is already doing this from version 72, for example, and Safari has done it for some time.

In addition, In Chrome and Firefox you cannot request notifications at all unless the site is a secure context (i.e. HTTPS), and you can no longer allow notification permissions to be requested from cross-origin ```<iframe>```s.

Checking current permission status
You can check to see if you already have permission by checking the value of the Notification.permission read only property. It can have one of three possible values:

##### default
The user hasn't been asked for permission yet, so notifications won't be displayed.
##### granted
The user has granted permission to display notifications, after having been asked previously.
##### denied
The user has explicitly declined permission to show notifications.
Getting permission
If permission to display notifications hasn't been granted yet, the application needs to use the Notification.requestPermission() method to request this from the user. In its simplest form, we just include the following:

```js
Notification.requestPermission().then(function(result) {
  console.log(result);
});
```
This uses the promise-based version of the method. If you want to support older versions, you might have to use the older callback version, which looks like this:

```js
Notification.requestPermission();
```
The callback version optionally accepts a callback function that is called once the user has responded to the request to display permissions.

## Creating a notification
Creating a notification is easy; just use the Notification constructor. This constructor expects a title to display within the notification and some options to enhance the notification such as an icon or a text body.

For example, in the to-do-list example we use the following snippet to create a notification when required (found inside the ```createNotification()``` function):

```js
var img = '/to-do-notifications/img/icon-128.png';
var text = 'HEY! Your task "' + title + '" is now overdue.';
var notification = new Notification('To do list', { body: text, icon: img });
```
## Closing notifications
Used ```close()``` to remove a notification that is no longer relevant to the user (e.g. the user already read the notification on the webpage, in the case of a messaging app, or the following song is already playing in a music app to notifies upon song changes). Most modern browsers dismiss notifications automatically after a few moments (around four seconds) but this isn't something you should generally be concerned about as it's up to the user and user agent. The dismissal may also happen at the operating system level and users should remain in control of this. Old versions of Chrome didn't remove notifications automatically so you can do so after a setTimeout() only for those legacy versions in order to not remove notifications from notification trays on other browsers.
```js
var n = new Notification('My Great Song');
document.addEventListener('visibilitychange', function() {
  if (document.visibilityState === 'visible') {
    // The tab has become visible so clear the now-stale Notification.                                                                                                                                      
    n.close();
  }
});
```

## Notification events
There are four events that are triggered on the Notification instance:

##### click
Triggered when the user clicks on the notification.
##### close
Triggered once the notification is closed.
##### error
Triggered if something goes wrong with the notification; this is usually because the notification couldn't be displayed for some reason.
##### show
Triggered when the notification is displayed to the user.
These events can be tracked using the onclick, onclose, onerror, and onshow handlers. Because Notification also inherits from EventTarget, it's possible to use the addEventListener() method on it.

## Replacing existing notifications
It is usually undesirable for a user to receive a lot of notifications in a short space of time — for example, what if a messenger application notified a user for each incoming message, and they were being sent a lot? To avoid spamming the user with too many notifications, it's possible to modify the pending notifications queue, replacing single or multiple pending notifications with a new one.

To do this, it's possible to add a tag to any new notification. If a notification already has the same tag and has not been displayed yet, the new notification replaces that previous notification. If the notification with the same tag has already been displayed, the previous notification is closed and the new one is displayed.

#### Tag example
Assume the following basic HTML:
```html
<button>Notify me!</button>
```
It's possible to handle multiple notifications this way:
```js
window.addEventListener('load', function () {
  // At first, let's check if we have permission for notification
  // If not, let's ask for it
  if (window.Notification && Notification.permission !== "granted") {
    Notification.requestPermission(function (status) {
      if (Notification.permission !== status) {
        Notification.permission = status;
      }
    });
  }

  var button = document.getElementsByTagName('button')[0];

  button.addEventListener('click', function () {
    // If the user agreed to get notified
    // Let's try to send ten notifications
    if (window.Notification && Notification.permission === "granted") {
      var i = 0;
      // Using an interval cause some browsers (including Firefox) are blocking notifications if there are too much in a certain time.
      var interval = window.setInterval(function () {
        // Thanks to the tag, we should only see the "Hi! 9" notification 
        var n = new Notification("Hi! " + i, {tag: 'soManyNotification'});
        if (i++ == 9) {
          window.clearInterval(interval);
        }
      }, 200);
    }

    // If the user hasn't told if he wants to be notified or not
    // Note: because of Chrome, we are not sure the permission property
    // is set, therefore it's unsafe to check for the "default" value.
    else if (window.Notification && Notification.permission !== "denied") {
      Notification.requestPermission(function (status) {
        // If the user said okay
        if (status === "granted") {
          var i = 0;
          // Using an interval cause some browsers (including Firefox) are blocking notifications if there are too much in a certain time.
          var interval = window.setInterval(function () {
            // Thanks to the tag, we should only see the "Hi! 9" notification 
            var n = new Notification("Hi! " + i, {tag: 'soManyNotification'});
            if (i++ == 9) {
              window.clearInterval(interval);
            }
          }, 200);
        }

        // Otherwise, we can fallback to a regular modal alert
        else {
          alert("Hi!");
        }
      });
    }

    // If the user refuses to get notified
    else {
      // We can fallback to a regular modal alert
      alert("Hi!");
    }
  });
});
```

Play with the code [here](https://jsfiddle.net/z7yjv9d5/).