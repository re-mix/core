# progressive-video-player core
A custom element that wraps HTMLVideoElement API

## Usage
### Load modules
The player consists of a core and plugin modules. For the core module to work, at least a video and skin plugins are necessary.
```html
<!-- Player core -->
<script type="module" src="player-core.mjs"></script>
<script nomodule src="player-core.js"></script>
<!-- Default skin plugin -->
<script type="module" src="skin-plugin-default.mjs"></script>
<script nomodule src="skin-plugin-default.js"></script>
<!-- HLS video plugin -->
<script type="module" src="video-plugin-hls.mjs"></script>
<script nomodule src="video-plugin-hls.js"></script>
<!-- Default ad plugin -->
<script type="module" src="ad-plugin-default.mjs"></script>
<script nomodule src="ad-plugin-default.js"></script>
```

### Declare elements
Once the modules are loaded, custom elements are ready to use.
```html
<progressive-video-player src="https://my-video.com/xxx.m3u8">
  <video-plugin-hls></video-plugin-hls>
  <skin-plugin-defalut language="ja"></skin-plugin-default>
  <ad-plugin-default>
    <ad-break href="https://my-ad.com/vast" position="pre"></ad-break>
    <ad-break href="https://my-ad.com/vpaid" position="120"></ad-break>
    <ad-break href="https://my-ad.com/vast" position="post"></ad-break>
  </ad-plugin-default>
</progressive-video-player>
```

### Property access / event handling
```js
// As video-player does not inherit from HTMLVideoElement,
// any property access (other than `src`) should be done through `elem` property
const video = document.querySelector('progressive-video-player');
console.log(`${video.elem.currentTime} / ${video.elem.duration}`);
video.elem.addEventListener('canplay', handler, false);
```

## API

### Element Name
`<progressive-video-player>`

### Supported Attributes
| Name       | Value                                                                                |
| ---------- | ------------------------------------------------------------------------------------ |
| src        | URL of the video (video file itself or a manifest file)                              |

### Children
A child must be either of the following elements (`source` and `track` elements will be ignored.)
* Custom video plugins, e.g. [`video-plugin-hls`](https://github.com/progressive-video-player/skin-plugin-default)
* Custom skin plugins, e.g. [`skin-plugin-default`](https://github.com/progressive-video-player/skin-plugin-default)
* Custom ad plugins, e.g. `ad-plugin-default`
```
