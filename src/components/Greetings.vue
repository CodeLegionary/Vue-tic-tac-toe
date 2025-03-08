<template>
  <header>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h2>Who is going to be the champion today?</h2>
  </div>
  </header>
</template>


<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
})
</script>


<style scoped>
h1, h2 {
  text-align: center;
  margin: 0;
  padding: 0;
}

.green {
  margin-top: 18px;
}

h1 {
  color: rgb(0, 64, 0);
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
  font-family: 'Courier New', Courier, monospace;
  padding-top: 10px;
}

h2 {
  font-size: 1.8rem;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: rgba(12, 84, 12, 0.704);
  padding-bottom: 20px;
}

@media (min-width: 1024px) {
  .greetings h1 {
    font-size: 3.6rem;
  }

  .greetings h2 {
    font-size: 2.4 rem;

  }
}

.greetings > h2 {
  animation: fadeIn 2s ease-in-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(-15px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
