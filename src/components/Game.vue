<template>
  <div class="game">
    <div class="status">
      <h2>Current MATCH:</h2>
      <h3 v-if="welcomeMessage" style="color: #35df;">{{ welcomeMessage }}</h3>
      <h3 v-else-if="!gameOverMessage">{{ currentPlayer }}, is your turn!</h3>
      <h3 v-else>{{ gameOverMessage }}</h3>
      
      <br/>
    </div>

    <Board @turn-changed="handleTurnChange" :reset="resetBoard" />

    <button class="reset" :disabled="gameOver" @click="resetMatch">New Match</button>

    <div class="status">
      <h2>GAME Scores:</h2>
      <p>Matches won by X = {{ xWins }}</p>
      <p>Matches won by O = {{ oWins }}</p>
    </div>

    <div v-if="showGameOverModal" class="modal">
      <div class="modal-content">
        <p>{{ gameOverModalMessage }}</p>
        <button @click="resetMatch">Play Again</button>
        &nbsp;
        <button @click="closeGameOverModal">Close</button>
      </div>
    </div>
  </div>
</template>



<script setup>
import { onMounted, ref } from 'vue';
import Board from './Board.vue';

const currentPlayer = ref('X');
const winner = ref(null);
const xWins = ref(0);
const oWins = ref(0);
const gameOverMessage = ref(null);
const resetBoard = ref(false);
const welcomeMessage = ref(null);

// Refs per il modale di fine partita
const showGameOverModal = ref(false);
const gameOverModalMessage = ref('');
const gameOver = ref(false); // Flag per la fine della partita

onMounted(() => {
  welcomeMessage.value = `Player ${currentPlayer.value} starts the game!`;
  setTimeout(() => {
    welcomeMessage.value = null;
  }, 2000);
});

function handleTurnChange(newPlayer, newWinner, board) {
  currentPlayer.value = newPlayer;
  winner.value = newWinner;

  if (newWinner === 'X') {
    xWins.value++;
    gameOverMessage.value = `Player ${newWinner} is the winner!!! 🏆`;
  } else if (newWinner === 'O') {
    oWins.value++;
    gameOverMessage.value = `Player ${newWinner} is the winner!!! 🏆`;
  } else if (newWinner === "tie") {
    gameOverMessage.value = "It's a tie!";
  }

  if (newWinner) {
    gameOver.value = true; // Imposta gameOver a true
    setTimeout(() => {
      gameOverModalMessage.value = newWinner === "tie" ? "It's a tie! Do you want to play again?" : `Player ${newWinner} has won! Do you want to play again?`;
      showGameOverModal.value = true;
      gameOver.value = false;
    }, 600);
  }
}

function closeGameOverModal() {
  showGameOverModal.value = false;
}

function resetMatch() {
  gameOver.value = false; // Imposta gameOver a false
  currentPlayer.value = 'X';
  winner.value = null;
  gameOverMessage.value = null;
  resetBoard.value = true;
  setTimeout(() => {
    resetBoard.value = false;
  }, 100);
  closeGameOverModal(); // Chiudi il modale quando la partita viene resettata
}
</script>



<style>
h2 {
  color: rgb(40, 30, 51);
}

h2:last-of-type {
  margin-top: 1px;
  margin-bottom: 1px;
}

p {
  margin: 8px;
  font-size: 1.2rem;
}

h3 {
  color: rgb(0, 64, 0);
  text-shadow: white 3px 3px;
  margin-bottom: 5px;
}

.game {
  background-color: #c0ffe770;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin: 0;
  padding: 0;
  height: 100%;
}
/*ad hoc query .game related (small screens)*/
@media (max-width: 620px) {
  .game {
    justify-content: space-around;
  }
}

.status {
  margin-top: 1px;
  text-align: center;
}

.status:first-of-type > h2 {
  margin-top: 10px;
}

.status p[v-if="welcomeMessage"] {
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 10px;
}

.reset {
  padding: 10px 20px;
  margin-top: 20px;
  cursor: pointer;
  font-size: 16px;
  background-color: rgb(147, 255, 219);
  margin: 10px;
  border-radius: 5px;
}

button:hover {
    background-color: rgb(175, 253, 229);
}

/* Stili per il modale */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
}
</style>