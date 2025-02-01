<template>
  <div class="game">
    <div class="rules">
      <h3>Rules:</h3>
      <p>1. This is a 2-player game. Each player takes turns by clicking the chosen box</p>
      <p>2. The player that is losing in the overall score begins. In case of a tie X starts first</p>
      <p>3. The first player to get 3 of their marks in a row (up, down, across, or diagonally) is the winner</p>
    </div>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <div class="status">
      <h3>Turn:</h3>
      <p>{{ currentPlayer }} is your move!</p>
      <h3>Score:</h3>
      <p>X-player Wins = {{ xWins }}</p>
      <p>O-player Wins = {{ oWins }}</p>
      <h3 v-if="winner">Player {{ winner }} is the winner&nbsp;!!! &#x1F3C6</h3>
      <button @click="resetGame">New Game</button>
    </div>
  </div>
</template>

///////////////////////

<script>

import { ref } from 'vue';

export default {
  setup() {
    const board = ref(Array(9).fill(''))
    const currentPlayer = ref('X')
    const winner = ref(null)
    const xWins = ref(0)
    const oWins = ref(0)

    function makeMove(index) {
      if (!board.value[index] && !winner.value) {
        board.value[index] = currentPlayer.value
        winner.value = checkWinner(board.value)
        if (winner.value) {
          if (winner.value === 'X') {
            xWins.value++
          } else if (winner.value === 'O') {
            oWins.value++
          }
        } else {
          currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X'
        }
      }
    }

    function resetGame() {
      board.value = Array(9).fill('')
      // Set the current player to the one with fewer wins
      if (xWins.value < oWins.value) {
        currentPlayer.value = 'X'
      } else if (oWins.value < xWins.value) {
        currentPlayer.value = 'O'
      } else {
        currentPlayer.value = 'X' // Default to 'X' if wins are equal
      }
      winner.value = null
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
      ]

      for (const combination of winningCombinations) {
        const [a, b, c] = combination
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return board[a]
        }
      }

      return null
    }

    return { board, currentPlayer, winner, xWins, oWins, makeMove, resetGame }
  }
}
</script>

///////////////////////

<style scoped>

p {
    color: rgb(68, 67, 67);
    background-color: rgba(255, 255, 255, 0.718);
    padding: 0%;

    align-items: center;
}

h3 {
    color: rgb(225, 105, 0);
    text-shadow: 2px 2px 2px aliceblue;
}


.game {
  font-family: Arial, sans-serif;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  align-items: center;
}

.rules {
  background-color: #b0ffd4;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 20px;
  height: max-content;
  margin: 0;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border: 1px solid #ccc
}

.board {
  display: grid;
  gap: 5px;
  margin: 20px auto;
  justify-content: center;
}

.cell {
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  border: 1px solid #000;
  cursor: pointer;
  background-color: #fff;
  transition: background-color 0.3s;
}

.board {
  grid-template-columns: repeat(3, 1fr); /* Adatta le colonne alla larghezza disponibile */
  gap: 5px; /* Riduci lo spazio tra le celle */
}

.cell:hover {
  background-color: #e0f7fa;
}

button {
  max-width: 100px;
  margin-top: 20px;
  padding: 10px;
  background-color: #2196f3;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
  font-weight: 600;
  font-size: 1rem;
}

button:hover {
  background-color: #1976d2;
}

.status {
  background-color: #b0ffd4;
  padding: 20px;
  border-radius: 10px;
  margin-top: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border: 1px solid #ccc
}

/* Media query for wide screens */
@media (min-width: 768px) {
  .game {
    flex-direction: row;
    justify-content: space-between; /* Distributes space evenly */
    width: 100%;
  }

  .board {
    grid-template-columns: repeat(3, 100px);
    gap: 15px;
  }

  .cell {
  width: 100px;
  height: 100px;
  }

  .rules, .board, .status {
    margin: 0 20px;
    flex: 1; /* Ensure equal space distribution */
  }
}
</style>
