<template>
  <div
    class="circular-progress"
    :style="{ ...loaderSize, ...loaderWidth }"
  ></div>
</template>

<script>
export default {
  name: 'CircularProgress',
  props: {
    size: {
      type: Number,
      default: 3
    },
    width: {
      type: Number,
      default: 3
    }
  },
  computed: {
    loaderSize() {
      return { width: `${this.size * 10}px`, height: `${this.size * 10}px` };
    },
    loaderWidth() {
      return {
        borderWidth: `${this.width}px`,
        borderTopWidth: `${this.width}px`
      };
    }
  }
};
</script>

<style lang="scss" scoped>
.circular-progress {
  border: 5px solid #eee; /* Light grey */
  border-top: 5px solid #3498db; /* Blue */
  border-radius: 50%;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
