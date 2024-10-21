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
  <div
    class="h-16 w-16 bg-red-500 rounded-full relative"
    @mouseover="showMenu = true"
    @mouseleave="showMenu = false"
  >
    <div class="absolute top-[-300px] flex flex-col gap-2">
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
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.menus-enter-from, .menus-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.menus-enter-to, .menus-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>