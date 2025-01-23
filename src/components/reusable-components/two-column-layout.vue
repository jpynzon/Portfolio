<template>
  <v-container fluid>
    <v-row class="d-flex flex-wrap" :class="customClass">
      <v-col v-if="showLeftColumn" :class="leftClass">
        <div v-if="defaultLeftLayout">
          <div class="mb-5">
            <h2>{{ leftHeader || "Left Header" }}</h2>
            <h3 v-if="leftSubheader" class="mb-2">
              {{ leftSubheader || "Left Subheader" }}
            </h3>
            <p>{{ leftDesciprtion || "Left Description" }}</p>
          </div>
          <v-btn
            v-if="showLeftButton"
            :color="leftButtonColor"
            :variant="leftButtonVariant"
            :height="leftButtonHeight"
            :class="leftButtonClass"
            >{{ leftButtonText || "Left Button Text" }}
          </v-btn>
        </div>

        <slot name="leftColumn" v-else></slot>
      </v-col>

      <v-col v-if="showRightColumn" :class="rightClass">
        <div v-if="defaultRightLayout">
          <div class="mb-5">
            <h2>{{ rightHeader || "Right Header" }}</h2>
            <h3 v-if="rightSubheader" class="mb-2">
              {{ rightSubheader || "Right Subheader" }}
            </h3>
            <p>{{ rightDescription || "Right Description" }}</p>
          </div>
          <v-btn
            v-if="showRightButton"
            :color="rightButtonColor"
            :variant="rightButtonVariant"
            :height="rightButtonHeight"
            :class="rightButtonClass"
            >{{ rightButtonText || "Right Button Text" }}</v-btn
          >
        </div>

        <slot name="rightColumn" v-else></slot>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
defineProps({
  leftClass: String,
  rightClass: String,
  customClass: String,
  showLeftColumn: {
    type: Boolean,
    default: true,
  },
  showRightColumn: {
    type: Boolean,
    default: true,
  },
  defaultLeftLayout: {
    type: Boolean,
    default: true,
  },
  defaultRightLayout: {
    type: Boolean,
    default: true,
  },
  leftHeader: String,
  leftSubheader: String,
  leftDescription: String,
  leftButtonText: String,
  leftButtonColor: String,
  leftButtonVariant: String,
  leftButtonClass: String,
  leftButtonHeight: String,
  showLeftButton: {
    type: Boolean,
    default: true,
  },
  rightHeader: String,
  rightSubheader: String,
  rightDescription: String,
  rightButtonText: String,
  rightButtonColor: String,
  rightButtonVariant: String,
  rightButtonClass: String,
  rightButtonHeight: String,
  showRightButton: {
    type: Boolean,
    default: true,
  },
});
</script>