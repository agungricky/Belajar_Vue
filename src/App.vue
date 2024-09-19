<script setup>
import { ref } from 'vue';

    const count =  ref(0);

    function tambah() {
      count.value++
    }

    function kurang() {
      count.value--
    }
</script>

<template>
  <main>
    <div>
      <h1>Counter</h1>
      <span id="value">{{ count }}</span>
      <div>
        <button @click="tambah">+</button>
        <button @click="kurang">-</button>
      </div>
    </div>
  </main>
</template>

<!-- Scoped : digunakan agar css ini hanya diload untuk tampilan ini bukan global -->
<style scoped>

main{
    text-align: center;
    background-color: #333333;
    padding: 20px;
    border-radius: 8px;
}

#value{
    font-size: 50px;
}

button{
    font-size: 16px;
    margin: 0 5px;
    background-color: #555555;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 4px;
}
</style>