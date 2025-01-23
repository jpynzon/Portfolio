<template>
  <div class="py-10">
    <v-container>
      <two-column-layout
        :default-left-layout="false"
        :default-right-layout="false"
        custom-class="align-center"
      >
        <template #leftColumn>
          <div class="mb-5">
            <h1 class="text-h1 mb-5 hidden-sm-and-down text-white">
              Joshua Paulo Ynzon
            </h1>
            <h1 class="text-h2 mb-5 hidden-md-and-up text-white">
              Joshua Paulo Ynzon
            </h1>
            <h1 class="text-subtitle-1 mb-10">
              A passionate web developer with the precision and problem-solving
              mindset of a software engineer.
            </h1>
            <div class="d-flex align-center">
              <v-btn
                color="primary"
                height="50px"
                variant="outlined"
                @click="downloadResume"
                :class="$vuetify.display.mobile ? 'px-5 me-3' : 'px-8 me-3'"
                rounded="pill"
                prepend-icon="mdi-tray-arrow-down"
                >Resume</v-btn
              >
              <v-btn
                href="#project"
                :class="$vuetify.display.mobile ? 'px-5 me-3' : 'px-8'"
                rounded="pill"
                color="primary"
                height="50px"
                >View Projects</v-btn
              >
            </div>
          </div>
        </template>
        <template #rightColumn>
          <div>
            <v-img
              src="@/assets/joshua.webp"
              min-width="300px"
              width="100%"
              height="100%"
              rounded="xl"
              elevation="2"
            ></v-img>
          </div>
        </template>
      </two-column-layout>
    </v-container>
  </div>
</template>
<script setup>
import { saveAs } from "file-saver";

const downloadResume = () => {
  saveAs("@/assets/resume.pdf", "Joshua-Paulo-Ynzon_Resume.pdf");
};
</script>