# NativeScript Sound

Play a sound in your NativeScript app.

This project was originally programmed by John Bristowe. However when this plugin is used in a project installed on a phone with iOS 13.2, the entire application would crash. This fork is a modified version of the original project that solves the instantiation crash issue that I encountered. The rest of the project remained intact.

## Installation

Run the following command from the root of your project:

```
npm i nativescript-sound-kak
```

## Usage

To use this plugin you must first require or import it:

```js
//CommonJs
const Sound = require("nativescript-sound-kak");

//ES6 Import
import * as Sound from "nativescript-sound-kak";
```

### Create and Play

It's important to preload the audio file into the **sound** module before playing it; there is a delay during creation due to the audio being processed:

```js
const beep = Sound.create("./path/to/file.mp3"); // preload the audio file

// play the sound (i.e. tap event handler)
beep.play();
```

You may wish to check that the file actually exists:

```js
import * as fs from "tns-core-modules/file-system";
import * as Sound from 'nativescript-sound-kak';

// currentApp().path leads to your app folder in the project
const pathToBeep = fs.path.join(fs.knownFolders.currentApp().path, '/assets/sounds/beep.mp3');
let beep;
if (fs.File.exists(pathToBeep)) {
	beep = Sound.create(pathToBeep);
}
```

### stop

```js
beep.stop();
```

### reset

```js
beep.reset();
```

### Background Playback

In iOS, the default playback method will silence all background sounds. You can define whether the audio playback in the app silences background audio (i.e. the Music app) or if it play concurrently.

```js
import * as Sound from 'nativescript-sound-kak';
// Sets the audio playback to background, i.e. allows it to play at the same time as other background audio.
Sound.setBackground(true);
```

```js
import * as Sound from 'nativescript-sound-kak';
// Turns off background playback. When the Sound object is created, background audio will be silenced
Sound.setBackground(false);
```