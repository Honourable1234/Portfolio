<script setup lang="ts">
import Button from "./Button.vue";
</script>
<template>
  <div className="fixed w-[100%] flex bg-[#10161F] py-[20px] items-center justify-between px-[5%] z-50">
     <p className="text-[20px] sm:text-[30px] text-[#FFFF]">Honourable</p>
     <div className="hidden md:flex gap-[40px] text-[#FEFEFE]">
       <p className="hover:text-[#3764EA]">Works</p>
       <p className="hover:text-[#3764EA]">Contact</p>
       <p className="hover:text-[#3764EA]">About</p>
     </div>
     <div>
       <Button label="Email Me"/>
     </div>
  </div>
</template>