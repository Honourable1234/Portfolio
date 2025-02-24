<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
import gitHub from "../assets/gitHub.svg";

const cubeRef = ref<HTMLElement | null>(null);

onMounted(() => {
  if (cubeRef.value) {
    gsap.to(cubeRef.value, {
      rotationY: 360,
      duration: 3,
      repeat: -1, // Infinite loop
      ease: "linear",
    });
  }
});
</script>

<template>
  <div class="h-screen flex items-center justify-center bg-gray-900 opacity-20 sm:opacity-50">
    <div ref="cubeRef" class="cube">
      <div class="face front bg-blue-500 flex items-center justify-center">
      Next.Js <img alt="Vue logo" src="../assets/NextLogo.svg" width="50" height="50" />
      </div>
      <div class="face back bg-green-500 flex items-center justify-center">
      Vue.js <img alt="Vue logo" src="../assets/VueLogo.svg" width="50" height="50" />
      </div>
      <div class="face left bg-cyan-500 flex items-center justify-center">
      React.js <img alt="Vue logo" src="../assets/ReactLogo.svg" width="50" height="50" />
      </div>
      <div class="face right bg-yellow-500 flex items-center justify-center">
      Node.js <img alt="Vue logo" src="../assets/NodeLogo.svg" width="50" height="50" />
      </div>
      <div class="face top bg-purple-500 flex items-center justify-center">
      TypeScript <img alt="Vue logo" src="../assets/TypeScript.svg" width="50" height="50" />
      </div>
      <div class="face bottom bg-orange-500 flex items-center justify-center">
      JavaScript <img alt="Vue logo" src="../assets/JavaScript.svg" width="50" height="50" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.cube {
  width: 300px; 
  height: 300px;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(-30deg);
}

.face {
  position: absolute;
  width: 300px; 
  height: 300px;
  border: 4px solid white;
  text-align: center;
  line-height: 300px;
  font-size: 28px; 
  font-weight: bold;
  color: white;
}

/* Positioning faces (Adjusted Translation to Match 300px Size) */
.front  { transform: translateZ(150px); }  /* Adjusted from 200px */
.back   { transform: rotateY(180deg) translateZ(150px); }
.left   { transform: rotateY(-90deg) translateZ(150px); }
.right  { transform: rotateY(90deg) translateZ(150px); }
.top    { transform: rotateX(90deg) translateZ(150px); }
.bottom { transform: rotateX(-90deg) translateZ(150px); }
</style>
