<template>
  <transition name="fade" tag="div" class="wrapper" mode="out-in">
    <div class="wrapper" v-if="isLoaded" id="app">
      <!-- Your components go here -->
      <Home :user="user" />
      <Description :user="user" :content="findSlug('description')" :links="findSlug('links')" />
      <Experience :content="findSlug('experiences')" />
      <Skills :content="findSlug('skills')" />
      <Projects :content="findSlug('projects')" />
      <Footer :user="user" :links="findSlug('links')" />
    </div>
  </transition>
</template>

<script>
import Home from "./components/Home.vue";
import Description from "./components/Description.vue";
import Experience from "./components/Experience.vue";
import Skills from "./components/skills.vue";
import Projects from "./components/Projects.vue";
import Footer from "./components/Footer.vue";

import { cosmic } from "./cosmic.js";

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
  data: () => ({
    isLoaded: false,
    user: {},
    posts: [],
  }),
  methods: {
    async fetchPosts() {
      try {
        const response = await cosmic.objects
          .find({
            type: 'portfolio-contents',
          })
          .props(['slug', 'title', 'metadata'])
          .limit(10);

        return response.objects;
      } catch (error) {
        console.error('Error fetching posts:', error);
        return [];
      }
    },
    async fetchUser() {
      try {
        const response = await cosmic.objects
          .findOne({
            type: 'portfolio-contents',
            slug: 'user-data',
          })
          .props(['slug', 'title', 'metadata']);

        return response ||{};
      } catch (error) {
        console.error('Error fetching user data:', error);
        return {};
      }
    },
    findSlug(slug) {
      return this.posts.find((item) => {
        return item.slug === slug;
      });
    },
    extractFirstObject(objects) {
      if (objects && objects.objects) {
        return objects.objects[0];
      }
      return undefined;
    },
  },
  async created() {
  document.body.classList.add("loading");
  try {
    const [posts, user_data_response] = await Promise.all([this.fetchPosts(), this.fetchUser()]);
    let user_data = this.extractFirstObject(user_data_response);
    this.posts = posts;

    // Check if user_data is defined before accessing properties
    if (user_data) {
      this.user = {
        name: user_data.metadata?.name,
        status: user_data.metadata?.status,
        email: user_data.metadata?.email,
        phone: user_data.metadata?.phone,
        city: user_data.metadata?.city,
        lang: user_data.metadata?.lang,
        photo: user_data.metadata?.photo,
      };
    } else {
      console.error('User data is undefined.');
    }

    this.isLoaded = true;
    this.$nextTick(() => document.body.classList.remove("loading"));
  } catch (error) {
    console.error('Error in created hook:', error);
  }
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
