# tray

A `Tray` represents an icon in operating system's notification area, it is
usually attached with a context menu.

```javascript
var app = require('app');
var Menu = require('menu');
var Tray = require('tray');

var appIcon = null;
app.on('ready', function(){
  appIcon = new Tray('/path/to/my/icon');
  var contextMenu = Menu.buildFromTemplate([
    { label: 'Item1', type: 'radio' },
    { label: 'Item2', type: 'radio' },
    { label: 'Item3', type: 'radio', checked: true },
    { label: 'Item4', type: 'radio' }
  ]);
  appIcon.setToolTip('This is my application.');
  appIcon.setContextMenu(contextMenu);
});

```

__Platform limitations:__

* On Linux app indicator will be used if it is supported, otherwise
  `GtkStatusIcon` will be used instead.
* On Linux distributions that only have app indicator support, you have to
  install `libappindicator1` to make tray icon work.
* App indicator will only be showed when it has context menu.
* When app indicator is used on Linux, `clicked` event is ignored.

So if you want to keep exact same behaviors on all platforms, you should not
rely on `clicked` event and always attach a context menu to the tray icon.

## Class: Tray

`Tray` is an [EventEmitter][event-emitter].

### new Tray(image)

* `image` [NativeImage](native-image.md)

Creates a new tray icon associated with the `image`.

### Event: 'clicked'

* `event` Event
  * `altKey` Boolean
  * `shiftKey` Boolean
  * `ctrlKey` Boolean
  * `metaKey` Boolean
* `bounds` Object - the bounds of tray icon
  * `x` Integer
  * `y` Integer
  * `width` Integer
  * `height` Integer

Emitted when the tray icon is clicked.

__Note:__ The `bounds` payload is only implemented on OS X and Windows.

### Event: 'right-clicked'

* `event` Event
  * `altKey` Boolean
  * `shiftKey` Boolean
  * `ctrlKey` Boolean
  * `metaKey` Boolean
* `bounds` Object - the bounds of tray icon
  * `x` Integer
  * `y` Integer
  * `width` Integer
  * `height` Integer

Emitted when the tray icon is right clicked.

__Note:__ This is only implemented on OS X and Windows.

### Event: 'double-clicked'

* `event` Event
  * `altKey` Boolean
  * `shiftKey` Boolean
  * `ctrlKey` Boolean
  * `metaKey` Boolean
* `bounds` Object - the bounds of tray icon
  * `x` Integer
  * `y` Integer
  * `width` Integer
  * `height` Integer

Emitted when the tray icon is double clicked.

__Note:__ This is only implemented on OS X and Windows.

### Event: 'balloon-show'

Emitted when the tray balloon shows.

__Note:__ This is only implemented on Windows.

### Event: 'balloon-clicked'

Emitted when the tray balloon is clicked.

__Note:__ This is only implemented on Windows.

### Event: 'balloon-closed'

Emitted when the tray balloon is closed because of timeout or user manually
closes it.

__Note:__ This is only implemented on Windows.

### Event: 'drop-files'

* `event`
* `files` Array - the file path of dropped files.

Emitted when dragged files are dropped in the tray icon.

__Note:__ This is only implemented on OS X.

### Tray.destroy()

Destroys the tray icon immediately.

### Tray.setImage(image)

* `image` [NativeImage](native-image.md)

Sets the `image` associated with this tray icon.

### Tray.setPressedImage(image)

* `image` [NativeImage](native-image.md)

Sets the `image` associated with this tray icon when pressed on OS X.

### Tray.setToolTip(toolTip)

* `toolTip` String

Sets the hover text for this tray icon.

### Tray.setTitle(title)

* `title` String

Sets the title displayed aside of the tray icon in the status bar.

__Note:__ This is only implemented on OS X.

### Tray.setHighlightMode(highlight)

* `highlight` Boolean

Sets whether the tray icon is highlighted when it is clicked.

__Note:__ This is only implemented on OS X.

### Tray.displayBalloon(options)

* `options` Object
  * `icon` [NativeImage](native-image.md)
  * `title` String
  * `content` String

Displays a tray balloon.

__Note:__ This is only implemented on Windows.

### Tray.popUpContextMenu([position])

* `position` Object - The pop position
  * `x` Integer
  * `y` Integer

The `position` is only available on Windows, and it is (0, 0) by default.

__Note:__ This is only implemented on OS X and Windows.

### Tray.setContextMenu(menu)

* `menu` Menu

Sets the context menu for this icon.

[event-emitter]: http://nodejs.org/api/events.html#events_class_events_eventemitter
