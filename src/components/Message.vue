<template>
  <div v-if="normal" class="message-container" id="normal">
    <p> {{ msg }} </p>
  </div>
  <div v-else-if="success" class="message-container" id="success">
    <p> {{ msg }} </p>
  </div>
  <div v-else class="message-container" id="fail">
    <p> {{ msg }} </p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
    success: Boolean,
    normal: Boolean
  }
}
</script>

<style>
  .message-container {
    background-color: #333;
    border-radius: 10px;
    padding: 10px;
    max-width: 500px;
    width: fit-content;
    margin: 30px auto;
  }

  #normal {
    border: 4px solid #1496de;
    color: #1496de;
  }

  #success {
    border: 4px solid rgb(0, 141, 0);
    color: rgb(0, 141, 0);
  }

  #fail {
    border: 4px solid #f00;
    color: #f00;
  }
</style>