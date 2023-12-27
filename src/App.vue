<template>
  <div id="app">
    <Home :user="user" />
    <Description :user="user" :content="content" />
    <Experience :content="experience" />
    <Skills :content="skills" />
    <Projects :content="projects" />
    <Footer :user="user" :links="links" />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Description from "./components/Description.vue";
import Experience from "./components/Experience.vue";
import Skills from "./components/skills.vue";
import Projects from "./components/Projects.vue";
import Footer from "./components/Footer.vue";

import { description, experiences, links, projects, skills, userData } from "./portfolioData.js";

export default {
  name: "App",
  components: {
    Home,
    Description,
    Experience,
    Skills,
    Projects,
    Footer,
  },
  data() {
    return {
      user: userData,
      content: description,
      experience: experiences,
      skills: skills,
      projects: projects,
      links: links,
    };
  },
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

#app {
  font-family: Montserrat-Regular, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.wrapper {
  height: 100%;
}
</style>