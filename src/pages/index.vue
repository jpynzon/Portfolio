<template>
  <v-main>
    <div class="backlight" :style="{ transform: `translate3d(${mouseX}px, ${mouseY}px, 0) translate(-50%, -50%)` }" />

    <navigation-header />
    <v-app>
      <GeminiChat />

      <div v-for="(section, index) in sections" :key="index" :id="sectionIds[index]" ref="sectionRefs">
        <component :is="section" />
      </div>
    </v-app>
  </v-main>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

import navigationHeader from "@/layouts/header.vue";

import HeroSection from "@/components/hero-section.vue";
import AboutSection from "@/components/about-section.vue";
import TechStackSection from "@/components/tech-stack-section.vue";
import ProjectSection from "@/components/project-section.vue";
import JourneySection from "@/components/journey-section.vue";
import ContactSection from "@/components/contact-section.vue";

gsap.registerPlugin(ScrollTrigger);

const mouseX = ref(0);
const mouseY = ref(0);
let animationFrameId = null;

const handleMouseMove = (e) => {
  if (animationFrameId) cancelAnimationFrame(animationFrameId);
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
  if (animationFrameId) cancelAnimationFrame(animationFrameId);
});

const sectionRefs = ref([]);
const sections = ref([
  markRaw(HeroSection),
  markRaw(AboutSection),
  markRaw(TechStackSection),
  markRaw(ProjectSection),
  markRaw(JourneySection),
  markRaw(ContactSection),
]);

const sectionIds = ref(["home", "about", "tech-stack", "project", "journey", "contact"]);

onMounted(() => {
  nextTick(() => {
    sectionRefs.value.forEach((section) => {
      gsap.fromTo(
        section,
        { opacity: 0, y: 50 },
        {
          opacity: 1,
          y: 0,
          duration: 1,
          scrollTrigger: {
            trigger: section,
            start: "top 80%",
            toggleActions: "play none none reverse",
          },
        }
      );
    });
  });
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
