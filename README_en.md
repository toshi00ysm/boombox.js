boombox
=======

The JavaScrit library support for audio feature of web browser includes [HTMLVideo](http://www.w3.org/TR/2009/WD-html5-20090825/video.html), [HTMLAudio](http://www.w3.org/TR/html5/embedded-content-0.html#the-audio-element), and [WebAudio](http://www.w3.org/TR/webaudio/).


It will makes you to controlling sound features of browser simply with integrated interfaces and feeling it just like playing with a boombox.

### Why use boombox?

`HTMLAudio`/`WebAudio`/`HTMLVideo` are used for playing sound on web browsers generally, though there are differences between browsers in how to call API and statement of support.

`boombox` privides integrated API encapsulate those differences in environment.
In addition, we designed it with thought of requirement of smartphone-specific like a stoping sound when the browser is inactive, or playing multiple sounds.

Though `boombox` is supposed and designed for general use-case, it will be reachable with creating extention for advanced features and API of `WebAudio` like a mixing. There is no barriers!!


## Demo

[**Single Sound**](http://cyberagent.github.io/boombox.js/demo/single.html)

[![](https://raw2.github.com/CyberAgent/boombox.js/gh-pages/screenshots/demo-single.png)](http://cyberagent.github.io/boombox.js/demo/single.html)

[**Mix Sound**](http://cyberagent.github.io/boombox.js/demo/mix.html)

[![](https://raw2.github.com/CyberAgent/boombox.js/gh-pages/screenshots/demo-mix.png)](http://cyberagent.github.io/boombox.js/demo/mix.html)

## Features

- Play
- Pause
- Stop
- Replay(playback from the begginning)
- Resume(playback from the point of paused)
- PowerON/PowerOFF
- Volume
- Reproducing loop
- Multiple sound playing
    - Support them as possible, depending on browser's support.
- Support for CORS Settings
    - Setting loading options of crossOrigin, location of sound resouces, etc. appropriately, you are available to use them with [CORS](https://developer.mozilla.org/ja/docs/HTTP_access_control) safely.
- Filterings
    - Support output classification with filtering in each environment.

## Reference information


|OS/Browser|audio load event|
|:------------:|:------------:|
|IOS 5: Safari|suspend|
|IOS 6, 7: Safari|suspend|
|Android 2.3: basic|stalled|
|Android 4.0: basic|loadeddata|
|Mac OSX: Chrome|canplay|

====

|OS/Browser|Web Audio|HTML Audio|HTML Video|
|:------------:|:------------:|:------------:|:------------:|
|IOS 5: Safari|-|✔ |✔ \*1|
|IOS 6, 7: Safari|✔|✔|✔ \*1|
|Android 2.3: basic|-|✔|✔|
|Android 4.0: basic|✔ \*2|✔|✔|
|Mac OSX: Chrome|✔|✔|✔|

> `*1` switching to other apps : cannot
>
> `*2` supported partly
> *HTMLVideo* : *appending the Element to any element in document is required* + *if you wish to use sound only, we adviced you to place it to outside of display area.*

====

|OS/Browser|1 sound|2 sound|multi sound|
|:------------:|:------------:|:------------:|:------------:|
|IOS 5: Safari|✔|-|-|
|IOS 6, 7: Safari|✔|✔|✔|
|Android 2.x: basic|✔|✔|✔|
|Android 4.x: basic|✔|✔ \*1|-|
|Mac OSX: Chrome|✔|✔|✔|

> `*1` use HTMLAudio/HTMLVideo at the same time

## Install

### Download

Download `boombox.js` or `boombox.min.js` from the followings.

- [boombox.js](https://raw2.github.com/CyberAgent/boombox.js/master/boombox.js)
- [boombox.min.js](https://raw2.github.com/CyberAgent/boombox.js/master/boombox.min.js)

### npm

```sh
$ npm install boombox.js
```

### Bower

```sh
$ bower install boombox.js
```

### component

```sh
$ component install CyberAgent/boombox.js
```

### HTML

After you get them with described above, load with `<script>` tag.

```html
<script type="text/javascript" src="YOUR/PATH/TO/boombox.js"></script><!-- for development -->
<script type="text/javascript" src="YOUR/PATH/TO/boombox.min.js"></script><!-- for product -->
```

> require.js is supported

## Build

You can build it with [Grunt](http://gruntjs.com/).

```sh
$ git clone https://github.com/CyberAgent/boombox.js.git
$ cd boombox
$ npm install -g grunt-cli # the first time only
$ npm install . # the first time only
$ grunt
```

## Browser Test

Use [Grunt](http://gruntjs.com/) and [beez-foundation](https://npmjs.org/package/beez-foundation) for testing

```sh
$ npm install -g beez-foundation # install server environment for testing (the first time only)
$ cd boombox
$ npm install . # the first time only
$ grunt foundation # star local server
```

@see [beez](https://github.com/CyberAgent/beez)

@see [beez-foundation](https://github.com/CyberAgent/beez-foundation)

**And access in your browser**

> example with script tag : [http://0.0.0.0:1109/m/boombox/spec/global.html](http://0.0.0.0:1109/m/boombox.js/spec/global.html)
>
> example with require.js : [http://0.0.0.0:1109/m/boombox/spec/requirejs.html](http://0.0.0.0:1109/m/boombox.js/spec/requirejs.html#)

## Usage

### Setup

setupping `boombox`

```javascript
boombox.setup();
```

#### Forced use options

Specify method to play sound forcibly

```javascript
{
    webaudio: {
        use: true
    },
    htmlaudio: {
        use: true
    },
    htmlvideo: {
        use: true
    }
}
```

### Load sound file

Load sound file

```javascript
var options = {
    src: [
        {
            media: 'audio/mp4',
            path: 'http://0.0.0.0:1109/m/spec/media/sound.m4a'
        }
    ]
};
boombox.load('sound', options, function (err, audio) {
    // write callback for handling loaded sound here
});

```

> You can specify mulgiple file type to src property as array. They are evaluated from head, and load files are abailable.


### Play

```javascript
boombox.play() // play all sound

boombox.get('sound').play() // play specified sound
```
#### Restriction

It is taken share by many phone that allows playing sounds triggered form user action (ex: MouseEvents) in smartphone market.
Please check your specification of phones you are targeting out.

### Volume control

```javascript
boombox.get.volume(0.5) // change valume of all sound. pass value between 0 and 1

boombox.get('sound').volume(0.5) // change valume of specified sound. pass value between 0 and 1
```

### Cut off the power

Sound stops just like power of boombox is turned off, even if sounds are playing.

#### Specified sound

```javascript
boombox.get('sound').power(boombox.POWER_OFF);
```

#### All sounds.

```javascript
boombox.power(boombox.POWER_OFF);
```

### Loop play

There is two ways for reproducing loop.

- Native Loop(Supported by `HTMLAudio` `WebAudio` `HTMLVideo` natively)
- Original loop(Using `onEnded` event)

```javascript
boombox.get('sound').setLoop(boombox.LOOP_ORIGINAL);
boombox.get('sound').play();
// or

boombox.get('sound').setLoop(boombox.LOOP_NATIVE);
boombox.get('sound').play();
```

### onEnded

Callen when fineshed playing sound to the end.
Use after override it.

```javascript
boombox.get('name').onEnded = function () {
    // write callback here
}
```

### Use filter

You can select sound for playing each phones and browsers, before load sound file, with filterings.
Please care about that they were handled as invalid if one of them is **NG**.

```javascript
boombox.addFilter('chrome', function filter() {
    if (/Chrome/.test(window.navigator.userAgent)) {
        return false; // [ OK ] Chrome
    } else {
        return true;  // [ NG ] others
    }
});
var options = {
    src: [
        {
            media: 'audio/mp4',
            path: 'http://0.0.0.0:1109/m/spec/media/sound.m4a'
        }
    ],
    filter: ["chrome"] // specify filter you desire
};
boombox.load('sound', options, true, function (err, audio) {
    // load sound file
});
```

> You should specify filter because browser's support are varied to playing sound.

### Forced use HTMLVideo

You can use `HTMLVideo` with passing true to third argument of `boombox.load()`.

> for the case that the browser support single sound only at HTMLAudio.


```javascript
var options = {
    src: [
        {
            media: 'audio/mp4',
            path: 'http://0.0.0.0:1109/m/spec/media/sound.m4a'
        }
    ]
};
// pass true to third argument of load()
boombox.load('sound', options, true, function (err, audio) {
    // load sound file
    // you must append it to any element in document if you use HTMLVideo.
});
```

### Cache

Once sound files are loaded, they are cached to `boombox.pool` as instances.

Caching by boombox.pool is very effective in SPA(Single Page Application), because behaviors of caching supplied from browsers are differenced each other.

### Priority

Priority of API `boombox` use by default is as follow.

`WebAudio` > `HTMLAudio` > `HTMLVideo`

- In browser support both `WebAudio` and `HTMLAudio`, `WebAudio` is prioritized.
- `HTMLVideo` is only used when enabled by option.

### currentTime

Seeking(currentTime) is ignored internally even if it are set when that feature isn't available at `HTMLAudio` or `HTMLVideo` in the browser.

### Inactive

`window.onpageshow/onpagehide`, `window.onblur/onfocus`, and `Event.onVisibilityChange` are used to judging whether the browser has gone to background.

> please check your phone whether it is support that, because that isn't avaialble in all phones.

### Customize Events

Please override event handler named as `onXXXX`. Those functions named like that are allowed to customize.

##### onVisibilityChange(e)

Handler for `visibilityChange` event.

##### onFocus(e)

Handler for `window.onFocus` event.

##### onBlur(e)

Handler for `window.onBlur` event.

##### onPageShow(e)

Handler for `window.onpageshow` event.

##### onPageHide(e)

Handler for `window.onpagehide` event.

##### onEnded(e)

Handler callen at sound played to the end. If playing is stoped in a middle, never raised.


```javascript

// simpple usage
boombox.onFocus = function (e) {
    logger.trace('onFocus');
}

// overriding of function

var fn = boombox.onFocus;

boombox.onFocus = function () {
    console.log("override:", onFocus);
    fn.apply(boombox, arguments);
}

```

## TODO

- AudioSprite: gather assets to 1 file.
    - Check develop branch
- localStorage: cache Audio

====

## Sample Sound File

### Location path

- `spec/media/sound.m4a`
- `spec/media/sound.wav`

### Creation software

Sound that was created in AudioSauna

[http://www.audiosauna.com/](http://www.audiosauna.com/)


## Contributing

- Kei FUNAGAYAMA - [@fkei](https://twitter.com/fkei) [github](https://github.com/fkei)
- Masaki Sueda - [github](htpts://github.com/masakisueda)
- HIRAKI Satoru - [github](htpts://github.com/Layzie)

## Copyright

CyberAgent, Inc. All rights reserved.

## LICENSE

@see : [LICENSE](https://github.com/CyberAgent/boombox.js/blob/master/LICENSE)

```
The MIT License (MIT)

Copyright © CyberAgent, Inc. All Rights Reserved.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

```


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/CyberAgent/boombox.js/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

