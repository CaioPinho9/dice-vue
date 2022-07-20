<template>
  <div id="main-banner">
    <div>
      <h1>Dice Forge</h1>
      <!--Runa escrito Dice Forge-->
      <h1 id="runa">&#5854;&#5825;&#5811;&#5846; &#5792;&#5801;&#5809;&#5815;&#5846;</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Banner"
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Runic&display=swap');
  
  #main-banner {
    background-image: url('/public/img/dice.png');
    background-position: 0-100px;
    background-size: cover;
    height: 600px;
    margin: -50px;
    margin-bottom: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  h1 {
    color: #fff;
    text-shadow: 3px 3px 10px #ff8800;
    font-size: 70px;
    margin: 0px;
  }

  #runa {
    font-family: 'Noto Sans Runic', sans-serif;
    font-size: 55px;
  }

</style>