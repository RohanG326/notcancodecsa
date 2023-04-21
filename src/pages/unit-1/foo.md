---
title: Test with files
date: '2022-08-15'
summary: 'The first article written to this website to test if my code worked.'
tags: ['test', 'first', 'article']
type: 'page'
due: '2022-09-14'
---

<script>
	import Runnable from '$components/Runnable.svelte';
	import testjava from '$files/test.java?raw';
	import hello from '$files/hello.c?raw';
</script>

# Uses

**Here's some stuff I use**

- SvelteKit
- VS Code
- Emojis 😎

```javascript
let canvas = document.getElementById('ThreeSun');
//Add Renderer
renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });
renderer.setPixelRatio(window.devicePixelRatio);
renderer.setSize(width, height);
//renderer.setClearColor(0x0f172a, 1); // 0x0f172a
renderer.setClearColor(0x00000, 1);

// Add ambience color
let ambient = new THREE.AmbientLight(0x0f172a, 1);
scene.add(ambient);

//add Camera
let camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
camera.position.z = 1 * 1.2;
camera.position.y = -2.5 * 1.2;
camera.position.x = 0.5 * 1.2;

// Add blackhole aura
const auraGeometry = new THREE.SphereGeometry(0.5, 32, 32);
const auraMaterial = new THREE.MeshBasicMaterial({ color: '#535bf2' }); // #535bf2
aura = new THREE.Mesh(auraGeometry, auraMaterial);
aura.renderOrder = -999;
aura.onBeforeRender = function (renderer) {
	renderer.clearDepth();
};
scene.add(aura);
```

<Runnable code={testjava} lang={"java"} title={"swaps.java"}/>

```javascript
let canvas = document.getElementById('ThreeSun');
//Add Renderer
renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });
renderer.setPixelRatio(window.devicePixelRatio);
renderer.setSize(width, height);
//renderer.setClearColor(0x0f172a, 1); // 0x0f172a
renderer.setClearColor(0x00000, 1);

// Add ambience color
let ambient = new THREE.AmbientLight(0x0f172a, 1);
scene.add(ambient);

//add Camera
let camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
camera.position.z = 1 * 1.2;
camera.position.y = -2.5 * 1.2;
camera.position.x = 0.5 * 1.2;

// Add blackhole aura
const auraGeometry = new THREE.SphereGeometry(0.5, 32, 32);
const auraMaterial = new THREE.MeshBasicMaterial({ color: '#535bf2' }); // #535bf2
aura = new THREE.Mesh(auraGeometry, auraMaterial);
aura.renderOrder = -999;
aura.onBeforeRender = function (renderer) {
	renderer.clearDepth();
};
scene.add(aura);
```

```javascript
let canvas = document.getElementById('ThreeSun');
//Add Renderer
renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true, alpha: true });
renderer.setPixelRatio(window.devicePixelRatio);
renderer.setSize(width, height);
//renderer.setClearColor(0x0f172a, 1); // 0x0f172a
renderer.setClearColor(0x00000, 1);

// Add ambience color
let ambient = new THREE.AmbientLight(0x0f172a, 1);
scene.add(ambient);

//add Camera
let camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
camera.position.z = 1 * 1.2;
camera.position.y = -2.5 * 1.2;
camera.position.x = 0.5 * 1.2;

// Add blackhole aura
const auraGeometry = new THREE.SphereGeometry(0.5, 32, 32);
const auraMaterial = new THREE.MeshBasicMaterial({ color: '#535bf2' }); // #535bf2
aura = new THREE.Mesh(auraGeometry, auraMaterial);
aura.renderOrder = -999;
aura.onBeforeRender = function (renderer) {
	renderer.clearDepth();
};
scene.add(aura);
```

```javascript
for (let i = 0; i <= 3; i++) {}
```

<Runnable code={hello} lang={"c"} title={"hello.c"}/>

<Runnable code={testjava} lang={"java"} title={"swaps.java"}/>