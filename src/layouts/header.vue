<template>
  <v-app-bar class="nav-bar" elevation="0">
    <v-container>
      <div class="d-flex w-100 justify-space-between align-center px-5">
        <div class="menu-button hidden-md-and-up">
          <v-btn
            @click="sidebar = !sidebar"
            class="menu-btn"
            variant="text"
            height="40px"
          >
            <span class="menu-icon" :class="{ open: sidebar }">
              <span></span>
              <span></span>
              <span></span>
            </span>
          </v-btn>
        </div>

        <div class="nav-links hidden-sm-and-down">
          <v-btn
            v-for="item in navigationLinks"
            :key="item.title"
            :href="item.href"
            class="me-5"
            height="50px"
          >
            {{ item.title }}
          </v-btn>
        </div>

        <div class="social-links">
          <v-btn
            v-for="item in socialLinks"
            class="me-2"
            size="small"
            target="_blank"
            :key="item.icon"
            :icon="item.icon"
            :href="item.href"
          />
        </div>
      </div>
    </v-container>
  </v-app-bar>

  <v-navigation-drawer
    v-model="sidebar"
    v-if="sidebar"
    class="side-bar"
    elevation="0"
    temporary
  >
    <v-list v-for="item in navigationLinks" :key="item.title">
      <v-list-item :href="item.href" :prepend-icon="item.icon">{{
        item.title
      }}</v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script setup>
const sidebar = ref(false);

const socialLinks = [
  { icon: "mdi-github", href: "https://github.com/jpynzon" },
  { icon: "mdi-linkedin", href: "https://linkedin.com/in/jpynzon" },
  { icon: "mdi-facebook", href: "https://facebook.com/jpynzon" },
];

const navigationLinks = [
  { title: "Home", icon: "mdi-home-outline", href: "#" },
  { title: "About", icon: "mdi-account-outline", href: "#about" },
  { title: "Projects", icon: "mdi-briefcase-outline", href: "#project" },
  { title: "Journey", icon: "mdi-notebook", href: "#journey" },
  { title: "Contact", icon: "mdi-email-outline", href: "#contact" },
];
</script>

<style scoped>
.nav-bar {
  background-color: rgba(0, 0, 0, 0.1) !important;
  backdrop-filter: blur(30px) !important;
  transition: background-color 0.3s, backdrop-filter 0.3s !important;
}
.side-bar {
  background-color: rgba(0, 0, 0, 0.5) !important;
  backdrop-filter: blur(30px) !important;
  transition: background-color 0.3s, backdrop-filter 0.3s !important;
}

.menu-btn {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  background: none;
  border: none;
  cursor: pointer;
}

.menu-icon {
  position: relative;
  width: 24px;
  height: 18px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.menu-icon span {
  display: block;
  width: 100%;
  height: 3px;
  background: #66fcf1;
  border-radius: 0px;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.menu-icon.open span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.menu-icon.open span:nth-child(2) {
  opacity: 0;
}

.menu-icon.open span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}
</style>