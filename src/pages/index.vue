<template>
  <v-main>
    <div class="backlight" :style="{
      transform: `translate3d(${mouseX}px, ${mouseY}px, 0) translate(-50%, -50%)`,
    }"></div>

    <navigation-header />
    <v-app>

      <GeminiChat />

      <hero-section />
      <about-section id="about" />
      <tech-stack-section />
      <project-section id="project" />
      <journey-section id="journey" />
      <contact-section id="contact" />
    </v-app>
  </v-main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import navigationHeader from "@/layouts/header.vue";

const mouseX = ref(0);
const mouseY = ref(0);
let animationFrameId = null;

const handleMouseMove = (e) => {
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId);
  }

  animationFrameId = requestAnimationFrame(() => {
    mouseX.value = e.clientX;
    mouseY.value = e.clientY;
  });
};

onMounted(() => {
  window.addEventListener("mousemove", handleMouseMove, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener("mousemove", handleMouseMove);
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId);
  }
});
</script>

<style scoped>
.backlight {
  pointer-events: none;
  position: fixed;
  width: 1200px;
  height: 1200px;
  border-radius: 50%;
  background: radial-gradient(circle,
      rgba(102, 252, 241, 0.15) 0%,
      rgba(102, 252, 241, 0.05) 40%,
      transparent 70%);
  z-index: 0;
  will-change: transform;
  mix-blend-mode: screen;
}
</style>
