<template>
  <div class="education sec-section" id="education">
    <h1 class="sec-heading">{{ heading }}</h1>

    <!-- Info Bar -->
    <div class="info-bar mt-4 d-flex flex-column">
      <div v-for="(line, index) in info" :key="index" class="item mb-3 d-flex align-items-center text-break"
        :class="line.class">
        <svg-icon type="mdi" class="me-2 icon" :path="line.icon"></svg-icon>
        <a v-if="line.link" :href="line.link" target="_blank" class="text-break">{{ line.text }}</a>
        <span v-else>{{ line.text }}</span>
      </div>
    </div>
    <!-- Education Content -->
    <div class="education-content mt-2">
      <ul>
        <li>
          Web development (Frontend & Backend)
        </li>
        <li>
          Game development with Unity & C#
        </li>
        <li>
          Database management (SQL, NoSQL)
        </li>
        <li>
          AI & Data analysis with Python
        </li>
        <li>
          UX/UI design & Agile methodologies
        </li>
        <li>
          Mobile & cloud computing
        </li>
        <li>
          Entrepreneurship & project management
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import SvgIcon from "@jamescoyle/vue-icon";
import { mdiSchoolOutline, mdiCalendarRange, mdiDomain } from "@mdi/js";
import "@/styles/main.css";

export default {
  name: "Education-Section",
  components: {
    SvgIcon
  },
  data() {
    return {
      heading: "EDUCATION",
      info: [
        { text: "Bachelor's in Web Technologies and Information Systems", icon: mdiSchoolOutline, class: "highlight" },
        { text: "2021-2023", icon: mdiCalendarRange, class: "highlight" },
        { text: "ESMAD - Escola Superior de Media, Artes e Design", icon: mdiDomain, class: "highlight", link: "https://www.esmad.ipp.pt/" }
      ],
    };
  },
  methods: {
  }
};
</script>