<template>
  <div class="py-10">
    <v-container>
      <header-and-subheader
        class="mb-15"
        header="My Projects"
        subheader="A collection of my personal and team projects."
      />

      <card-with-image-and-text :items="projects" />

      <v-col class="d-flex justify-center mt-5">
        <v-btn
          height="40px"
          rounded="pill"
          variant="text"
          append-icon="mdi-arrow-right"
          to="projects"
        >
          See All
        </v-btn>
      </v-col>
    </v-container>
  </div>
</template>

<script setup>
import quizStudio from "@/assets/project-thumbnails/quiz-studio.webp";
import installSmtp from "@/assets/project-thumbnails/install-smtp.webp";
import quickBites from "@/assets/project-thumbnails/quick-bites.webp";

const projects = [
  {
    image: quizStudio,
    title: "Quiz Studio",
    description:
      "An AdminCMS for managing dynamic quizzes and participants, with customizable themes, question types, and participant tracking.",
    buttons: [
      { href: "", label: "Repository", icon: "mdi-github" },
      {
        href: "https://dev.studio.passafund.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
  {
    image: installSmtp,
    title: "Install SMTP",
    description:
      "An automated solution for setting up SMTP, simplifying the configuration process for seamless email integration.",
    buttons: [
      {
        href: "https://github.com/jpynzon/install-smtp",
        label: "Repository",
        icon: "mdi-github",
      },
      {
        href: "https://dev.play.passafund.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
  {
    image: quickBites,
    title: "Quick Bites",
    description:
      "A canteen pre-order system that lets customers pre order products from the canteen for a quick pick-up.",
    buttons: [
      {
        href: "https://github.com/orgs/QuickBites-Capstone/repositories",
        label: "Repository",
        icon: "mdi-github",
      },
      {
        href: "https://dev.play.passafund.com",
        label: "Live Demo",
        icon: "mdi-web",
      },
    ],
  },
];
</script>

<style scoped>
.card {
  transition: 0.3s;
}
.card:hover {
  cursor: pointer;
  transform: translateY(-10px);
  box-shadow: inset 0 0 0 1px #66fcf1;
}
</style>
