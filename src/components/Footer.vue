<template>
    <footer class="footer">
      <div>
          <p>Copyright</p>
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
  