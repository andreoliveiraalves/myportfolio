<template>
  <div class="sidebar">
    <div v-if="!hideAvatar">
      <div class="avatar-container d-flex justify-content-center align-items-end mt-4 mb-4">
        <img class="avatar" src="/profile-photo.webp" alt="A picture of me" />
      </div>
      <div class="text-container mb-4">
        <p class="name text-center m-0 p-0 fs-4">ANDRÉ ALVES</p>
        <p class="role text-center m-0 p-0">{{ translations.sidebar.role }}</p>
      </div>
    </div>
    <div class="navigation mt-5 mt-md-4">
      <nav>
        <a v-for="link in links" :key="link.id"
          :class="['link', 'd-flex', 'align-items-center', 'ps-4', 'mb-3', { active: activeLink === link.id }]"
          :href="link.href" data-bs-dismiss="offcanvas" @click="setActiveLink(link.id)">
          <span class="d-flex align-items-center">
            <svg-icon class="icon me-2" type="mdi" :path="link.icon"></svg-icon>
          </span>
          {{ translations.sidebar[link.text.toLowerCase()] }}
        </a>
      </nav>
    </div>
  </div>
</template>

<script>
import SvgIcon from "@jamescoyle/vue-icon";
import { mdiCardAccountDetails, mdiSchool, mdiCogs, mdiBriefcase, mdiFolderMultiple, mdiHeart, mdiEmail } from "@mdi/js";

// Import translation files
import enTranslations from '@/translations/en.json';
import ptTranslations from '@/translations/pt.json';

export default {
  name: "SideBar",
  components: {
    SvgIcon,
  },
  props: {
    hideAvatar: Boolean,
    language: {
      type: String,
      default: 'pt', // Default to 'pt'
    },
  },
  data() {
    return {
      activeLink: 'about', // Default active link
      translations: ptTranslations, // Default to pt-PT translations
      links: [
        { id: 'about', text: 'about', href: '#about', icon: mdiCardAccountDetails },
        { id: 'education', text: 'education', href: '#education', icon: mdiSchool },
        { id: 'skills', text: 'skills', href: '#skills', icon: mdiCogs },
        { id: 'experience', text: 'experience', href: '#experience', icon: mdiBriefcase },
        { id: 'portfolio', text: 'portfolio', href: '#portfolio', icon: mdiFolderMultiple },
        { id: 'hobbies', text: 'hobbies', href: '#hobbies', icon: mdiHeart },
        { id: 'contact', text: 'contact', href: '#contact', icon: mdiEmail }
      ]
    };
  },
  watch: {
    language(newLang) {
      // Dynamically load translations based on the selected language
      this.translations = newLang === 'en' ? enTranslations : ptTranslations;
    },
  },
  created() {
    // Set the default language from the parent prop
    this.translations = this.language === 'en' ? enTranslations : ptTranslations;
  },
  methods: {
    setActiveLink(linkId) {
      this.activeLink = linkId;
    },
  },
};
</script>

<style scoped>
.sidebar {
  width: 100%;
  height: 100%;
  background-color: #212529;
  overflow-y: auto;
}

@media (min-width: 768px) {
  .sidebar {
    width: 300px;
    height: 100vh;
    position: fixed;
    left: 0;
    top: 0;
  }
}

.avatar-container {
  width: 100%;
  padding-top: 20px;
}

.avatar {
  width: 130px;
  height: 130px;
  border: 5px solid rgba(106, 119, 131, 0.15);
  border-radius: 100%;
  object-fit: cover;
  object-position: bottom;
}

.text-container {
  width: 100%;
}

.name {
  color: #fff;
  font-weight: 700;
}

.role {
  color: #adb5bd;
  font-size: 14px;
}

.link {
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  color: #bebebe;
  padding: 8px 16px;
  transition: all 0.2s ease;
}

.link.active,
.link:hover {
  color: #F8F9FA;
  background-color: rgba(255, 255, 255, 0.1);
}

.link.active .icon,
.link:hover .icon {
  color: #bebebe;
}

.link .icon {
  width: 18px;
  height: 18px;
  color: #F8F9FA;
}
</style>