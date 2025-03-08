<template>
  <h2>&#x2694;&#x2b55; ARENA </h2>
  <div class="board">
    <div v-for="(cell, index) in board" :key="index" class="cell" :class="{ 'played': cell !== '' }" @click="makeMove(index)">
      <span :class="{ 'o-player': cell === 'O' }">{{ cell }}</span>
    </div>
  </div>
</template>


<script setup>
import { ref, watch } from 'vue';

const board = ref(Array(9).fill(''));
const currentPlayer = ref('X');
const winner = ref(null);
const props = defineProps(['reset']);
const emit = defineEmits(['turn-changed']);

function makeMove(index) {
  if (!board.value[index] && !winner.value) {
    board.value[index] = currentPlayer.value;
    winner.value = checkWinner(board.value);
    if (!winner.value) {
      currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X';
    }
    emit('turn-changed', currentPlayer.value, winner.value, board.value);
  }
}

function checkWinner(board) {
  const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];

  for (const combination of winningCombinations) {
    const [a, b, c] = combination;
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a];
    }
  }

  if (board.every(cell => cell)) {
    return 'tie';
  }

  return null;
}

watch(
  () => props.reset,
  (newVal) => {
    if (newVal) {
      board.value = Array(9).fill('');
      currentPlayer.value = 'X';
      winner.value = null;
    }
  }
);
</script>


<style scoped>
.o-player {
  color: rgb(244, 0, 0);
}

h2 {
  margin-bottom: 0;
  margin-top: 0;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;
}

.cell {
  width: 55px;
  height: 55px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  cursor: pointer;
  border-radius: 2px;
  background-color: rgba(255, 255, 255, 0.982)
}

.cell:hover {
  background-color: #e0f7fa;
}

.cell.played {
  cursor: default;
}
</style>