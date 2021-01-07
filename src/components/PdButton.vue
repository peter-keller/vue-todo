<template>
  <button
    :class="buttonClasses"
    :disabled="disabled"
    @click="handleClick"
  >
    <slot />
  </button>
</template>

<script>

export default {
  name: 'PdButton',

  props: {
    disabled: {
      type: Boolean,
      default: false
    },

    displayStyle: {
      type: String,
      default: 'standard'
    }
  },

  computed: {
    buttonClasses () {
      return [
        'pd-button',
        `pd-button__${this.displayStyle}`,
        {
          'pd-button--disabled': this.disabled
        }
      ]
    }
  },

  methods: {
    handleClick() {
      if (this.disabled) return

      this.$emit('click')
    }
  }
}
</script>

<style scoped>
.pd-button {
  border: 0;
  height: 100%;
  width: 48px;
  color: white;
  font-size: 28px;
}

.pd-button__standard {
  background-color: var(--btn-add-bg-color);
}

.pd-button__alert {
  background-color: var(--btn-delete-bg-color);
}

.pd-button--disabled {
  background-color: var(--btn-disabled-bg-color);
}
</style>
