<script setup>
import { ref, watch } from 'vue';

const showMenu = ref(false);
const circles = ref([]);

watch(showMenu, (newValue) => {
  if (newValue) {
    circles.value = Array.from({ length: 4 }, (_, index) => index);
  } else {
    circles.value = [];
  }
});
</script>

<template>
  <div class="relative">
    <div
      class="h-16 w-16 bg-red-500 rounded-full cursor-pointer shadow-md hover:shadow-lg hover:scale-105 transition-all duration-300 flex justify-center items-center"
      @click="showMenu = !showMenu"
    >
      <transition name="icon" mode="out-in">
        <div v-if="showMenu" key="close">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </div>
        <div v-else key="settings">
          <img src="../assets/settings.svg" alt="">
        </div>
      </transition>
    </div>
    <div class="absolute top-[-300px] flex flex-col gap-2 hover:scale-100">
      <transition-group name="menus">
        <div
          v-for="index in circles"
          :key="index"
          class="h-16 w-16 bg-green-500 rounded-full"
          :style="{ transitionDelay: `${(3 - index) * 40}ms` }"
        ></div>
      </transition-group>
    </div>
  </div>
</template>

<style scoped>
.menus-enter-active, .menus-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.menus-enter-from, .menus-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.menus-enter-to, .menus-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.icon-enter-active, .icon-leave-active {
  transition: opacity 0.2s ease-in-out, transform 0.2s ease-in-out;
}

.icon-enter-from, .icon-leave-to {
  opacity: 0;
  transform: translateX(10px);
}
</style>