<script setup lang="ts">
type Props = {
  imageSource: string;
  imageAlt: string;
};

defineProps<Props>();

const mouseX = ref('0%');
const mouseY = ref('0%');
const backgroundX = ref('50%');
const backgroundY = ref('50%');

const opacity = ref(0);

const handleCursorMove = (e: any) => {
  const mouseXPercent = (e.offsetX / e.srcElement.offsetWidth) * 100;
  const mouseYPercent = (e.offsetY / e.srcElement.offsetHeight) * 100;

  const backgroundXPercent = 50 + (mouseXPercent / 100) * 20;
  const backgroundYPercent = 50 + (mouseYPercent / 100) * 20;

  mouseX.value = mouseXPercent.toFixed(2) + '%';
  mouseY.value = mouseYPercent.toFixed(2) + '%';

  backgroundX.value = backgroundXPercent.toFixed(2) + '%';
  backgroundY.value = backgroundYPercent.toFixed(2) + '%';
};
</script>

<template>
  <div
    class="card relative border border-slate-900 min-w-80 w-80 overflow-hidden cursor-pointer onHover"
    :style="{
      '--m-x': mouseX,
      '--m-y': mouseY,
      '--bg-x': backgroundX,
      '--bg-y': backgroundY,
      '--opacity': opacity
    }"
    @mousemove="handleCursorMove($event)"
    @mouseenter="opacity = 0.6"
    @mouseleave="opacity = 0"
  >
    <div class="parent">
      <div>
        <img class="baseImage" :src="imageSource" :alt="imageAlt" />
      </div>
      <div class="firstLayer" />
      <div class="secondLayer" />
    </div>
  </div>
</template>

<style scoped>
.card {
  border-radius: 48px;
}

.parent {
  display: grid;
  will-change: transform;
  transform-origin: center center;
  transition-duration: ;
  transition-timing-function: ;
  transition-delay: ;
  transition-behavior: ;
  transition-property: transform;
  transform: rotateY(var(--r-x)) rotateX(var(--r-y));
  border-radius: var(--radius);
  border: 1px solid var(--color-border-primary);
}

.parent > * {
  width: 100%;
  height: 100%;
  display: grid;
  grid-area: 1 / 1;
  clip-path: inset(0 0 0 0 round var(--radius));
}

.firstLayer {
  --radius: 20px;

  mix-blend-mode: soft-light;
  clip-path: inset(0 0 1px 0 round var(--radius));
  opacity: var(--opacity);
  will-change: background;
  transition-property: opacity, background;
  background: radial-gradient(
    farthest-corner circle at var(--m-x) var(--m-y),
    rgba(255, 255, 255, 0.8) 10%,
    rgba(255, 255, 255, 0.65) 20%,
    rgba(255, 255, 255, 0) 90%
  );
}

.secondLayer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, var(--opacity));
  transition: background 0.3s;
  mix-blend-mode: color-dodge;
  opacity: var(--opacity);
  will-change: background;
  transition-duration: ;
  transition-timing-function: ;
  transition-delay: ;
  transition-behavior: ;
  transition-property: opacity;
  clip-path: inset(0 0 1px 0 round var(--radius));
  --foil-svg: url(../assets/images/card_backround_image.svg);
  --step: 5%;
  --pattern: var(--foil-svg) center/100% no-repeat;
  --rainbow: repeating-linear-gradient(
      0deg,
      rgb(255, 119, 115) calc(var(--step) * 1),
      rgba(255, 237, 95, 1) calc(var(--step) * 2),
      rgba(168, 255, 95, 1) calc(var(--step) * 3),
      rgba(131, 255, 247, 1) calc(var(--step) * 4),
      rgba(120, 148, 255, 1) calc(var(--step) * 5),
      rgb(216, 117, 255) calc(var(--step) * 6),
      rgb(255, 119, 115) calc(var(--step) * 7)
    )
    0% var(--bg-y) / 200% 700% no-repeat;
  --diagonal: repeating-linear-gradient(
      128deg,
      #0e152e 0%,
      hsl(180, 10%, 60%) 3.8%,
      hsl(180, 10%, 60%) 4.5%,
      hsl(180, 10%, 60%) 5.2%,
      #0e152e 10%,
      #0e152e 12%
    )
    var(--bg-x) var(--bg-y) / 300% no-repeat;
  --shade: radial-gradient(
      farthest-corner circle at var(--m-x) var(--m-y),
      rgba(255, 255, 255, 0.1) 12%,
      rgba(255, 255, 255, 0.15) 20%,
      rgba(255, 255, 255, 0.25) 120%
    )
    var(--bg-x) var(--bg-y) / 300% no-repeat;
  background-blend-mode: hue, hue, hue, overlay;
  background: var(--pattern), var(--rainbow), var(--diagonal), var(--shade);
  /* background: var(--pattern); */
}

.secondLayer::after {
  content: '';
  mix-blend-mode: exclusion;
  background-blend-mode: soft-light, hue, hard-light;
  grid-area: inherit;
  background: inherit;

  background-position: center, 0% var(--bg-y), calc(var(--bg-x) * -1) calc(var(--bg-y) * -1),
    var(--bg-x) var(--bg-y);
}
</style>
