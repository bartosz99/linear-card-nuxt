<script setup lang="ts">
import { customerCards } from '../contants/index';
</script>

<template>
  <div class="landing flex items-center justify-center px-8 py-16 lg:px-32 bg-black">
    <div
      class="grid grid-cols-1 gap-y-6 gap-x-6 justify-items-center max-w-5xl md:flex-grow md:grid-cols-2 xl:grid-cols-3"
    >
      <CustomerCard
        v-for="card in customerCards"
        :key="card.id"
        :imageSource="card.src"
        :imageAlt="card.alt"
      />
    </div>
  </div>
</template>

<style scoped>
.landing {
  background-color: #000212;
}
</style>
