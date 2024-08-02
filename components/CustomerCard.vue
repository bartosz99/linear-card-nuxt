<script setup lang="ts">
type Props = {
  imageSource: string;
  imageAlt: string;
};

defineProps<Props>();

const mouseX = ref('0%');
const mouseY = ref('0%');
const opacity = ref(0);

const handleCursorMove = (e: any) => {
  mouseX.value = ((e.offsetX / e.srcElement.offsetWidth) * 100).toFixed(2) + '%';
  mouseY.value = ((e.offsetY / e.srcElement.offsetHeight) * 100).toFixed(2) + '%';
};

const handleHover = () => {
  console.log();
  opacity.value = 1;
};
</script>

<template>
  <div
    class="relative border rounded-3-xl border-slate-900 min-w-80 w-80 rounded-3xl overflow-hidden cursor-pointer onHover"
    :style="{ '--m-x': mouseX, '--m-y': mouseY, '--opacity': opacity }"
    @mousemove="handleCursorMove($event)"
    @mouseenter="opacity = 1"
    @mouseleave="opacity = 0"
  >
    <img class="baseImage" :src="imageSource" :alt="imageAlt" />
    <div class="firstLayer"></div>
  </div>
</template>

<style scoped>
.card {
  /* border-color: #f7f8f8; */
}

.firstLayer {
  --radius: 20px;

  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, var(--opacity));
  transition: background 0.3s;

  mix-blend-mode: soft-light;
  clip-path: inset(0 0 1px 0 round var(--radius));
  opacity: var(--opacity);
  transition-duration: ;
  transition-timing-function: ;
  transition-delay: ;
  transition-behavior: ;
  will-change: background;
  transition-property: opacity, background;
  background: radial-gradient(
    farthest-corner circle at var(--m-x) var(--m-y),
    rgba(255, 255, 255, 0.8) 10%,
    rgba(255, 255, 255, 0.65) 20%,
    rgba(255, 255, 255, 0) 90%
  );
}
</style>
