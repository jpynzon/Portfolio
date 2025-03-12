<template>
  <div class="py-10">
    <v-container>
      <header-and-subheader class="mb-15" header="About Me" :show-subheader="false" />
      <v-card rounded="xl">
        <two-column-layout :default-left-layout="false" :default-right-layout="false" custom-class="align-center px-10">
          <template #rightColumn>
            <div class="mb-5">
              <h1 class="text-body-1 mb-5">
                Hi, I'm Joshua Paulo Ynzon, a web developer who loves combining
                creativity with technical skills to build seamless digital
                experiences. My expertise lies in modern frameworks like Vue.js
                and Vuetify, backed by a strong foundation in backend
                development using Laravel.
              </h1>
              <h1 class="text-body-1">
                Driven by curiosity and a passion for problem-solving, I thrive
                on tackling challenges and creating user-centric solutions that
                make an impact. When I'm not coding, you'll find me exploring
                new design trends or learning about emerging technologies to
                stay ahead in the ever-evolving tech world.
              </h1>
            </div>
          </template>
          <template #leftColumn>
            <div>
              <LottieAnimation style="min-width: 200px; width: 100%; height: 100%" :animation-data="manCoding" />
            </div>
          </template>
        </two-column-layout>
      </v-card>
    </v-container>
  </div>
</template>

<script setup>
import manCoding from "@/assets/lottie/man-coding.json";
</script>
