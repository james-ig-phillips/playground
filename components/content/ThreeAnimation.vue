<template>
  <div>
    <canvas class="aspect-[4/3] !h-auto !w-full rounded-xl" ref="canvas" />
  </div>
</template>

<script setup>
import * as THREE from "three";
import { gsap } from "gsap";

const canvas = ref(null);

// Scene
const scene = new THREE.Scene();

// Red Cube
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);

// Sizes
const sizes = {
  width: 800,
  height: 600,
};

// Camera
const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height);
camera.position.z = 3;
scene.add(camera);

onMounted(() => {
  // Renderer
  const renderer = new THREE.WebGLRenderer({
    canvas: canvas.value,
  });

  renderer.setSize(sizes.width, sizes.height);

  // Clock
  // const clock = new THREE.Clock();

  gsap.to(mesh.position, { duration: 1, delay: 1, x: 2 });
  gsap.to(mesh.position, { duration: 1, delay: 2, x: 0 });

  //Animations
  const tick = () => {
    // Clock
    // const elapsedTime = clock.getElapsedTime();

    // // Update objects
    // camera.position.x = Math.sin(elapsedTime);
    // camera.position.y = Math.cos(elapsedTime);
    // camera.lookAt(mesh.position);

    // Render
    renderer.render(scene, camera);

    window.requestAnimationFrame(tick);
  };

  tick();
});
</script>
