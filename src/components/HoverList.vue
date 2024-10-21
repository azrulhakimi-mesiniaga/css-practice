<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const hoveredIndex = ref(null);
const clicked = ref(false);
let keyDownInterval = null;

const hoverList = index => {
  hoveredIndex.value = index;
}

const handleClick = index => {
  console.log(index);
  clicked.value = !clicked.value;
}

const handleKeyDown = event => {
  if (event.key === 'ArrowUp' || event.key === 'ArrowDown') {
    event.preventDefault();
    if (!keyDownInterval) {
      keyDownInterval = setInterval(() => {
        const newIndex = hoveredIndex.value === null 
          ? 1 
          : (hoveredIndex.value + (event.key === 'ArrowUp' ? -1 : 1) + 8) % 8 || 8; // Wrap around logic
        hoverList(newIndex);
      }, 100); // Adjust the interval as needed
    }
  }
}

const handleKeyUp = () => {
  clearInterval(keyDownInterval);
  keyDownInterval = null;
}

onMounted(() => {
  window.addEventListener('keydown', handleKeyDown);
  window.addEventListener('keyup', handleKeyUp);
});

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeyDown);
  window.removeEventListener('keyup', handleKeyUp);
});
</script>

<template>
  <div class="container flex flex-col justify-center items-center gap-4">
    <button
      class="relative w-[250px] h-[50px] bg-blue-800 rounded-lg transition-all duration-500 outline-none"
      v-for="n in 8"
      :key="n"
      :class="{
        'scale-[1.75] z-[10000] !bg-blue-700': hoveredIndex === n,
        'scale-[1.5] z-[3] !bg-blue-600': hoveredIndex === n + 1 || hoveredIndex === n - 1,
        'scale-[1.25] z-[2] !bg-blue-500': hoveredIndex === n + 2 || hoveredIndex === n - 2,
      }"
      @mouseover="hoverList(n)"
      @mouseleave="hoverList(null)"
      @focus="hoverList(n)"
      @blur="hoverList(null)"
      @click="handleClick(n)"
      tabindex="0"
    ></button>
  </div>
</template>