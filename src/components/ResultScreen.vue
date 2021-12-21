<template>
  <div class="screen">
    <div class="screen_block">
      <h1>✨Congratulation✨</h1>
      <h3>{{ Math.round(timer / 1000) }} seconds</h3>
      <button @click="onStartAgain">Start Again</button>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      timer: {
        type: Number,
        required: true,
      }
    },
    methods: {
      onStartAgain(){
        this.$emit("onStartAgain")
      }
    }
  }
</script>

<style scoped>
  .screen{
    display: flex;
    height: 100vh;
    background-color: var(--dark);
  }
  .screen_block{
    margin: auto;
    color: var(--light);
    text-align: center;
  }
  .screen_block h1{
    font-size: 50px;
  }
  .screen_block h3{
    margin-bottom: 24px;
  }
  
  button{
    padding: 6px 24px;
    border-radius: 12px;
    background-color: var(--dark);
    color: var(--light);
    border: 1px solid var(--light);
    cursor: pointer;
    transition: all ease-in 0.2s;
  }

  button:hover{
    background-color: var(--light);
    color: var(--dark);
  }
</style>