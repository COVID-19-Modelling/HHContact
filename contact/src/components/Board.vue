<template>
  <div class="vis-board">
    <svg :id="vid"></svg>
  </div>
</template>
<script>

export default {
  props: {
    vid: {
      type: String,
      required: true
    }
  }
}

</script>
<style>
.vis-board {
  width: 100%;
  box-shadow: 0 0.5rem 2rem -1rem rgba(0, 0, 0, 0.1);
  border-radius: 1rem;
  grid-column: 1 / -1;
  align-self: center;
  display: grid;
  align-content: start;
  background-color: #e03131;
  gap: 0.2rem;
  aspect-ratio: 1;
}

</style>