<template>
  <div id="app">
    <Greetings msg="Welcome to Tic-Tac-Toe!" />
    <div id="container">
      <Rules />
      <Game />
      <History />
    </div>
  </div>
</template>



<script setup>
import Game from './components/Game.vue';
import Greetings from './components/Greetings.vue';
import History from './components/History.vue';
import Rules from './components/Rules.vue';
</script>


// Mobile First Approach Style

<style scoped>
#app {
  text-align: center;
}

p {
  font-size: 40;
}

#container {
  display: flex;
  flex-direction: column;
  margin-top: 0;
  justify-content: center;
  align-items: center;
}

#container > div {
  flex-grow: 1;     /* Makes the components grow to fill available space */
  flex-shrink: 0;   /* Prevents the components from shrinking */
  flex-basis: 0;    /* Sets the initial main size of a flex item */
  padding: 10px;    /* adds padding around the content */
  box-sizing: border-box; /* Ensures padding is included in the width calculation */
  width: 100%;      /* Makes the components take up the full width */
  align-items: center;
}

/* Media queries for larger screens */

@media (min-width: 520px) {
  #container {
    flex-direction: row;
  }

  #container > div {
    height: 830px;
  }
}

@media (min-width: 560px) {
  #container > div {
    line-height: 1.4;
  }
}

@media (min-width: 620px) {
  #container > div {
    height: 600px;
    line-height: 1.2;
  }
}

@media (min-width: 720px) {
  #container > div {
    height: 530px;
    line-height: 1.3;
  }
}

@media (min-width: 820px) {
  #container > div {
    line-height: 1.4;
  }
}
</style>
