<template>
    <div>
      <Nav />
      <nuxt />
      <Footer />
    </div>
</template>
<script>
import Footer from '../components/Footer.vue'
export default {
  components: { Footer },
  head: {
    titleTemplate: 'MyApps',
  },
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Almarai:wght@300;400;700;800&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css');
@import url('~/assets/scss/style.scss');

html {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
  
}
body {
  margin: 0;
  font-family: 'Almarai', sans-serif;
  line-height: 2;
  height: 100%;
  text-align: right;
  direction: rtl;
  overflow-x: hidden
}
h1, h2, h3, h4, h5, h6{
  font-weight: 600;
}
</style>
