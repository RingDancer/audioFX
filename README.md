# audioFX [![GitHub version](https://badge.fury.io/gh/madebywild%2FaudioFX.svg)](http://badge.fury.io/gh/madebywild%2FaudioFX)

High-Level Audio Effects using the Web Audio API in JavaScript, ~1-2 KB gzipped.

Currently only a lowpass-filter is available and things are very **alpha** as there is not a single test yet. API **will** change in the future. Currently 91% test coverage in latest Chrome, FF and Safari.

[Demo](http://madebywild.github.io/audioFX/)

## Installation

### CDN

Waiting for approval.
``<script src="//cdn.jsdelivr.net/audiofx/latest/audioFX.min.js"></script>``

### Bower [![Bower version](https://badge.fury.io/bo/AudioFX.svg)](http://badge.fury.io/bo/AudioFX)

``bower install AudioFX``

### NPM [![npm version](https://badge.fury.io/js/audiofx.svg)](http://badge.fury.io/js/audiofx)

``npm install audiofx``

## Usage Instructions

*Note:* **AudioFX** should be called after the window has loaded to ensure we have access to the Audio Context of the Browser.

### new AudioFX(url, [callback], [options])

Creates a new AudioFX instance that represents one loaded Audio file. If you store it in a variable for later use, make sure to ``null`` the variable so it's fully eligible to garbage collection.
 
- ``url`` {string} - A URL where to load the file from.
- ``callback`` {function} - A function that gets called once the buffer has been loaded and we are ready for playback. *optional*
- ``options`` {object} - Custom options on instance level. *optional*

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    // do something
}, {
    loop: true
});
```

### play()

Plays the ``AudioFX`` instance from the beginning and re-evaluates the options of the instance before playing (in case they were changed in the meantime).
You can only play an instance once its file has been loaded, so its the best to use inside the constructor callback function.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    this.play();
});
```

### stop()

Stops the ``AudioFX`` instance immediately.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    this.play();
    setTimeout(function(){
      TestAudio.stop();
    },1000);
});
```

### toggle()

Toggles the play/stop state of the ``AudioFX`` instance.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    document.addEventListener('mousedown', function(){
      TestAudio.toggle();
    });
});
```

### changeVolume(volume)

- ``volume`` {number} - the new volume to set (supply a fraction like 0.5 between 0 and 1)

You can also use ``volume()`` which is simply syntactic sugar for the ``changeVolume()`` function.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    this.play();
    TestAudio.changeVolume(0.8);
});
```

### changeFilter(frequency, quality)

- ``frequency`` {number} - the frequency of when the filter cuts off (supply a fraction like 0.5 between 0 and 1) for more info see http://en.wikipedia.org/wiki/Low-pass_filter
- ``quality`` {number} - the quality of the filter (supply a fraction like 0.5 between 0 and 1) for more info see: http://en.wikipedia.org/wiki/Q_factor

You can also use ``filter()`` which is simply syntactic sugar for the ``changeFilter()`` function.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    this.play();
    document.addEventListener('mousemove', function(e){
      var f = e.pageX / window.innerWidth;
      var q = e.pageY / window.innerHeight;
      TestAudio.changeFilter(f,q);
    });
}, {loop:true});
```

### destroy()

Stops and destroys the ``AudioFX`` instance, be sure to ``null`` the variable/references to completely get rid of it in the memory.

You can also use ``remove()`` and ``kill()`` which is simply syntactic sugar for the ``destroy()`` function.

Example:
```javascript
var TestAudio = new AudioFX("test.mp3", function(){
    this.play();
    setTimeout(function(){
      TestAudio.destroy();
    },1000);
});
```

## Dependencies

**None!** Drop it in as you please.

## Compatibility

It uses ``UMD`` and therefore is compatible with ``AMD``, ``CommonJS`` and returns a global ``AudioFX``.
This is the list of browsers that support the Web Audio API, that means it should work there, albeit not every version has been tested. Test reports are very welcome!

- Chrome 14+
- Firefox 23+
- Opera 15
- Safari 6
- **No Internet Explorer!**

## Roadmap

- [ ] currentTime
- [ ] hasLoaded
- [ ] real pause / no stop in toggle
- [ ] HTML5 Audio Player fallback so there is progressive enhancement (sound playing, but no FX)
- [ ] autoplay option
- [ ] all Filter types (highpass etc.)
- [ ] Global Volume Change across all audioFX instances
- [ ] Fade In / Fade Out (non-linear)
- [ ] Reverb (Convolver)

## License

(The MIT License)

Copyright (c) 2015 Thomas Strobl @tom2strobl tom@wild.as

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.