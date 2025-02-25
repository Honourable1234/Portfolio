<template>
    <div ref="scrollerContainer" class="relative bg-gray-100  rounded-[20px]">
      <!-- Scrollable Container -->
      <div
        ref="scrollContainer"
        class="overflow-hidden flex transition-all duration-500 ease-in-out relative"
        @mousedown="startDrag"
        @mousemove="drag"
        @mouseup="stopDrag"
        @mouseleave="stopDrag"
      >
        <!-- Dynamic Sections -->
        <div
          v-for="(section, index) in sections"
          :key="index"
          class="relative flex-shrink-0 flex flex-col items-center justify-center rounded-lg shadow-lg p-6 transition-all duration-500 w-full h-[350px] overflow-hidden"
        >
          <!-- Background Image (Absolute Positioning) -->
          <img
            :src="section.image"
            alt="Section Image"
            class="absolute top-0 left-0 w-full h-full object-cover z-0  rounded-[20px]"
          />
  
          <!-- Text Content (Above Image) -->
          <div class="relative z-10 text-left py-[20px]">
            <h2 class="text-3xl font-bold" :style="{ color: section.textColor }">
              {{ section.title }}
            </h2>
            <p class="text-lg mt-2" :style="{ color: section.textColor }">
              {{ section.description }}
            </p>
            <P class="text-[15px] mt-2" :style="{ color: section.textColor }">Check out this project at <a>{{ section.link }}</a></P>
          </div>
        </div>
      </div>
  
      <!-- Left Button -->
      <button
        class="absolute left-0 top-1/2 transform -translate-y-1/2 bg-gray-300 opacity-[40%] w-[47px] h-[47px] rounded-full flex items-center justify-center shadow-lg z-10"
        @click="scroll('left')"
      >
        ⬅️
      </button>
  
      <!-- Right Button -->
      <button
        class="absolute right-0 top-1/2 transform -translate-y-1/2 bg-gray-300 opacity-[40%] w-[47px] h-[47px] rounded-full flex items-center justify-center shadow-lg z-10"
        @click="scroll('right')"
      >
        ➡️
      </button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from "vue";
  import gitHubLogo from "@/assets/gitHub.svg"
  
  // Define Type for Sections
  interface Section {
    title: string;
    description: string;
    image: string;
    textColor: string;
  }
  
  // References
  const scrollContainer = ref<HTMLElement | null>(null);
  const scrollerContainer = ref<HTMLElement | null>(null);
  const isDragging = ref<boolean>(false);
  const startX = ref<number>(0);
  const scrollLeft = ref<number>(0);
  const sectionWidth = ref<number>(0);
  
  // Sections Data
  const sections = ref<section[]>([
    {
      title: "Vue.js",
      description: "A progressive JavaScript framework for building UI.",
      image: "https://imgur.com/a/nXr7tCV.jpg",
      textColor: "#FFFFFF",
      link: ""
    },
    {
      title: "React.js",
      description: "A library for building user interfaces with components.",
      image: "/images/react-bg.jpg",
      textColor: "#FFDD00",
    },
    {
      title: "Angular",
      description: "A powerful framework for building enterprise-grade apps.",
      image: "/images/angular-bg.jpg",
      textColor: "#FF5733",
    },
  ]);
  
  // Update section width on window resize
  const updateSectionWidth = () => {
    if (scrollerContainer.value) {
      sectionWidth.value = scrollerContainer.value.clientWidth;
    }
  };
  
  // Scroll Function
  const scroll = (direction: "left" | "right") => {
    if (scrollContainer.value) {
      scrollContainer.value.scrollLeft += direction === "left" ? -sectionWidth.value : sectionWidth.value;
    }
  };
  
  // Start Dragging
  const startDrag = (event: MouseEvent) => {
    if (!scrollContainer.value) return;
    isDragging.value = true;
    startX.value = event.pageX - scrollContainer.value.offsetLeft;
    scrollLeft.value = scrollContainer.value.scrollLeft;
  };
  
  // Dragging Motion
  const drag = (event: MouseEvent) => {
    if (!isDragging.value || !scrollContainer.value) return;
    event.preventDefault();
    const x = event.pageX - scrollContainer.value.offsetLeft;
    const walk = (x - startX.value) * 2; // Adjust speed
    scrollContainer.value.scrollLeft = scrollLeft.value - walk;
  };
  
  // Stop Dragging
  const stopDrag = () => {
    isDragging.value = false;
  };
  
  // Set section width on mount & listen for resize
  onMounted(() => {
    updateSectionWidth();
    window.addEventListener("resize", updateSectionWidth);
  });
  
  onUnmounted(() => {
    window.removeEventListener("resize", updateSectionWidth);
  });
  </script>
  
  <style scoped>
  /* Enables Smooth Scrolling */
  .overflow-hidden {
    scroll-behavior: smooth;
    white-space: nowrap;
  }
  </style>
  