<script setup>
import { ref } from "vue";
const showform = ref(false);
const memo = ref("");
const memos = ref([]);
const error = ref("");

function addMemo() {
  if (!memo.value) {
    error.value = "Mohon Isi Form terlebih dahulu";
    return;
  }

  memos.value.push({
    id: Date.now(),
    memo: memo.value,
    date: new Date().toLocaleDateString("en-GB"),
    bg: `#${Math.floor(Math.random() * 16777215).toString(16)}`,
  });

  memo.value = "";
  showform.value = false;
}

function deletecard(id) {
  memos.value = memos.value.filter((memo)=>memo.id !== id)
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1 class="title">memo</h1>
        <button class="button" @click="showform = true">+</button>
      </header>
      <div class="card-container">
        <div v-for="(memo, index) in memos" :key="index" class="card" :style="{ backgroundColor: memo.bg }">
          <p>{{ memo.memo }}</p>
          <div class="card-footer">
            <p class="card-date">{{ memo.date }}</p>
            <button @click="deletecard(memo.id)">x</button>
          </div>
        </div>

      </div>
    </div>

    <div v-if="showform" class="form-overlay">
      <div class="form-modal">
        <button class="close" @click="showform = false">&times;</button>
        <p v-if="!memo" class="error">{{ error }}</p>
        <textarea v-model="memo" name="memo" id="memo" cols="30" rows="10"></textarea>
        <button @click="addMemo" class="save">Simpan</button>
      </div>
    </div>
  </main>
</template>

<style scope>
.container {
  max-width: 90%;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 25px;
  color: #495a7d;
}

.button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  border-radius: 100%;
  background-color: #495a7d;
  color: white;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
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

.form-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.077);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.form-modal {
  width: 420px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.save {
  margin-top: 15px;
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: #495a7d;
  border: none;
  cursor: pointer;
  border-radius: 15px;
  color: white;
}

.close {
  position: absolute;
  top: 5px;
  right: 10px;
  width: 30px;
  height: 30px;
  background-color: transparent;
  border: none;
  font-size: 25px;
  cursor: pointer;
}

.error {
  color: red;
}

.card-footer{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>