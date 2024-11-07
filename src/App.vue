<script>
export default {
  data() {
    return {
      count: 1,
    };
  },
  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    },
  }
};
</script>

<template>
  <main>
    <h1>Counter</h1>
    <span id="value">{{ count }}</span>
    <div>
      <button @click="decrement" id="decrement">-</button>
      <button @click="increment" id="increment">+</button>
    </div>
  </main>
</template>

<style scoped>
main {
  text-align: center;
  background-color: #333333;
  padding: 20px;
  border-radius: 20px;
}

#value {
  font-size: 50px;
}

button {
  font-size: 16px;
  margin: 0 5px;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  background-color: #555;
  color: #fff;
  padding: 10px 20px;
  transition: 0.3s ease-in-out;
}

button:hover {
  background-color: #777777;
}

button:active {
  transform: scale(0.9);
}
</style>
