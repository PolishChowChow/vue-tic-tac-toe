<script setup lang="ts">
import Square from "./Square.vue";
import { ref } from "vue";
let board = ref<string[]>(["", "", "", "", "", "", "", "", ""]);
let currentSign = "O";
let isWinner = false;
let moves = 0;
let titleText = "";
const setBoard = (internalIndex: number) => {
  console.log(internalIndex);
  if (board.value[internalIndex] !== "" || isWinner) {
    return;
  }
  board.value[internalIndex] = currentSign;
  moves++;
  checkWinner();
  currentSign = currentSign === "O" ? "X" : "O";
  // console.log(board);
  // console.log(moves)
};

function checkWinner() {
  if (moves === 9) {
    isWinner = true;
    titleText = "draw";
  }
  const sequences: number[][] = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  sequences.map((sequence) => {
    if (
      board.value[sequence[0]] !== "" &&
      board.value[sequence[0]] === board.value[sequence[1]] &&
      board.value[sequence[0]] === board.value[sequence[2]]
    ) {
      isWinner = true;
      titleText = `The winner is ${currentSign}`;
    }
  });
}

function restartGame() {
  board.value = ["", "", "", "", "", "", "", "", ""];
  currentSign = "O";
  isWinner = false;
  moves = 0;
  titleText = "";
}
</script>

<template>
  <h2 v-if="!isWinner">Now is turn: {{ currentSign }}</h2>
  <h2 v-if="isWinner">{{ titleText }}</h2>
  <div class="board">
    <div class="square" v-for="(square, index) in board" :key="index">
      <Square :content="square" :internalIndex="index" :handler="setBoard">
      </Square>
    </div>
  </div>
  <button @click="restartGame">Restart Game</button>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
button{
  color: white;
  border: 2px solid transparent;

  padding: 14px 10px;
  outline:none;
  margin: 30px;
}
button:hover{
  border: 2px solid white;
}
</style>
