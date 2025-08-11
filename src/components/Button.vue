<template>
  <button :class="buttonClasses" :disabled="disabled" @click="handleClick">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    label: {
      type: String,
      required: true,
    },
    color: {
      type: String,
      default: 'primary', // Bootstrap colors
    },
    size: {
      type: String,
      default: 'medium',
      validator: (value) => ['small', 'medium', 'large'].includes(value),
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    style: {
      type: String,
      default: 'filled',
      validator: (value) => ['outlined', 'filled'].includes(value),
    },
  },
  emits: ['click'],
  methods: {
    handleClick(event) {
      if (!this.disabled) {
        this.$emit('click', event)
      }
    },
  },
  computed: {
    buttonClasses() {
      const sizeMap = {
        small: 'btn-sm',
        medium: '',
        large: 'btn-lg',
      }

      const styleClass =
        this.style === 'outlined' ? `btn-outline-${this.color}` : `btn-${this.color}`

      return ['btn', styleClass, sizeMap[this.size]].join(' ').trim()
    },
  },
}
</script>
