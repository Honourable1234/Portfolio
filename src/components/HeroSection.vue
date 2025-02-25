<script setup lang="ts">
import { ref, onMounted, computed } from "vue";
import RollingCube from "./RollingCube.vue";
import gitHub from "../assets/gitHub.svg";

const texts: string[] = [
  "Next.js",
  "Vue.js",
  "React.js",
  "Node.js",
  "TypeScript",
  "JavaScript",
];
const displayedText = ref<string>("");
const textRef = ref<HTMLElement | null>(null);
const currentIndex = ref<number>(0);
const isDeleting = ref<boolean>(false);

const cursorColor = computed<string>(() => {
  const colors: Record<string, string> = {
    "Next.js": "text-blue-500",
    "Vue.js": "text-green-500",
    "React.js": "text-blue-400",
    "Node.js": "text-green-400",
    "TypeScript": "text-blue-600",
    "JavaScript": "text-yellow-400",
  };
  return colors[texts[currentIndex.value]] || "text-blue-500";
});

onMounted(() => {
  let charIndex = 0;

  function typeEffect() {
    let currentText = texts[currentIndex.value];

    if (isDeleting.value) {
      displayedText.value = currentText.substring(0, charIndex--);
    } else {
      displayedText.value = currentText.substring(0, charIndex++);
    }

    let typingSpeed: number = isDeleting.value ? 50 : 100;

    if (!isDeleting.value && charIndex === currentText.length + 1) {
      isDeleting.value = true;
      typingSpeed = 1000; // Pause before deleting
    } else if (isDeleting.value && charIndex === 0) {
      isDeleting.value = false;
      currentIndex.value = (currentIndex.value + 1) % texts.length;
    }

    setTimeout(typeEffect, typingSpeed);
  }

  typeEffect();
});
</script>
<template>
  <div
    class="pt-[200px] pb-[150px] flex items-center md:justify-between justify-center bg-gray-900 text-white px-[5%]"
  >
    <div class="h-[350px] absolute gao-[20px] z-10 md:relative">
      <h1
        class="text-[30px] md:text-[45px] lg:text-[60px] font-bold px-[5%] leading-[40px] lg:leading-[70px]"
      >
        I am proficient in <br />
        <span ref="textRef" :class="['cursor', cursorColor]">
          {{ displayedText }}
        </span>
        <span :class="['cursor', cursorColor]">|</span>
      </h1>
      <p class="text-[14px] sm:text-[16px] px-[5%] pt-[20px]">
        Passionate about building, optimizing, Creating, learning, and pushing
        boundaries
      </p>
         <p class="text-[18px] sm:text-[20px] px-[5%] pt-[20px]">Click<a href="https://github.com/Honourable1234" target="_blank" rel="noopener noreferrer" class="text-blue-400 font-semibold hover:text-blue-600"> here </a>to check out my GitHub!</p>
         <p class="text-[18px] sm:text-[20px] px-[5%] pt-[20px]">Email: Omobolaji119@gmail.com</p>
    </div>
    <div class="w-[300px] h-[300px] sm:w-[400px] sm:h-[400px] flex justify-center items-center"><RollingCube /></div>
  </div>
</template> 
