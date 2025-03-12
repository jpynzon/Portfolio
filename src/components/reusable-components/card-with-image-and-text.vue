<template>
  <div>
    <v-row>
      <v-col cols="12" lg="6" md="6" sm="6" v-for="item in items" :key="item">
        <v-card class="custom-card cursor-pointer pa-5" rounded="xl">
          <div class="image-container">
            <v-img class="card-image" rounded="xl" cover :src="item.image || 'https://i.sstatic.net/y9DpT.jpg'" />

            <div class="overlay pa-5">
              <div>
                <v-img v-if="item.logo" :src="item.logo" max-width="200px" width="100%" class="mb-5" />

                <p class="text-caption font-outfit mb-5">
                  {{ item.description || "Project Description" }}
                </p>

                <v-chip v-for="(tag, index) in item.tags" :key="index" class="bg-white font-outfit me-2" size="small">
                  {{ tag }}
                </v-chip>
              </div>
            </div>
          </div>

          <div class="card-content">
            <h1 class="card-title font-bangers">{{ item.title || "Project Title" }}</h1>
          </div>

          <!-- Buttons Section -->
          <div class="button-container d-flex align-center">
            <v-btn v-for="button in item.buttons" :key="button.label" class="me-3" height="40px" variant="outlined"
              rounded="pill" size="small" :prepend-icon="button.icon" :href="button.href" target="_blank">
              {{ button.label || "Button Label" }}
            </v-btn>
          </div>
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

<style scoped>
.custom-card {
  position: relative;
  overflow: hidden;
  transition: bottom 0.7s;
  transition-property: all;
  transition-timing-function: cubic-bezier(.4, 0, .2, 1);
}

.image-container {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
  border-radius: 12px;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: 0.7s;
  transition-property: all;
  transition-timing-function: cubic-bezier(.4, 0, .2, 1);
}

.overlay {
  position: absolute;
  display: flex;
  align-items: end;
  bottom: -100%;
  opacity: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  font-size: 20px;
  font-weight: bold;
  transition: bottom 0.7s;
  transition-property: all;
  transition-timing-function: cubic-bezier(.4, 0, .2, 1);
}

.image-container:hover .overlay {
  bottom: 0;
  opacity: 1;
}

.image-container:hover .card-image {
  transform: scale(1.2);
}

.card-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px;
  color: white;
}
</style>
