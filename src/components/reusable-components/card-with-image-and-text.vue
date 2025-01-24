<template>
  <div>
    <v-row>
      <v-col cols="12" lg="4" md="4" sm="6" v-for="item in items" :key="item">
        <v-card class="card" rounded="xl">
          <v-container>
            <v-card width="100%" height="200px" rounded="xl">
              <v-img
                :src="item.image || 'https://i.sstatic.net/y9DpT.jpg'"
                height="100%"
                width="100%"
                cover
              />
            </v-card>
            <div class="text mb-5">
              <h1 class="text-h6 mb-2 mt-5">
                {{ item.title || "Project title" }}
              </h1>
              <h1 class="text-body-2">
                {{ item.description || "Project Description" }}
              </h1>
            </div>
            <div class="d-flex align-center">
              <div v-for="button in item.buttons" :key="button">
                <v-btn
                  v-if="button"
                  class="me-3"
                  height="40px"
                  variant="outlined"
                  rounded="pill"
                  size="small"
                  :prepend-icon="button.icon"
                  :href="button.href"
                  target="_blank"
                  >{{ button.label || "Button Label" }}</v-btn
                >
              </div>
            </div>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
defineProps({
  items: Array,
});
</script>