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
          class="relative flex-shrink-0 flex flex-col rounded-lg shadow-lg p-6 transition-all duration-500 w-full h-[350px] overflow-hidden"
        >
          <!-- Background Image (Absolute Positioning) -->
          <img
            :src="section.image"
            alt="Section Image"
            class="absolute top-0 left-0 w-full h-full object-cover z-0 opacity-50  rounded-[20px]"
          />
  
          <!-- Text Content (Above Image) -->
          <div class="relative z-10 text-center">
            <h2 class="text-[24px] font-black drop-shadow-lg" :style="{ color: section.textColor }">
              {{ section.title }}
            </h2>
            <p class="text-[18px] mt-2 font-extrabold drop-shadow-lg" :style="{ color: section.textColor }">
              {{ section.description }}
            </p>
            <P class="text-[15px] mt-2 font-bold drop-shadow-lg" :style="{ color: section.textColor }">Click  <a :href="section.link" target="_blank" rel="noopener" class="underline text-blue-500">here</a> to check it out</P>
          </div>
        </div>
      </div>
  
      <!-- Left Button -->
      <button
        class="absolute left-0 top-3/4 transform -translate-y-1/2 bg-gray-300 opacity-[70%] w-[47px] h-[47px] rounded-full flex items-center justify-center shadow-lg z-10"
        @click="scroll('left')"
      >
        ⬅️
      </button>
  
      <!-- Right Button -->
      <button
        class="absolute right-0 top-3/4 transform -translate-y-1/2 bg-gray-300 opacity-[70%] w-[47px] h-[47px] rounded-full flex items-center justify-center shadow-lg z-10"
        @click="scroll('right')"
      >
        ➡️
      </button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from "vue";
  
  // Define Type for Sections
  interface Section {
    title: string;
    description: string;
    image: string;
    textColor: string;
    link: string;
  }
  
  // References
  const scrollContainer = ref<HTMLElement | null>(null);
  const scrollerContainer = ref<HTMLElement | null>(null);
  const isDragging = ref<boolean>(false);
  const startX = ref<number>(0);
  const scrollLeft = ref<number>(0);
  const sectionWidth = ref<number>(0);
  
  // Sections Data
  const sections = ref<Section[]>([
    {
      title: "Study Hug",
      description: "A web app to practice CBT exams for UTME students",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740439198/dkp0pumiplvgfbbet1wx.png",
      textColor: "yellow-400",
      link: "https://studyhug.netlify.app/"
    },
    {
      title: "Track IT",
      description: "Demo financial tracking app built with Chakra UI",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740479250/Screenshot_2025-02-25_112655_qinfjt.png",
      textColor: "black",
      link: "https://tractit.netlify.app/"
    },
    {
      title: "Pay-4-me",
      description: "An informative landing page for a payment app",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740479898/Screenshot_2025-02-25_113740_fgjxqz.png",
      textColor: "black",
      link: "https://pay-4-me.netlify.app/"
    },
    {
      title: "My stock Tracker",
      description: "Displays stock and crypto prices from an API",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740480369/Screenshot_2025-02-25_114540_pcijtd.png",
      textColor: "#FFFFFF",
      link: "https://mystocktrackerr.netlify.app/"
    },
    {
      title: "Wabais",
      description: "A landing page for a branding business",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740480711/Screenshot_2025-02-25_115127_oosifp.png",
      textColor: "#32CD32",
      link: "https://wabais.netlify.app/"
    },
    {
      title: "Nexcent",
      description: "A landing page for a branding business",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740481008/Screenshot_2025-02-25_115623_i3qahh.png",
      textColor: "black",
      link: "https://nexcentbyhonourable.netlify.app/"
    },
    {
      title: "Biccas",
      description: "A landing page for a Virtual assistance business",
      image: "https://res.cloudinary.com/dabihkozn/image/upload/v1740481452/Screenshot_2025-02-25_120140_vpiwyk.png",
      textColor: "black",
      link: " https://biccaspage.netlify.app/"
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
  