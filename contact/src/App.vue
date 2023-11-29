<template>
  <div class="main-container">
    <Board vid="visual"/>
    <div class="btn-group" style="width: 100%">
      <a class="ctrl-btn btn btn-info w-30">Step</a>
      <a class="ctrl-btn btn btn-primary w-40">Start</a>
      <a class="ctrl-btn btn btn-danger w-30">Reset</a>
    </div>

    <a class="ctrl-btn btn btn-outline-info w-100" @click="showModal">Settings</a>
    <Settings v-if="isModalVisible" @close="closeModal"></Settings>
  </div>
</template>

<script>
import Board from './components/Board.vue'
import Settings from './components/Settings.vue'

export default {
  name: 'App',
  components: {
    Board,
    Settings,
  },
  data() {
    return {
      isModalVisible: false,
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  }
}


</script>

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
  overflow: hidden;
}

.main-container {
  background-color: #9dff64;
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

a.ctrl-btn {
  font-size: 18pt;
}
</style>
