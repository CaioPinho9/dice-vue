<template>
  <div>
    <p>mensagem</p>
    <div>
      <form id="dice-form" @submit="createDice">
        <div class="input-container">
          <label class="input-label" for="client">Nome do Cliente:</label>
          <input @focus="removeError" class="input" type="text" id="client" name="client" v-model="client" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label class="input-label" for="number">Escolha o dado:</label>
          <select @focus="removeError"  class="input" name="number" id="number" v-model="number">
            <option value="">Selecione o número de lados</option>
            <option v-for="number in numbers" :key="number.id" :value="number.tipo">{{ number.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label class="input-label" for="color">Cor:</label>
          <select @focus="removeError"  class="input" name="color" id="color" v-model="color">
            <option value="">Selecione a cor dos dados</option>
            <option v-for="color in colors" :key="color.id" :value="color.tipo">{{ color.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label class="input-label" for="material">Material:</label>
          <select @focus="removeError"  class="input" name="material" id="material" v-model="material">
            <option value="">Selecione o material do dado</option>
            <option v-for="material in materials" :key="material.id" :value="material.tipo">{{ material.tipo }}</option>
          </select>
        </div>
        <div id="optional-container" class="input-container">
          <label id="optional-title" for="optional">Opcionais:</label>
          <div class="checkbox-container" v-for="option in optionals" :key="option.id">
            <input type="checkbox" name="optional" v-model="optional" :value="option.tipo">
            <span>{{ option.tipo }}</span>
          </div>
          <label v-if="bomDia">Bom Dia</label>
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
  name: "DiceForm",
  data() {
    return {
      client: "",
      number: "",
      color: "",
      material: "",
      optionals: null,
      clients: null,
      numbers: null,
      colors: null,
      materials: null,
      optional: [],
      msg: null,
      bomDia: false
    }
  },
  methods: {
    async getDetails() {
      const req = await fetch("http://localhost:3000/details")
      const data = await req.json()

      this.numbers = data.numbers
      this.colors = data.colors
      this.materials = data.materials
      this.optionals = data.optional

    },
    checkError() {
      var check = true
      document.querySelectorAll(".input").forEach(input => {
        if (input.value == "") {
          input.setAttribute("data-error", "")
          check = false
        }

        if (input.value.includes("Selecione")) {
          input.setAttribute("data-error", "")
          check = false
        }
      })
      return check
    },
    removeError(e) {
      e.target.removeAttribute("data-error")
    },
    async createDice(e) {
      e.preventDefault()

      const data = {
        client: this.client,
        number: this.number,
        color: this.color,
        material: this.material,
        optional: Array.from(this.optional),
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)

      if (!this.checkError()) {
        return
      }

      const req = await fetch("http://localhost:3000/dices", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      })

      const res = await req.json()

      if (data.optional.includes("Bom Dia")) {
        this.bomDia = true
      } else {
        this.bomDia = false
      }

      this.client = ""
      this.number = ""
      this.color = ""
      this.material = ""
      this.optional = []
    }
  },
  mounted() {
    this.getDetails()
  }
  
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

  ::placeholder {
    color: #ff8800
  }

  input, select {
    width: 100%;
    padding: 5px 10px;
    background-color: #555;
    border: 1px solid #ff8800;
    color: #ff8800;
  }

  .input[data-error] {
    border-color: #f00;    
  }

  .input-label[data-error] {
    border-color: #f00;    
    color: #f00
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
    border: 2px solid #ff8800;
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