<template>
    <section id="projects">
      <AnimateOnVisible name="fadeDown" :duration="1">
          <Title
          class="title"
          :title="content.metadata.title"
          :description="content.metadata.description"
          />
      </AnimateOnVisible>
  
      <div class="container-fluid center-block">
        <article class="content text-center">
          <AnimateOnVisible class="timeline mx-auto" v-for="(post, index) in content.metadata.items" :key="index" name="fadeLeft" :duration="0.5">
              <vue-timeline-update
          :date="new Date(post.date)"
          :title="post.title"
          :description="post.content"
          :thumbnail="getImgUrl(post.image)"
          :color="post.color"
          :category="post.tag"
          icon="code"
        />
          </AnimateOnVisible>
        </article>
      </div>
    </section>
</template>
  
<script>
  import Title from "./Title.vue";
  
  export default {
    name: "Projects",
    props: ['content'],
    components: {
      Title
    },
    methods: {
      getImgUrl(img) {
        if(img == undefined || img == "")
          return ""
        return require('../assets/img/projects/'+img)
      },
    },
  };
</script>
  