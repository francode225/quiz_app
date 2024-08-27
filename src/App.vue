<script setup lang="ts">
import quizCard from './components/quizCard.vue'
</script>

<template>
  <div class="container">
    <quiz-card />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap');
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Merriweather', serif;
}

.container {
  width: 100%;
  height: 100vh;
  background: #f79d00;
  background: -webkit-linear-gradient(to right, #f78000, #24fa36);
  background: linear-gradient(to right, #f78000, #24fa36);
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
