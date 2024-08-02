<script setup lang="ts">
type Props = {
  imageSource: string;
  imageAlt: string;
};

defineProps<Props>();
</script>

<template>
  <div
    class="border rounded-3-xl border-slate-900 relative min-w-80 w-80 rounded-3xl overflow-hidden"
  >
    <img :src="imageSource" :alt="imageAlt" class="" />
  </div>
</template>

<style scoped>
.card {
  /* border-color: #f7f8f8; */
}
</style>
