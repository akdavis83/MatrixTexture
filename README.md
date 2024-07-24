# Matrix Texture
===================

Matrix Texture is a [threex game extension for three.js](http://www.threejsgames.com/extensions/).
It provides help to handle videos in texture.
It is possible to put html5 ```<video>``` output in texture with ```threex.videotexture.js```.
You can even put the webcam in a texture with ```threex.webcamtexture.js```.
It is cool if you want to make a TV screen in your game, You can easily use this extension. You pick the video to play and you are ready to go. 
The screen surface will use your video texture making it look like a TV set.
If you need it, you can try ```threex.audiovideotexture.js``` where the
video is mapped on the texture and the sound of the video
is handled via 
[web audio API](https://dvcs.w3.org/hg/audio/raw-file/tip/webaudio/specification.html).
Thus you can have localized sound, which is neat in the 3d environment.

Take A Look
===============
* Here is an example: https://akdavis83.github.io/MatrixTexture/
It reads the video from a file via video DOM element and displays it in a texture



How To Install
==============

You can install this manually. Type:

```html
<script src='threex.videotexture.js'></script>
```

You can install with [bower](http://bower.io/).

```bash
bower install threex.videotexture
```

then you add that in your html

```html
<script src="bower_components/threex.videotexture/threex.videotexture.js"></script>
```

How To Use it
=============

## threex.videotexture.js

First, you instantiate the texture itself:

```JAVASCRIPT
// create the videoTexture
var videoTexture= new THREEx.VideoTexture('videos/sintel.ogv')
updateFcts.push(function(delta, now){
	// to update the texture are every frame
	videoTexture.update(delta, now)
})
```

Then you use it in a mesh like this.
	
```JS
// use the texture in a THREE.Mesh
var geometry	= new THREE.CubeGeometry(1,1,1);
var material	= new THREE.MeshBasicMaterial({
	map	: videoTexture.texture
});
var mesh	= new THREE.Mesh( geometry, material );
scene.add( mesh );
```

Here is the detailled API:

* ```videoTexture.video```: the video dom element from which the video is used
* ```videoTexture.texture```: the generated ```THREE.Texture``` 
* ```videoTexture.update(delta, now)```: update the texture from the video element
* ```videoTexture.destroy()```: destroy the object

## threex.webcamtexture.js

It will read the webcam using
[getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/Navigator.getUserMedia).
The browser will likely ask for permission.
Let's see how to use it. You instantiate the texture itself.

```JS
var webcamTexture	= new THREEx.WebcamTexture()
updateFcts.push(function(delta, now){
	// to update the texture are every frame
	webcamTexture.update(delta, now)
})
```

Then you use it in a mesh

	
```javascript
// use the texture in a THREE.Mesh
var geometry	= new THREE.CubeGeometry(1,1,1);
var material	= new THREE.MeshBasicMaterial({
	map	: videoTexture.texture
});
var mesh	= new THREE.Mesh( geometry, material );
scene.add( mesh );
```

Here is the detailled API:

* ```videoTexture.video```: the video dom element from which the video is used
* ```videoTexture.texture```: the generated ```THREE.Texture``` 
* ```videoTexture.update(delta, now)```: update the texture from the video element
* ```videoTexture.destroy()```: destroy the object
* ```THREEx.WebcamTexture.available```: true if ```getUserMedia``` is available on this
browser, false otherwise.
