<template>
  <section id="experience">
    <AnimateOnVisible name="fadeDown" :duration="1">
      <Title class="title"/>
    </AnimateOnVisible>

    <AnimateOnVisible name="fadeUp" :duration="1">
      <div class="container-fluid">
        <div class="row">
          <ExperienceColumn
            :posts="content.content"
            class="col-12 col-md left"
          />
          <ExperienceColumn
            :posts="experience ? experience.year : []"
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
  props: ["experience", "content"],
  components: {
    Title,
    ExperienceColumn,
  },
};
</script>

<style scoped lang="scss">
  @import "@/styles/constants.scss";

  $linear: map-get($colors, dark);

  #experience {
    background-color: lighten(map-get($colors, primary), 5%);
  }

  .title {
    color: map-get($colors, light);
  }

  .row {
    padding-top: 20px;
    text-align: center;
  }

  @media (min-width: #{map-get($breakpoints, small)}) {
    .left {
      text-align: right;
      border-right: 2px solid $linear;
    }
    .right {
      text-align: left;
    }
  }

  @media (max-width: #{map-get($breakpoints, small)}) {
    .right {
      margin-top: 20px;
    }
    .left:before {
      content : "";
      position: absolute;
      left    : 20%;
      bottom  : 0;
      height  : 2px;
      width   : 60%;
      border-bottom: 2px solid $linear;
    }
  }

  /* Adjusted selector for scoped styling */
  ::v-deep .text-wrapper {
    &:after {
      border-bottom: 1px solid map-get($colors, dark);
    }
  }
</style>
