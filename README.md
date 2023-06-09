# Youtube Ambilight Effect

#### Overview

<p> This is a youtube ambilight effect script. it consists of a video selection interface and a custom video player. The user is presented with a series of video thumbnails and can select any video to play. </p>

#### Structure

The project is structured around two main pages:

1. index.html: This page displays the video selection interface with thumbnails.
2. player.html: This page displays the video player.

The project also includes a JavaScript file player.js, which controls the video playback and the creation of a "Ambilight" effect.

## Code Flow

The `index.html` page contains a series of video thumbnails presented as clickable cards. Each card includes a thumbnail image, which is associated with a particular video file.

The code uses CSS classes for styling and links to a stylesheet `index.css`.

```html
<!-- index.html code snippet -->
<div class="card_ct">
    <a href="/player?video=Video%201" class="video-card">
        <img src="/static/media/pictures/Thumbnail_1.jpg" alt="Video 1 Thumbnail">
        <p>Video 1</p>
    </a>
    <!-- Add more video cards -->
</div>
```

The thumbnails link to the `player.html` page, with the chosen video file passed as a URL parameter.

The `player.html` page is responsible for playing the chosen video.

```html
<!-- player.html code snippet -->
<video id="video-player" width="1024" height="628" data-src="{{ video_path }}" controls type="video/mp4" autoplay></video>
<canvas id="background-canvas"></canvas>

```

The `video-player` element is a standard HTML video player, which accepts a data-src attribute holding the path to the video file. The background-canvas element is used to generate the Ambilight effect.

`player.js` handles the video player controls and the Ambilight effect. The script uses the `<canvas>` element to create a "Ambilight" effect which is updated for each frame of the video.

```javascript
// player.js code snippet
backgroundCanvas.width = video.width * 2;
backgroundCanvas.height = video.height * 2;
...
function updateAmbilight() {
    ...
    ctx.drawImage(video, video.width * 0.5, video.height * 0.5, video.width, video.height);
    ...
}
...
requestAnimationFrame(updateAmbilight);

```

In `getVideoSrc()`, the video file path is retrieved from the data-src attribute of the `video-player` element.

```javascript
// player.js code snippet
function getVideoSrc() {
    return video.getAttribute('data-src');
}
video.src = getVideoSrc();
```

## Styling

The styling for the project is provided through the index.css and player.css files (not provided in the code samples). You should refer to these files for the CSS rules applied to the HTML elements in the project.

#### Notes

This code assumes the video file path is correctly encoded in the `data-src` attribute. The path should be properly set on the server-side before rendering the `player.html` page.
