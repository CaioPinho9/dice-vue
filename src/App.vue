<template>
  <NavBar :logo="logo_src" :alt="logo_alt" />
  <router-view/>
  <Footer />
</template>

<script>
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    NavBar,
    Footer
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Dice Forge"
    }
  }
}
</script>

<style>
  * {
    font-family: Arial;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #fff;
  }

  body {
    background-color: #152238;
  }


</style>
