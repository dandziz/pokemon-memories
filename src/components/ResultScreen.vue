<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <button @click="onStartAgain()">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>

<style>
.screen {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: var(--dark);
  color: var(--light);
}
h1 {
  font-size: 5rem;
}
p {
  font-size: 3rem;
  margin-top: 1.5rem;
}
button {
  border: 1px solid var(--light);
  margin: 1rem;
  border-radius: 0.5rem;
  background-color: var(--dark);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: var(--font);
  color: var(--light);
  cursor: pointer;
  transition: 0.5s ease-in-out;
  padding: 1rem 1.25rem;
}
button:hover {
  background-color: var(--light);
  color: var(--dark);
  transition: 0.5s ease-in-out;
}
</style>
