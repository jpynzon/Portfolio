<template>
  <div class="py-10">
    <v-container>
      <header-and-subheader
        class="mb-15"
        header="Career Journey"
        subheader="Showcasing the companies I've worked with and the hands-on experience I've gained."
      />

      <v-card
        v-for="item in journey"
        :key="item.company"
        rounded="xl"
        class="mb-10"
      >
        <two-column-layout
          :default-left-layout="false"
          :default-right-layout="false"
          custom-class="align-center px-10 py-5"
        >
          <template #leftColumn>
            <div class="mb-5">
              <div class="mb-5">
                <h1 class="text-h4">{{ item.company }}</h1>
                <h1 class="text-h6">{{ item.position }}</h1>
              </div>
              <h1 class="text-body-1">
                {{ item.description }}
              </h1>
            </div>
          </template>
          <template #rightColumn>
            <div>
              <v-carousel
                hide-delimiters
                style="
                  min-width: 200px;
                  width: 100%;
                  height: 100%;
                  border-radius: 15px;
                "
              >
                <v-carousel-item
                  v-for="image in item.carouselImages"
                  :key="image"
                  :src="image.src"
                  max-height="350px"
                  cover
                ></v-carousel-item>
              </v-carousel>
            </div>
          </template>
        </two-column-layout>
      </v-card>
    </v-container>
  </div>
</template>

<script setup>
import passafundImage1 from "@/assets/images/passafund/passafund-1.webp";
import passafundImage2 from "@/assets/images/passafund/passafund-2.webp";
import passafundImage3 from "@/assets/images/passafund/passafund-3.webp";

const journey = [
  {
    company: "Passafund",
    position: "Software Engineer OJT",
    description:
      "Contributed to the development of dynamic web applications by building user-friendly interfaces using modern frameworks like Vue.js and Vuetify. Collaborated closely with senior developers to optimize performance and ensure code quality. Implemented key features for Passafund's platform, such as real-time data fetching, dynamic quiz management, and enhanced user authentication. This experience provided a strong foundation in software engineering practices, teamwork, and problem-solving.",
    carouselImages: [
      { src: passafundImage1 },
      { src: passafundImage2 },
      { src: passafundImage3 },
    ],
  },
];
</script>