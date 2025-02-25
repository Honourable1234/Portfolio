<script setup lang="ts">
import { onMounted, ref } from "vue";
import gsap from "gsap";
import Scroller from "./Scroller.vue";

const textContainer = ref<HTMLElement | null>(null);
const title = ref<HTMLElement | null>(null);
const subtitle = ref<HTMLElement | null>(null);

onMounted(() => {
  gsap.to(textContainer.value, { opacity: 1, duration: 0.5 });

  gsap.from(title.value, {
    opacity: 0,
    y: 50,
    scale: 0.6,
    duration: 3,
    ease: "power4.out",
    delay: 0.3,
  });

  gsap.from(subtitle.value, {
    opacity: 0,
    y: 30,
    duration: 3,
    ease: "power4.out",
    delay: 2,
  });
});
</script>
<template>
    <div className="sm:flex items-center justify-between bg-[#10161F] px-[5%] min-h-[500px] text-[#FEFEFE] pt-[100px] sm:pt-[50px]">
        <div className="w-[100%] sm:w-[500px] border h-[350px]  rounded-[20px]">
        <Scroller />
       </div>
       <div ref="textContainer">
          <h2  ref="title" className="max-w-[750px] text-[30px] md:text-[45px] lg:text-[60px] font-bold px-[5%] leading-[40px] lg:leading-[70px]  pt-[30px]">Here are projects I have worked on</h2>
          <p ref="subtitle" className="text-[14px] sm:text-[16px] px-[5%] pt-[20px] pb-[30px]">🚀 Working with you helps me build experience, and that goes a long way! 💡✨🔥</p>
       </div>
    </div>
</template>