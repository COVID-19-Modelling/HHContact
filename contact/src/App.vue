<template>
  <div class="main-container">
    <Board vid="visual" :model="model"/>
    <div class="btn-group" style="width: 100%">
      <a class="ctrl-btn btn btn-info w-30" @click="step">Step</a>
      <a class="ctrl-btn btn btn-primary w-40" @click="start" v-if="!isRunning">Start</a>
      <a class="ctrl-btn btn btn-secondary w-40" @click="stop" v-if="isRunning">Stop</a>
      <a class="ctrl-btn btn btn-outline-danger w-30" @click="reset">Reset</a>
    </div>
    <a class="ctrl-btn btn btn-light w-100" @click="showModal">Settings</a>
    <Settings v-if="isModalVisible" @close="closeModal"></Settings>
    <h2>Time: {{time}}</h2>
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
      isRunning: false,
      time: 0,
      timer: null,
      model: null
    };
  },
  methods: {
    _step() {
      this.time++;

      this.model.Agents.forEach(ag => {
        ag.PosX = Math.random();
        ag.PosY = Math.random();
      })
    },
    step() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timer);
      }
      this._step();
    },
    start() {
      this.isRunning = true;
      this.timer = setInterval(this._step, 1000);
    },
    stop() {
      this.isRunning = false;
      clearInterval(this.timer);
    },
    reset() {
      this.isRunning = false;
      this.time = 0;
      clearInterval(this.timer);
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
  mounted() {
    this.model = {
      Agents: []
    }

    for (let i = 0; i < 10; i++) {
      this.model.Agents.push({PosX: Math.random(), PosY: Math.random(), value: Math.ceil(Math.random() * 5)});
    }

  }
}


</script>

<style>
/* Variables */
:root {
  --col-prim: #a6dc5c;
  --col-sec: #37a35f;
  --col-txt-prim: #ffffff;
  --col-txt-sec: #c0c0c0;
  --col-txt-dark: #777777;
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
  font-size: 70%;
  overflow: hidden;
}

.main-container {
  background-color: var(--col-prim);
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
