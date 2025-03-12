<template>
    <div>
        <Flicking :options="{ circular: true, bound: false, align: 'prev', moveType: 'snap' }" :plugins="plugins"
            class="carousel">
            <div v-for="item in items" :key="item.title" class="flicking-panel">
                <v-card class="card" rounded="xl">
                    <v-container>
                        <v-card width="100%" height="200px" rounded="xl">
                            <v-img :src="item.image || 'https://i.sstatic.net/y9DpT.jpg'" height="100%" width="100%"
                                cover />
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
                            <div v-for="button in item.buttons" :key="button.label">
                                <v-btn v-if="button" class="me-3" height="40px" variant="outlined" rounded="pill"
                                    size="small" :prepend-icon="button.icon" :href="button.href" target="_blank">
                                    {{ button.label || "Button Label" }}
                                </v-btn>
                            </div>
                        </div>
                    </v-container>
                </v-card>
            </div>
        </Flicking>
    </div>
</template>

<script setup>
import Flicking from "@egjs/vue3-flicking";
import "@egjs/vue3-flicking/dist/flicking.css";
import { AutoPlay } from "@egjs/flicking-plugins";

defineProps({
    items: Array,
});

const plugins = [new AutoPlay({ duration: 3000, direction: "NEXT", stopOnHover: true })];
</script>

<style scoped>
.carousel {
    width: 100%;
    overflow: hidden;
}

.flicking-panel {
    width: 33%;
    /* Show 3 cards at a time */
    padding: 10px;
}
</style>
