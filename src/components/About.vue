<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
import Profile from "./Profile.vue";

const textContainer = ref<HTMLElement | null>(null);
const title = ref<HTMLElement | null>(null);
const paragraph = ref<HTMLElement | null>(null);

onMounted(() => {
  gsap.to(textContainer.value, { opacity: 1, duration: 0.3 });

  gsap.from(title.value, {
    opacity: 0,
    y: -100,
    duration: 1.2,
    ease: "power3.out",
  });

  gsap.from(paragraph.value, {
    opacity: 0,
    x: -50,
    duration: 1.5,
    ease: "power3.out",
    delay: 0.4, 
    stagger: 0.1,
  });
});
</script>
<template>
    <div className="flex flex-wrap gap-[100px] justify-center items-center bg-gray-900 px-[5%] min-h-[500px] text-[#FEFEFE] py-[70px] sm:py-[30px]">
        <div ref="textContainer" className="max-w-[700px]">
            <h2 ref="title" className="text-[20px] sm:text-[28px] md:text-[34px]">🚀 Hire a Passionate and Problem-Solving Frontend Developer</h2>
            <P ref="paragraph" className="text-[14px] sm:text-[16px] pt-[20px]" >👋 Hi, I’m Ogunsola Omobolaji! <br/> I’m a frontend-focused web developer passionate about building interactive, user-friendly, and high-performance web applications. I am actively looking for opportunities to gain hands-on experience, work with industry experts, and grow into a top-tier web developer. <br/><br/>💡 My Approach to Development? <br/> I always say this wherever I talk about development:<span className="text-[16px] sm:text-[18px] text-yellow-400">"I might not have all the answers off the top of my head, but I know exactly where to look in order to get the work done right."</span> <br/>This mindset drives me to continuously learn, solve real-world problems, and ensure that every project I work on meets the highest quality standards.</P>
        </div>
        <div>
            <Profile /> 
        </div>
    </div>
</template>