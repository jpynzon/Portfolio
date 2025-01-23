<template>
  <div class="py-10 mb-15">
    <v-container>
      <header-and-subheader
        class="mb-15"
        header="Let's Work Together"
        subheader="We'd love to hear from you! Share your thoughts and ideas with us."
        :show-subheader="true"
      />

      <v-card rounded="xl" class="pa-10">
        <v-form
          ref="form"
          @submit.prevent="sendEmail"
          class="position-relative"
        >
          <LottieAnimation
            v-if="successfulSubmission"
            :animation-data="success"
            custom-style="height: 200px !important; position: absolute; top: 0; left: 50%; transform: translate(-50%, 50%);"
          />

          <div
            class="mb-3"
            :style="successfulSubmission ? 'opacity: 0;' : 'block'"
          >
            <h1 class="text-body-2">How should we call you?</h1>
            <v-text-field
              v-model="formData.name"
              placeholder="Type your full name"
              rounded="lg"
              required
              hint="Tell us your name so we can address you properly."
              :rules="nameRules"
            />
          </div>
          <div
            class="mb-3"
            :style="successfulSubmission ? 'opacity: 0;' : 'block'"
          >
            <h1 class="text-body-2">Where can we reach you?</h1>
            <v-text-field
              v-model="formData.email"
              placeholder="example@email.com"
              type="email"
              required
              hint="We'll use this to get back to you."
              :rules="emailRules"
            />
          </div>
          <div :style="successfulSubmission ? 'opacity: 0;' : 'block'">
            <h1 class="text-body-2">What’s on your mind?</h1>
            <v-textarea
              v-model="formData.message"
              placeholder="Type your message"
              required
              hint="Feel free to share any thoughts, feedback, or ideas."
              :rules="messageRules"
            />
          </div>

          <v-btn
            v-if="!successfulSubmission"
            class="float-right"
            type="submit"
            height="40px"
            rounded="pill"
            color="primary"
            :loading="loading"
            :disabled="!isFormValid"
          >
            Send Message
          </v-btn>
        </v-form>

        <div v-if="errorMessage">{{ errorMessage }}</div>
      </v-card>

      <v-row class="mt-5">
        <v-col
          v-for="item in contactItems"
          :key="item.name"
          cols="12"
          xs="6"
          sm="6"
          md="4"
        >
          <v-card rounded="xl" class="card pa-3">
            <v-col class="d-flex align-center">
              <v-icon :color="item.color" class="me-2" size="x-large">
                {{ item.icon }}
              </v-icon>
              <span class="w-100 text-wrap pe-10">
                {{ item.name }}
              </span>
            </v-col>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import emailjs from "emailjs-com";
import success from "@/assets/lottie/email-sent.json";

const errorMessage = ref("");
const formData = ref({
  name: "",
  email: "",
  message: "",
});

const successfulSubmission = ref(false);
const loading = ref(false);

const isAnyFieldFilled = computed(() => {
  return formData.value.name || formData.value.email || formData.value.message;
});
const nameRules = [
  (value) => !isAnyFieldFilled.value || !!value || "Name is required",
];
const emailRules = [
  (value) => !isAnyFieldFilled.value || !!value || "Email is required",
  (value) =>
    !isAnyFieldFilled.value ||
    /.+@.+\..+/.test(value) ||
    "Please enter a valid email address",
];
const messageRules = [
  (value) => !isAnyFieldFilled.value || !!value || "Message is required",
];

const isFormValid = computed(() => {
  return (
    formData.value.name &&
    formData.value.email &&
    formData.value.message &&
    /.+@.+\..+/.test(formData.value.email)
  );
});

const contactItems = [
  { icon: "mdi-email", name: "joshuapauloynzon@gmail.com", color: "#f2a60c" },
  { icon: "mdi-linkedin", name: "jpynzon", color: "#0077B5" },
  { icon: "mdi-facebook", name: "jpynzon", color: "#1877F2" },
];

const resetForm = () => {
  formData.value.name = "";
  formData.value.email = "";
  formData.value.message = "";
};

const sendEmail = () => {
  loading.value = true;

  const serviceID = import.meta.env.VITE_SERVICE_ID;
  const templateID = import.meta.env.VITE_TEMPLATE_ID;
  const userID = import.meta.env.VITE_USER_ID;

  const templateParams = {
    from_email: formData.value.email,
    from_name: formData.value.name,
    message: formData.value.message,
  };

  const onSuccess = () => {
    successfulSubmission.value = true;
    resetForm();
    setTimeout(() => {
      successfulSubmission.value = false;
    }, 5000);
  };

  const onError = () => {
    errorMessage.value = "An error occurred. Please try again later.";
  };

  const onFinally = () => {
    loading.value = false;
  };

  emailjs
    .send(serviceID, templateID, templateParams, userID)
    .then(onSuccess)
    .catch(onError)
    .finally(onFinally);
};
</script>

