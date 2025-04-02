<template>
  <div class="about section" id="about">
    <h1 class="main-heading">{{ translations.about.heading }}</h1>
    <div class="info-bar mt-4 d-flex flex-column flex-md-row">
      <div v-for="(line, index) in translations.about.info" :key="index"
        class="item mb-3 mb-md-0 me-md-4 d-flex align-items-center" :class="line.class">
        <!-- Icon for each contact line -->
        <svg-icon v-if="line.icon" type="mdi" class="me-2 icon" :path="getIcon(line.icon)"></svg-icon>
        <!-- Contact info rendering -->
        <a v-if="line.type === 'email'" :href="`mailto:${line.text}`" class="text-break">{{ line.text }}</a>
        <a v-else-if="line.type === 'phone'" :href="`tel:${line.text}`">{{ line.text }}</a>
        <span v-else>{{ line.text }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import SvgIcon from "@jamescoyle/vue-icon";
import { mdiCityVariantOutline, mdiEmailOutline, mdiCellphone } from "@mdi/js"; // Import icons directly
import enTranslations from '@/translations/en.json';  // Import English translations
import ptTranslations from '@/translations/pt.json';  // Import Portuguese translations

export default {
  name: "About-me",
  components: {
    SvgIcon
  },
  props: {
    language: {
      type: String,
      default: "pt"
    }
  },
  data() {
    return {
      translations: ptTranslations,  // Default to Portuguese
      // Define icons explicitly in the data (fallback to these if icon path isn't in translation)
      icons: {
        city: mdiCityVariantOutline,
        email: mdiEmailOutline,
        phone: mdiCellphone
      }
    };
  },
  watch: {
    language(newLang) {
      // Dynamically load translations based on the selected language
      this.translations = newLang === "en" ? enTranslations : ptTranslations;
    }
  },
  methods: {
    // Helper method to get the correct icon based on translation or fallback to `icons`
    getIcon(iconName) {
      return this.icons[iconName] || mdiCityVariantOutline; // Default to city icon if not found
    }
  }
};
</script>