<template>
  <Message :msg="msg" :normal="normal" v-show="msg" />
  <div id="burger-table">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#</div>
        <div>Cliente:</div>
        <div>Número:</div>
        <div>Cor:</div>
        <div>Material:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="dice in dices" :key="dice.id">
        <div class="order-number">{{ dice.id }}</div>
        <div>{{ dice.client }}</div>
        <div>{{ dice.number }}</div>
        <div>{{ dice.color }}</div>
        <div>{{ dice.material }}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in dice.optional" :key="index">{{ opcional }}</li>
          </ul>
        </div>
        <div id="select">
          <select name="status" class="status" @change="updateDice($event, dice.id)">
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="dice.status == s.tipo">{{ s.tipo }}</option>
          </select>
          <button class="delete-btn" @click="deleteDice(dice.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue"

export default {
  name: "DashBoard",
  data() {
    return {
      dices: null,
      dice_id: null,
      status: [],
      normal: true,
      msg: null
    }
  },
  components: {
    Message
  },
  methods: {
    async getDetails() {
      const req = await fetch("http://localhost:3000/dices")

      const data = await req.json()

      this.dices = data

      this.getStatus()
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status")

      const data = await req.json()

      this.status = data
    },
    async deleteDice(id) {
      const req = await fetch('http://localhost:3000/dices/'+id, {
        method: "DELETE"
      })
      
      const res = await req.json()

      this.getDetails()
      
      this.msg = "O pedido Nº"+id+" foi cancelado com sucesso"
      setTimeout(() => this.msg = "", 5000)
    },
    async updateDice(event, id) {
      const option = event.target.value

      const dataJson = JSON.stringify({ status: option })

      const req = await fetch('http://localhost:3000/dices/'+id, {
        method: "PATCH",
        headers: { "Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json()

      this.msg = "O pedido Nº"+id+" foi atualizado para \""+option+"\" com sucesso"
      setTimeout(() => this.msg = "", 5000)

    }
  },
  mounted() {
    this.getDetails()
  }
}
</script>

<style scoped>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
  }

  #burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #222;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 15%;
  }

  .burger-table-row #select {
    width: 19%;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ff8800;
  }

  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select,
  .delete-btn {
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

  select {
    padding: 10px;
    padding-left: 4px;
    padding-right: 0px;
    margin-right: 6px;
    font-weight: 100;
    width: 56%;
  }

  .delete-btn:hover {
    background-color: #ff8800;
    border: 2px solid #ff8800;
    color: #fff;
  }

  ul {
    list-style-type: none;
  }

  
</style>