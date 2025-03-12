<template>
  <div class="py-10">
    <v-container>
      <header-and-subheader class="mb-15" header="Tech Stack"
        subheader="Languages, frameworks, and tools I work with:" />
      <v-row ref="techStackContainer">
        <transition-group name="slide-y">
          <v-col v-for="(item, index) in visibleTechStack" :key="item.name" cols="12" xs="6" sm="6" md="4"
            :data-index="index" class="tech-item">
            <v-card rounded="xl" class="card pa-3">
              <v-col>
                <v-icon :color="item.color" class="me-2" size="x-large">
                  {{ item.icon }}
                </v-icon>
                {{ item.name }}
              </v-col>
            </v-card>
          </v-col>
        </transition-group>
      </v-row>
      <v-col v-if="showExpandButton" class="d-flex justify-center mt-5">
        <v-btn class="hidden-md-and-up" height="40px" variant="text" rounded="pill" :append-icon="expandButtonIcon"
          @click="toggleExpanded">
          {{ expandButtonText }}
        </v-btn>
      </v-col>
    </v-container>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, nextTick } from "vue";
import { useDisplay } from "vuetify";
import gsap from "gsap";

const display = useDisplay();
const ITEMS_TO_SHOW = 3;
const isExpanded = ref(false);
const techStackContainer = ref(null);

const techStack = [
  { icon: "mdi-language-html5", name: "HTML5", color: "#F06529" },
  { icon: "mdi-language-css3", name: "CSS3", color: "#264de4" },
  { icon: "mdi-language-javascript", name: "JavaScript", color: "#F7DF1E" },
  { icon: "mdi-vuejs", name: "Vue.js", color: "#42B883" },
  { icon: "mdi-vuetify", name: "Vuetify", color: "#1867C0" },
  { icon: "mdi-laravel", name: "Laravel", color: "#FF2D20" },
  { icon: "mdi-database", name: "MySQL", color: "#4479A1" },
  { icon: "mdi-language-php", name: "PHP", color: "#777BB4" },
  { icon: "mdi-git", name: "Git & GitHub", color: "#F05032" },
];

const visibleTechStack = computed(() => {
  if (isExpanded.value || display.mdAndUp.value) {
    return techStack;
  }
  return techStack.slice(0, ITEMS_TO_SHOW);
});

const showExpandButton = computed(() => {
  return !display.mdAndUp.value && techStack.length > ITEMS_TO_SHOW;
});

const expandButtonText = computed(() => {
  return isExpanded.value ? "Show Less" : "Show More";
});

const expandButtonIcon = computed(() => {
  return isExpanded.value ? "mdi-chevron-double-up" : "mdi-chevron-double-down";
});

const toggleExpanded = () => {
  isExpanded.value = !isExpanded.value;
  nextTick(() => animateTechStack());
};

const animateTechStack = () => {
  gsap.from(".tech-item", {
    opacity: 0,
    y: 50,
    duration: 0.6,
    stagger: 0.2,
    ease: "power2.out",
  });
};

onMounted(() => {
  nextTick(() => animateTechStack());
});
</script>

<style scoped>
.card {
  transition: 0.3s;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: inset 0 0 0 1px #66fcf1;
}
</style>
