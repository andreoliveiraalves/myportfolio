<template>
  <div class="container-fluid p-0">
    <!-- Mobile Hamburger Button -->
    <button class="menu-toggle position-fixed d-md-none m-3 bg-light rounded p-2 shadow-sm" type="button"
      @click="isNavOpen = !isNavOpen">
      <svg-icon type="mdi" :path="mdiMenu" size="24" />
    </button>

    <!-- Language Toggler -->
    <LanguageToggler class="language-toggler" @language-changed="handleLanguageChange" />

    <!-- Overlay for Background Dim Effect -->
    <div v-if="isNavOpen" class="overlay" @click="isNavOpen = false"></div>

    <!-- Desktop Sidebar -->
    <div class="side-bar-container d-none d-md-block">
      <SideBar :language="currentLanguage" />
    </div>

    <!-- Custom Mobile Sidebar -->
    <div v-if="isNavOpen" class="mobile-sidebar">
      <button class="close-btn" @click="isNavOpen = false">&times;</button>
      <SideBar hide-avatar @close-sidebar="isNavOpen = false" :language="currentLanguage" />
    </div>

    <!-- Main Content -->
    <div class="main-container" :class="{ 'blurred': isNavOpen }">
      <About :language="currentLanguage" />
      <Education />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SideBar from "./components/SideBar.vue";
import About from "./components/main/About.vue";
import Education from "./components/main/Education.vue";
import LanguageToggler from "./components/LanguageToggler.vue";
import { mdiMenu } from "@mdi/js";
import SvgIcon from "@jamescoyle/vue-icon";

const isNavOpen = ref(false);
const currentLanguage = ref(localStorage.getItem("preferredLanguage") || "pt");

// Handle the language change event emitted from LanguageToggler
const handleLanguageChange = (newLanguage) => {
  currentLanguage.value = newLanguage;
  localStorage.setItem("preferredLanguage", newLanguage); // Store language in localStorage
};
</script>

<style scoped>
.container-fluid {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  overflow-x: hidden;
  background: linear-gradient(135deg, #ffffff, #f4f4f4);
}

.main-container {
  background: linear-gradient(135deg, #ffffff, #f4f4f4);
  margin-left: 0;
  padding: 2.5rem;
  transition: margin 0.3s ease-in-out, opacity 0.3s ease-in-out;
}

@media (min-width: 768px) {
  .main-container {
    margin-left: 300px;
    padding: 3rem;
  }
}

/* Mobile Sidebar */
.mobile-sidebar {
  position: fixed;
  top: 0;
  left: 0;
  min-width: 95vw;
  height: 100vh;
  background-color: #212529;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.2);
  padding: 1.5rem;
  transition: transform 0.3s ease-in-out;
  z-index: 1050;
}

/* Close Button */
.close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  background: none;
  border: none;
  font-size: 24px;
  color: white;
  cursor: pointer;
}

/* Menu Button */
.menu-toggle {
  z-index: 1050;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

/* Overlay Dim Effect (No Blur) */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.4);
  z-index: 1049;
  transition: opacity 0.3s ease-in-out;
}

/* Dim Effect on Main Content */
.blurred {
  opacity: 0.5;
  pointer-events: none;
}
</style>