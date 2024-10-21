<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  title: {
    type: String,
    default: 'New Design'
  },
  subtitle: {
    type: String,
    default: '2 Hours ago'
  },
  description: {
    type: String,
    default: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sed ducimus nam impedit doloremque, expedita fugiat?'
  },
  imgSrc: {
    type: String,
    default: '../assets/example-img.png'
  }
})
</script>

<template>
  <div
    class="relative group w-[300px] h-[300px] bg-white rounded-3xl shadow-sm transition-all duration-500 hover:h-[420px] overflow-hidden"
  >
    <div class="image-box relative w-full h-[260px] bg-black blur-md group-hover:filter-none transition-all duration-500">
      <!-- image-box::before equivalent -->
      <div class="absolute bottom-[-40px] w-full h-[80px] rounded-3xl bg-white"></div>
      <!-- image-box::after equivalent -->
      <div class="absolute right-0 bottom-[40px] w-[80px] h-[80px] bg-transparent rounded-3xl shadow-[75px_70px_0_40px_rgba(255,255,255,1)]"></div>
      <img src="../assets/example-img.png" alt="Example Image" class="object-cover w-full h-full" />
    </div>
    <div class="relative top-[-20px] z-10 py-0 px-[30px] transition-all duration-500 flex flex-col gap-6">
      <h3 class="text-[1.25em] relative">
        {{ title }} <br>
        <span class="absolute bottom-[-15px] text-[0.65em] opacity-[0.75]">{{ subtitle }}</span>
      </h3>
      <p class="relative opacity-0 transition-all duration-500 group-hover:opacity-100">
        {{ description }}
      </p>
    </div>
  </div>
</template>