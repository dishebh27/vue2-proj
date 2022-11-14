<template>
  <div
    class="checkbox-container"
    :class="disabled && 'disabled'"
    @click="toggleCheckbox"
  >
    <input type="checkbox" :disabled="disabled" :checked="value" />
    <GoldcastText
      v-if="label"
      :color="labelColor"
      :fontSize="14"
      :textAlign="'left'"
      >{{ label }}</GoldcastText
    >
  </div>
</template>

<script>
import GoldcastText from '../components/core/GoldcastText.vue';

export default {
  name: 'Checkbox',
  components: { GoldcastText },
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    value: {
      type: Boolean,
      required: true
    },
    label: {
      type: String,
      default: ''
    },
    labelColor: {
      type: String,
      default: '#000'
    }
  },
  methods: {
    toggleCheckbox(e) {
      if (this.disabled) return;
      this.$emit('change', e);
    }
  }
};
</script>

<style lang="scss" scoped>
.checkbox-container {
  display: flex;
  align-items: center;
  gap: 5px;
  cursor: pointer;
  position: relative;
  width: fit-content;
  font-weight: 400;
  opacity: 1;

  input {
    accent-color: #1867c0;
    height: 16px;
    width: 16px;
    cursor: pointer;
  }
}

.checkbox-container.disabled {
  cursor: not-allowed !important;
  opacity: 0.38;
  input {
    cursor: not-allowed !important;
  }
}
</style>
