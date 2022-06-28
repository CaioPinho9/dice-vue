<template>
  <div class="main-container">
    <Banner />
    <h1>Forje seu Dado:</h1>
    <DiceForm />
  </div>
</template>

<script>
// @ is an alias to /src

import Banner from '../components/Banner.vue'
import DiceForm from '../components/DiceForm.vue'

export default {
  name: 'HomeView',
  components: {
    Banner,
    DiceForm
}
}
</script>

<style scoped>
  h1 {
      text-shadow: 2px 2px 7px #1496de;
  }
</style>
