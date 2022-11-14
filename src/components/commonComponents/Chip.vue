<template>
  <div
    class="chip"
    :style="{ backgroundColor, borderRadius: `${borderRadius}px` }"
  >
    <GoldcastText :color="textColor" fontWeight="bold" :fontSize="12">
      {{ label }}
    </GoldcastText>
    <img
      v-if="allowClose"
      src="https://dp3k82tjmkfj0.cloudfront.net/assets/close.svg"
      @click="closeChip"
    />
  </div>
</template>

<script>
import GoldcastText from '../components/core/GoldcastText';

export default {
  name: 'Chip',
  components: { GoldcastText },
  props: {
    label: {
      type: String,
      default: 'Chip Component'
    },
    borderRadius: {
      type: Number,
      default: 4
    },
    allowClose: {
      type: Boolean,
      default: false
    },
    textColor: {
      type: String,
      default: 'rgba(0, 0, 0, 0.87)'
    },
    backgroundColor: {
      type: String,
      default: '#e0e0e0'
    }
  },
  methods: {
    closeChip() {
      this.$emit('closeChip');
    }
  }
};
</script>

<style lang="scss" scoped>
.chip {
  padding-top: 5px;
  padding-bottom: 5px;
  padding-left: 12px;
  padding-right: 12px;
  display: flex;
  align-items: center;
  width: fit-content;
  cursor: inherit;
  gap: 10px;

  img {
    cursor: pointer;
    height: 18px;
    width: 18px;
  }
}
</style>
