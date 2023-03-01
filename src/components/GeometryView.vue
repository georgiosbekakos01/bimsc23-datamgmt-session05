<template>
  <div id="viewport" class="flex flex-col p-5">
    <div id="threejs-container" class="py-5"></div>
  </div>
</template>

<script setup>
// Imports;
import { onMounted, onUpdated } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

// Property coming from parent component
const props = defineProps(['radius', 'widthSegments', 'heightSegments', 'phiStart', 'phiLength', 'thetaStart', 'thetaLength', 'meshBoolean']);



// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 700;
let height = 700;

function init() {
  // renderer
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(width, height);
  renderer.setPixelRatio(window.devicePixelRatio);
  document.getElementById("threejs-container").appendChild(renderer.domElement);

  // camera
  camera = new THREE.PerspectiveCamera(25, width / height, 0.1, 1000);
  camera.position.set(10, 50, 70);

  // scene
  scene = new THREE.Scene();
  scene.background = new THREE.Color("#000000");
  
  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  // add fun shape
  createSphere();
  animate();
}

// for controls update
function animate() {
  
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);


}

function createSphere(radius, widthSegments, heightSegments, phiStart, phiLength, thetaStart, thetaLength) {
  geometry = new THREE.SphereGeometry(radius, widthSegments, heightSegments, phiStart, phiLength,thetaStart, thetaLength);
  const material = new THREE.MeshStandardMaterial({wireframe: props.meshBoolean, color: 0xff0000, // red color
    metalness: 0.0, // low metalness
    roughness: 3.0, // low roughness 
    emissive: 0x330000
  });
  const Sphere = new THREE.Mesh(geometry, material);
  scene.add(Sphere);


      // Add lights to the scene
      const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
    scene.add(ambientLight);

    const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
    directionalLight.position.set(1, 1, 1);
    scene.add(directionalLight);
}

function onSliderChange() {
  scene.clear();
  //createBox(props.size1, props.size2, props.size3);
  createSphere(props.radius, props.widthSegments, props.heightSegments, props.phiStart, props.phiLength, props.phiStart, props.thetaStart, props.thetaLength);
}


// This function runs at the beginning of the component lifecycle.
// More about Vue lifecycles: https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram
onMounted(() => {
  init();
  animate();
});

// This function runs when DOM updates.
onUpdated(() => {
  // text content should be the same as current `count.value`
  onSliderChange();

});

</script>
