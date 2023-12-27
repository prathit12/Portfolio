<template>
    <section id="skills">
      <AnimateOnVisible name="fadeDown" :duration="1">
        <Title :title="skillsTitle" :description="skillsDescription" />
      </AnimateOnVisible>
  
      <div class="section-content">
        <div class="container-fluid">
          <div class="row d-flex flex-wrap align-items-center">
            <div class="col-md-2 m-auto pb-4" v-for="(skill, index) in skills" :key="index">
              <AnimateOnVisible name="bounce">
                <img
                  id="imgLogo"
                  class="img-responsive mx-auto d-block"
                  :src="getImgUrl(skills.img)"
                  :alt="skill.title"
                />
              </AnimateOnVisible>
            </div>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  <script>
  import Title from './Title.vue';
  import {skills} from '../portfolioData.js'; 
  
  export default {
    name: 'Skills',
    components: {
      Title,
    },
    data() {
      const defaultSkillsTitle = 'Skills';
      const defaultSkillsDescription = 'Here are my skills';
  
      return {
        skillsTitle: skills.title || defaultSkillsTitle,
        skillsDescription: skills.description || defaultSkillsDescription,
        skills: skills.items || [],
      };
    },
    methods: {
      getImgUrl(img) {
        return require(`../assets/img/logo/${img}`);
      },
    },
  };
  </script>
  
  <style scoped lang="scss">
  @import '@/styles/constants.scss';
  
  #skills {
    background-color: lighten(map-get($colors, dark), 100%);
  }
  
  @media (min-width: #{map-get($breakpoints, medium)}) {
    .section-content {
      width: 80%;
      margin: 0 auto;
    }
  }
  
  img {
    max-width: 120px;
  }
  
  .altCaption {
    color: map-get($colors, secondary);
    margin-top: 1rem;
  }
  </style>
  