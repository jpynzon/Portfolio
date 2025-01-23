<template>
  <div ref="animationContainer" :style="customStyle"></div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import lottie from "lottie-web";

const props = defineProps({
  animationData: Object,
  autoplay: {
    type: Boolean,
    default: true,
  },
  loop: {
    type: Boolean,
    default: true,
  },
  customStyle: {
    type: String,
  },
});

const animationContainer = ref(null);
let animationInstance = null;

onMounted(() => {
  animationInstance = lottie.loadAnimation({
    container: animationContainer.value,
    animationData: props.animationData,
    renderer: "svg",
    autoplay: props.autoplay,
  });
});

watch(
  () => props.animationData,
  (newAnimationData) => {
    if (animationInstance) {
      animationInstance.stop();
      animationInstance.destroy();
    }
    animationInstance = lottie.loadAnimation({
      container: animationContainer.value,
      animationData: newAnimationData,
      renderer: "svg",
      autoplay: props.autoplay,
    });
  }
);
</script>
