<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";

const buttonRef = ref<HTMLElement | null>(null);

onMounted(() => {
  if (buttonRef.value) {
    gsap.to(buttonRef.value, {
      opacity: 0.5, 
      duration: 1,
      repeat: -1,  
      yoyo: true,   
      ease: "power1.inOut", 
    });
  }
});

defineProps({
  label: {
    type: String,
    required: true,
  },
});
const emailAddress = 'omobolaji119@gmail.com';
const subject = 'Hello Omobolaji';
const mailtoLink = `mailto:${emailAddress}?subject=${encodeURIComponent(subject)}`;
</script>
<template>
       <a :href="mailtoLink">
    <button
      ref="buttonRef"
      class="bg-[#3764EA] text-[#10161F] px-[30px] py-[10px] rounded-[25px]"
    >
      {{ label }}
    </button>
  </a>
</template>