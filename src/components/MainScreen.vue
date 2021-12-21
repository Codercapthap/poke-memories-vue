<template>
  <div class="screen">
    <div class="screen_block">
      <h1>POKE MEMORIES</h1>
      <h3>Select mode to start game</h3>
      <div class="actions">
        <button @click="onStart(16)">
          <span>4x4</span>
          <span>Ease</span>
        </button>
        <button @click="onStart(36)">
          <span>6x6</span>
          <span>Normal</span>
        </button>
        <button @click="onStart(64)">
          <span>8x8</span>
          <span>Hard</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks })
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

  .actions{
    display: flex;
    width: 500px;
    justify-content: space-around;
  }

  button{
    flex-basis: 30%;
    padding: 40px 0;
    margin: 0 12px;
    border-radius: 24px;
    flex: 1;
    text-align: center;
    display: flex;
    flex-direction: column;
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
  span{
    margin: auto;
  }
</style>