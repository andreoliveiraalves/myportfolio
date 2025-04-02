<template>
  <div class="language-toggler" @click="toggleLanguage">
    <img :src="flagSrc" :alt="language" class="flag-icon" />
    <span class="lang-text"><small>{{ language.toUpperCase() }}</small></span>
  </div>
</template>

<script>
export default {
  name: "LanguageToggler",
  data() {
    return {
      language: localStorage.getItem("preferredLanguage") || "pt", // Load from localStorage or default to "pt"
    };
  },
  computed: {
    flagSrc() {
      return this.language === "en"
        ? "https://flagcdn.com/w40/gb.png"
        : "https://flagcdn.com/w40/pt.png";
    },
  },
  methods: {
    toggleLanguage() {
      this.language = this.language === "en" ? "pt" : "en";
      localStorage.setItem("preferredLanguage", this.language); // Save to localStorage
      this.$emit("language-changed", this.language);
    },
  },
};
</script>

<style scoped>
.language-toggler {
  position: fixed;
  top: 10px;
  right: 15px;
  background: rgba(0, 0, 0, 0.05);
  color: white;
  padding: 8px 15px;
  border-radius: 10px;
  font-size: 14px;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  user-select: none;
  gap: 8px;
}

.language-toggler:hover {
  background: rgba(0, 0, 0, 0.1);
  transform: scale(1.05);
}

/* Flag styling */
.flag-icon {
  width: 24px;
  height: 16px;
  border-radius: 3px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

/* Language text styling */
.lang-text {
  font-weight: bold;
  font-size: 14px;
  color: rgb(33, 37, 41);
}
</style>