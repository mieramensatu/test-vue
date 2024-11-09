<script setup>
import { ref } from "vue";

const showForm = ref(false);
const newMemo = ref("");
const memos = ref([]);
const error = ref("");

function addMemo() {
  if (newMemo.value === "") {
    error.value = "Please enter a memo";
    return;
  }
  memos.value.push({
    id: Date.now(),
    content: newMemo.value,
    date: new Date().toLocaleString("en-us"),
    backgroundColor: getRandomColor(),
  });
  newMemo.value = "";
  showForm.value = false;
}

function getRandomColor() {
  return `#${Math.floor(Math.random() * 16777215).toString(16)}`;
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1 class="header-title">memo</h1>
        <button @click="showForm = true" class="header-button">+</button>
      </header>
      <div class="card-container">
        <div
          v-for="(memo, index) in memos"
          :key="index"
          class="card"
          :style="{ backgroundColor: memo.backgroundColor }"
        >
          <p class="card-content">
            {{ memo.content }}
          </p>
          <p>{{ memo.date }}</p>
        </div>
      </div>
    </div>
    <div v-if="showForm" class="form-overlay">
      <div class="form-modal">
        <button @click="showForm = false" class="form-close-btn">
          &times;
        </button>
        <p v-if="error" class="form-error">{{ error }}</p>
        <textarea
          v-model="newMemo"
          name="memo"
          id="memo"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addMemo" class="form-save-btn">save</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 900px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
header .header-title {
  color: gray;
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 3rem;
}

header .header-button {
  cursor: pointer;
  border: transparent;
  border-radius: 100%;
  height: 50px;
  width: 50px;
  padding: 10px;
  background-color: cornflowerblue;
  color: white;
}

.card {
  width: 225px;
  height: 225px;
  padding: 10px;
  background-color: #ffa6c1;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.form-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-modal {
  width: 420px;
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.form-save-btn {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: #495a7d;
  border: none;
  border-radius: 5px;
  color: white;
  cursor: pointer;
  margin-top: 20px;
  box-shadow: 0 0 10px #495a7d;
  font-weight: bold;
  transition: all 0.2s ease;
  outline: none;
}
.form-save-btn:hover {
  background-color: #516393;
  box-shadow: 0 0 10px #516393;
  transform: scale(1.03);
  transition: all 0.2s ease;
  outline: none;
}

.form-close-btn {
  position: absolute;
  top: 0;
  right: 0;
  width: 30px;
  height: 30px;
  background-color: transparent;
  border: none;
  font-size: 25px;
  cursor: pointer;
}
.form-error{
  color: red;
}
</style>
