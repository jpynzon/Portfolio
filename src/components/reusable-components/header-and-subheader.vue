<template>
  <div>
    <h1 class="text-h2 mb-5" :class="headerClass">{{ header }}</h1>
    <h1 class="text-h6" :class="subheaderClass" v-if="showSubheader">
      {{ subheader }}
    </h1>
  </div>
</template>

<script setup>
defineProps({
  headerClass: {
    type: String,
    default: "text-white text-center",
  },
  subheaderClass: {
    type: String,
    default: "text-center",
  },
  header: {
    type: String,
    default: "Header",
  },
  subheader: {
    type: String,
    default: "Subheader",
  },
  showSubheader: {
    type: Boolean,
    default: true,
  },
});
</script>