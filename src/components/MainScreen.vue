<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <p>Select mode to start game</p>
    <div class="action">
      <button class="choose-level" @click="onStart(4)">
        <span>2x2</span>
        <span>Super Easy</span>
      </button>
      <button class="choose-level" @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button class="choose-level" @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
    </div>
    <div class="action">
      <button class="choose-level" @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button class="choose-level" @click="onStart(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-size: 4.5rem;
  color: var(--light);
}
p {
  font-size: 2rem;
}
.screen {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: var(--light);
  background-color: var(--dark);
}
.action {
  display: flex;
  margin-top: 2rem;
}
button {
  border: 1px solid var(--light);
  margin: 0 1rem;
  width: 40%;
  border-radius: 1rem;
  background-color: var(--dark);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: var(--font);
  color: var(--light);
  cursor: pointer;
  transition: 0.5s;
}
button::before {
  content: "";
  display: block;
  padding-top: 20%;
}
button span:first-child {
  font-size: 2rem;
}
button span:last-child {
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
button:hover {
  background-color: var(--light);
  color: var(--dark);
  transition: 0.5s;
}
</style>
