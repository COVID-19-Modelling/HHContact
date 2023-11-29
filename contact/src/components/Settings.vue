<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <h3>Parameter settings</h3>
            <button
              type="button"
              class="btn-close"
              @click="$emit('close')"
            >
            </button>
          </div>
          <div class="modal-body">
            <div v-for="(par, i) in parameters" :key="i">
              <p>{{par.name}}</p>

            </div>
          </div>

          <div >
            <a class="btn btn-danger btn-block w-100 btn-apply" @click="$emit('apply')">
              Apply
            </a>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Settings',
  props: {
    parameters: {
      type: Array,
      default() {
        return [
          {name: 'a', desc: 'Parameter A', value: 0.3},
          {name: 'b', desc: 'Parameter B', value: 5},
        ]
      }
    }
  },
  methods: {
    close() {
      this.$emit('close');
    },
  },
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  max-width: 80%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.5s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.btn-apply {
  font-size: 18pt;
}
</style>