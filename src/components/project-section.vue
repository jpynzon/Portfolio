<template>
  <div class="py-10">
    <v-container>
      <header-and-subheader class="mb-15" header="My Projects"
        subheader="A collection of my personal and team projects." />

      <card-with-image-and-text :items="displayedProjects" />

      <v-col class="d-flex justify-center mt-5">
        <v-btn height="40px" rounded="pill" variant="text" append-icon="mdi-arrow-right" @click="toggleShowAll">
          {{ showAll ? 'Show Less' : 'See All' }}
        </v-btn>
      </v-col>
    </v-container>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import wealthMe from "@/assets/project-thumbnails/wealthme.png";
import quizStudio from "@/assets/project-thumbnails/quiz-studio.png";
import passaQuiz from "@/assets/project-thumbnails/passaquiz.png";
import yenhost from "@/assets/project-thumbnails/yenhost.png";
import quickBites from "@/assets/project-thumbnails/quickbites.png";

import wealthMeLogo from "@/assets/project-logos/wealthme-logo.png";
import quizStudioLogo from "@/assets/project-logos/quiz-studio.webp";
import passaQuizLogo from "@/assets/project-logos/passaquiz-logo.png";
import yenhostLogo from "@/assets/project-logos/yenhost.png";
import quickBitesLogo from "@/assets/project-logos/quickbites-logo.png";

const projects = [
{
    image: wealthMe,
    logo: wealthMeLogo,
    title: "WealthMe",
    tags: ['Vuetify', 'Laravel', 'OpenAI'],
    description:
      "AI powered personal finance management tool that helps users track their expenses, set budgets, and gain insights into their spending habits.",
    buttons: [
      {
        href: "https://github.com/orgs/QuickBites-Capstone/repositories",
        label: "Repository",
        icon: "mdi-github",
      },
    ],
  },
  {
    image: quizStudio,
    logo: quizStudioLogo,
    title: "Quiz Studio",
    tags: ['Vuetify', 'Laravel', 'BootstrapCSS'],
    description:
      "An AdminCMS for managing dynamic quizzes and participants, with customizable themes, question types, and participant tracking.",
    buttons: [
      {
        href: "https://games.studio.passafund.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
  {
    image: passaQuiz,
    logo: passaQuizLogo,
    title: "PassaQuiz",
    tags: ['PrimeVue', 'Laravel', 'TailwindCSS'],
    description:
      "An AdminCMS for managing dynamic quizzes and participants, with customizable themes, question types, and participant tracking.",
    buttons: [
      {
        href: "https://play.passafund.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
  {
    image: yenhost,
    logo: yenhostLogo,
    title: "YenHost",
    tags: ['Vuetify'],
    description:
      "A reliable shared web hosting service with cPanel integration, offering seamless website management and performance optimization.",
    buttons: [
      {
        href: "https://github.com/jpynzon/yenhost-frontend",
        label: "Repository",
        icon: "mdi-github",
      },
      {
        href: "https://yenhost.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
  {
    image: quickBites,
    logo: quickBitesLogo,
    title: "Quick Bites",
    tags: ['Vuetify', 'Laravel'],
    description:
      "A canteen pre-order system that lets customers pre order products from the canteen for a quick pick-up.",
    buttons: [
      {
        href: "https://github.com/orgs/QuickBites-Capstone/repositories",
        label: "Repository",
        icon: "mdi-github",
      },
    ],
  },
];

const showAll = ref(false);

const displayedProjects = computed(() => (showAll.value ? projects : projects.slice(0, 2)));

const toggleShowAll = () => {
  showAll.value = !showAll.value;
};
</script>
