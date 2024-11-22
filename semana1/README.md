# Documentação do Desenvolvimento em sala

## Tags gerais do codigos

```
<a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
</a-scene>
```
- `vr-mode-ui="enabled: false":` Disables the VR UI since these are AR-focused applications.

- `arjs="debugUIEnabled:false":` Disables AR.js debug controls, simplifying the interface for the user.


```
<a-marker present="hiro">
    <!-- AR content here -->
</a-marker>
```
- `present="hiro":` Specifies the Hiro marker, a predefined marker pattern in AR.js.


```
<a-entity camera=""></a-entity>
```

- Purpose: Ensures the AR scene interacts with the user's device camera.

## Específicos do codigo

```
<a-marker present="hiro">
    <a-box color="#ff0e0e0e"></a-box>
</a-marker>
```
- `<a-box>:` A basic 3D shape (a cube) rendered on the Hiro marke

- **Purpose:** Demonstrates rendering a simple 3D object with minimal configuration.

```
<a-assets>
    <img id="sete" src="IMAGE_URL" />
</a-assets>
<a-marker present="hiro">
    <a-image width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#sete"></a-image>
</a-marker>
```
- `<a-assets>:` Manages and preloads resources for the scene.
    - `<img>:` Preloads the image asset with an ID for referencing.
- `<a-image>:` Displays the preloaded image on the marker.
    - `width="1" height="1":` Sets the dimensions of the image.
    - `rotation="-90 0 0":` Rotates the image 90 degrees on the X-axis so it's flat on the marker.
    - `position="0 0 0":` Positions the image at the origin of the marker.

- **Purpose:** Introduces asset management and rendering of 2D content (an image) within the AR environment.


```
<a-assets>
    <audio id="som" preload="auto" src="AUDIO_URL"></audio>
    <video id="robo" src="VIDEO_URL"></video>
</a-assets>
<a-marker present="hiro" controlador>
    <a-video width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#robo"></a-video>
    <a-entity sound="src: #som; autoplay:true; loop:true"></a-entity>
</a-marker>
```

- `<a-assets>:` Preloads audio and video resources for the scene.
    - `<audio>:` Loads an audio file and assigns it an ID.
    - `<video>:` Loads a video file and assigns it an ID.
- `<a-video>:` Displays the preloaded video on the marker.
    - Similar transformations to <a-image> (dimensions, rotation, position).
- `<a-entity sound>:` Plays the preloaded audio in a loop when the marker is detected.
    - `autoplay:true; loop:true:` Starts playback automatically and repeats the sound.

```
AFRAME.registerComponent('controlador', {
    init: function() {
        this.toggle = false;
        this.vid = document.querySelector("#robo");
        this.vid.pause();
    },
    tick: function() {
        if (this.el.object3D.visible) {
            if (!this.toggle) {
                this.toggle = true;
                this.vid.play();
            } else {
                this.toggle = false;
                this.vid.pause();
            }
        }
    }
});
```
- **Purpose:** Dynamically toggles video playback based on marker visibility.
- **Integration:** The component is attached to the marker using the controlador attribute.

- **Purpose:** Combines video and sound playback with interactive behavior triggered by the marker.

```
<a-assets>
    <a-asset-item id="shiba" src="3D_MODEL_URL"></a-asset-item>
</a-assets>
<a-marker present="hiro">
    <a-entity gltf-model="#shiba"></a-entity>
</a-marker>
```

- `<a-assets>:` Preloads the 3D model asset.
- `<a-asset-item>:` Loads a GLTF 3D model and assigns it an ID.
- `<a-entity gltf-model>:` Renders the preloaded 3D model on the marker.
- `gltf-model="#shiba":` References the preloaded GLTF model using its ID.
- **Purpose:** Demonstrates rendering 3D content (a GLTF model) on the marker.