<script setup>
import Board from './components/Board.vue'
</script>

<template>
  <div class="main-container">
    <Board/>
  </div>
</template>

<style>
/* Variables */
:root {
  --col-prim: #91dd2e;
  --col-sec: #37a35f;
  --col-food-apple: #e03131;
  --col-light-grey: #f3f3f3;
  --col-txt-prim: #ffffff;
  --col-txt-sec: #c0c0c0;
  --col-txt-dark: #444444;
}

/* Global styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  touch-action: manipulation;
  user-select: none;
}

html {
  font-size: 62.5%;
  overflow: hidden;
}

.main-container {
  background-color: #535bf2;
  height: 100dvh;
  margin: auto;
  padding: 2rem;
  max-width: 70rem;

  display: flex;
  flex-direction: column;
  gap: 2rem;
}
.main-container > * {
  min-width: 0;
}
</style>
