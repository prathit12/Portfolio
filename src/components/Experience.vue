<template>
    <section id="experience">
      <AnimateOnVisible name="fadeDown" :duration="1">
        <Title
          class="title"
          :title="content.metadata.title"
          :description="content.metadata.description"
        />
      </AnimateOnVisible>
  
      <AnimateOnVisible name="fadeUp" :duration="1">
          <div class="container-fluid">
              <div class="row">
                  <ExperienceColumn
                      :posts="content.metadata.academic"
                      title="Education"
                      class="col-12 col-md left"
                  />
                  <ExperienceColumn
                      :posts="content.metadata.professional"
                      title="Professional"
                      class="col-12 col-md right"
                  />
              </div>
          </div>
      </AnimateOnVisible>
    </section>
</template>
  
<script>
import Title from "./Title.vue";
import ExperienceColumn from "./ExperienceColumn.vue";

export default {
  name: "Experience",
  props: ["content"],
  components: {
    Title,
    ExperienceColumn,
  }
};
</script>
  