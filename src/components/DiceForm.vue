<template>
  <div>
    <p>mensagem</p>
    <div>
      <form id="dice-form">
        <div class="input-container">
          <label for="client">Nome do Cliente:</label>
          <input type="text" id="client" name="client" v-model="client" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="numero">Escolha o dado:</label>
          <select name="numero" id="numero" v-model="numero">
            <option value="">Selecione o número de lados</option>
            <option value="2">2</option>
          </select>
        </div>
        <div class="input-container">
          <label for="color">Cor:</label>
          <select name="color" id="color" v-model="color">
            <option value="">Selecione a cor dos dados</option>
            <option value="blue">Azul</option>
          </select>
        </div>
        <div class="input-container">
          <label for="client">Material:</label>
          <select name="material" id="material" v-model="material">
            <option value="">Selecione o material do dado</option>
            <option value="2">2</option>
          </select>
        </div>
        <div id="optional-container" class="input-container">
          <label id="optional-title" for="optional">Opcionais:</label>
          <div class="checkbox-container">
            <input type="checkbox" name="opcionais" v-model="opcionais" value="Bolsa de Dados">
            <span>Bolsa de Dados</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Forjar">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "DiceForm"
}
</script>

<style scoped>
  #dice-form {
    max-width: 400px;
    margin: 0 auto;
    padding: 10px;
    background-color: #333;
    border: 4px solid #ff8800;
    border-radius: 10px;
    color: #ff8800;
}

  .input-container{
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    padding: 5px 10px;
    border-left: 4px solid #ff8800;
  }

  input, select {
    width: 100%;
    padding: 5px 10px;
    background-color: #555;
    border: 1px solid #ff8800;
    color: #ff8800;
  }

  #optional-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #optional-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container input, span {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;

  }

  .submit-btn {
    background-color: #222;
    color: #ff8800;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: #ff8800;
    border: 2px solid #ff8800;
    color: #fff;
  }
</style>