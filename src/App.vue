<template>
  <div id="app">
    <Greetings msg="Welcome to Tic-Tac-Toe!" />
    <TheGame />
  </div>
</template>

///////////////////////////

<script setup>
import Greetings from './components/Greetings.vue';
import TheGame from './components/TheGame.vue'; /* PartiallyEnd: #3632/scriptSetup.vue */
</script>

///////////////////////////

<style scoped>
#app {
  text-align: center;
}
</style>
