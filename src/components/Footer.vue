<template>
    <footer class="footer">
      <div>
          <font-awesome-icon class="copyright-icon" icon="copyright"/> 
          2020 {{user.name}}
          | Get this template <a href="https://github.com/hbollon/portfolio-vuejs" target="_blank">here</a> ! 
      </div>
      <SocialBar :links="links"/>
    </footer>
</template>
  
<script>
  import SocialBar from './SocialBar'
  export default {
    name: 'Footer',
    props: ['user', 'links'],
    components: {
      SocialBar
    }
  }
</script>
  