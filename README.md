# arToolKit JS Guide
## Used Library
| Library  | Version |
| ------------- | ------------- |
| THREE.OBJLoader2 | 1.3.1  |
| three.min.js (three.js minified version)  | r93  |
| artoolkit.min.js (artoolkit.js minified version)  | [7773318  on 3 Feb 2017](https://github.com/artoolkit/jsartoolkit5/blob/77733182a4c519b8e683cbf246a22920d94f3deb/build/artoolkit.min.js)  |
| artoolkit.three.js | [f17a470  on 3 Jul 2017](https://github.com/artoolkit/jsartoolkit5/blob/f17a470a2c8eb4452c6ed5f0d5ec2c32de96c17f/js/artoolkit.three.js) |

## Inital the library in .html
```html
<script async src="artoolkit.min.js"></script>
<script async src="three.min.js"></script>
<script async src="artoolkit.three.js"></script>
```

## Creacte Object
### Shpere
```javascript
var createShpere = function () {
	var sphere = new THREE.Mesh(
		new THREE.SphereGeometry(0.5, 8, 8),
		new THREE.MeshNormalMaterial()
	);
	sphere.material.shading = THREE.FlatShading;
	sphere.position.z = 0.5;

	return sphere;
}
```
## QR Code
### Add a pattern 5 QR Code
```javascript
arController.setPatternDetectionMode(artoolkit.AR_MATRIX_CODE_DETECTION);
...
var markerRoot = arController.createThreeBarcodeMarker(5);
markerRoot.add(sphere); // Marker represent the sphere
arScene.scene.add(markerRoot);
```
### Add .patt QR Code (patt.hiro)
```javascript
arController.loadMarker('Data/patt.hiro', function(markerId) {
  var markerRoot = arController.createThreeMarker(markerId);
  markerRoot.add(sphere);
  arScene.scene.add(markerRoot);
  });
```
[Online marker generate tool](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)
### Set the mode, for better detection of the QR code
#### pattern QR code
```javascript
arController.setPatternDetectionMode(artoolkit.AR_MATRIX_CODE_DETECTION);
```
#### .patt QR code
```javascript
arController.setPatternDetectionMode(artoolkit.AR_TEMPLATE_MATCHING_MONO_AND_MATRIX);
```

## Under findObjectUnderEvent class
### For single object, use intersectObject(objects)
```javascript
var intersects = raycaster.intersectObject(objects);
```
### For mult. object, use intersectObjects(objects)
```javascript
var intersects = raycaster.intersectObjects(objects.children, true);
```
