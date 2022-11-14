<template>
  <div class="avatar" :style="cssVars">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Avatar',
  props: {
    size: {
      type: Number,
      default: 48
    },
    backgroundColor: {
      type: String,
      default: '#cbe2ff'
    }
  },
  computed: {
    cssVars() {
      return {
        '--size': `${this.size}px`,
        '--background-color': this.backgroundColor
      };
    }
  }
};
</script>

<style lang="scss" scoped>
.avatar {
  height: var(--size);
  width: var(--size);
  border-radius: 50%;
  background-color: var(--background-color);
  display: flex;
  align-items: center;
  justify-content: center;

  img {
    width: inherit;
    height: inherit;
    border-radius: inherit;
  }
}
</style>
