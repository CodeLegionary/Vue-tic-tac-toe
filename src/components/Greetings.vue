<template>
  <header>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h2>Are you ready to make your move?</h2>
  </div>
  </header>
</template>

///////////////////////////

<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
})
</script>

<style scoped>
h1 {
  color: rgb(0, 64, 0);
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
  font-family: 'Courier New', Courier, monospace
}

h2 {
  font-size: 1.8rem;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: rgba(12, 84, 12, 0.704)
}

.greetings h1,
.greetings h2 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1 {
    font-size: 3.6rem;
  }

  .greetings h2 {
    font-size: 2.4 rem;
  }
}

.greetings {
  animation: fadeIn 2s ease-in-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(-20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

</style>
