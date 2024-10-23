<script setup>
import BlurredCard from './components/BlurredCard.vue';
import HoverList from './components/HoverList.vue';
import FloatingMenu from './components/FloatingMenu.vue';
</script>

<template>
  <div class="relative flex gap-4 items-center">
    <BlurredCard />
    <BlurredCard />
  </div>

  <!-- <div>
    <HoverList />
  </div> -->

  <div class="fixed bottom-12 right-12">
    <FloatingMenu></FloatingMenu>
  </div>
</template>