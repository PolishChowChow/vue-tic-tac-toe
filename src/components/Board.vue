<script setup lang="ts">
import Square from "./Square.vue";
import { ref } from "vue"
let board = ref<string[]>(["", "", "", "", "", "", "", "", ""]);
let currentSign = "O";
let isWinner = false;
const setBoard = (internalIndex: number) => {
    console.log(internalIndex);
    if(board.value[internalIndex]!=='' || isWinner){
        return;
    }
    board.value[internalIndex] = currentSign;
    currentSign = currentSign === "O" ? "X" : "O";
    checkWinner()
    console.log(board);
    
}
function checkWinner(){
    return undefined;
}
</script>

<template>
  <div class="board">
    <div class="square" v-for="(square, index) in board" :key="index">
      <Square :content="square" :internalIndex="index" :handler="setBoard"> </Square>
    </div>
  </div>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>
