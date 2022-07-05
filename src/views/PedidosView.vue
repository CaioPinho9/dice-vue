<template>
  <div class="main-container">
    <h1>Gerenciar Pedidos</h1>
    <Dashboard />
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue'

export default {
  name: "PedidosView",
  components: {
    Dashboard
  }
}
</script>

<style scoped>
  h1 {
    color: #fff;
    text-shadow: 3px 3px 10px #ff8800;
    font-size: 60px;
    margin: 50px;
  }

  #html, body, #app, .main-container {
    height: 71.8vh;
  }

</style>
