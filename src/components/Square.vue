<script setup lang="ts">
const { content, internalIndex, handler } = defineProps<{
  content: string;
  internalIndex: number;
  handler: (internalIndex: number) => void;
}>();
const onClickHandler = (_: Event) => {
  handler(internalIndex);
};
</script>

<template>
  <div class="square" @click="onClickHandler">
    {{ content }}
  </div>
</template>

<style scoped>
.square {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  width: 100px;
  height: 100px;
  font-size: 40px;
  border: 1px solid white;
  transition: .1s all ease-in-out;
}
.square:hover{
  background-color: #555;
  cursor: pointer;
}
</style>
