<template>
  <div
    class="select-box"
    :class="expandedClass"
  >
    <div class="select-box__box" @mousedown="open">
      {{ selected }}
      <span class="select-box__arrow">
        <svg width="16" height="11" viewBox="0 0 16 11" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M2 2L8 8L14 2" stroke="black" stroke-width="3"/>
        </svg>
      </span>
    </div>
    <span @click="close" class="select-box__close-area"/>
    <ul
      class="select-box__options"
      :style="expandedStyle"
    >
      <li
        v-for="option in options"
        class="select-box__option"
        :class="option === selected && 'select-box__option--selected'"
        @mouseup="select(option)"
      >
        {{ option }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'select-box',
  props: {
    options: {
      type: Array,
      required: true,
    },
    default: {
      type: String,
      required: false,
    },
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      selected: this.value,
      expanded: false,
      canMouseupClose: false,
      optionHeight: 0,
    }
  },
  mounted() {
    window.addEventListener('mouseup', this.handleMouseup)
    try {
      const singleOption = document.querySelector('.select-box__option')
      this.optionHeight = singleOption.offsetHeight
    } catch(e) {
      this.optionHeight = 63
    }
  },
  methods: {
    open() {
      this.expanded = true
      setTimeout(() => {
        this.canMouseupClose = true
      }, 250)
    },
    close() {
      this.expanded = false
      this.canMouseupClose = false
    },
    select(option) {
      if (this.canMouseupClose) {
        this.close()
        this.selected = option
        this.$emit('update:value', option)
      }
    },
    handleMouseup() {
      if (!this.expanded) return
      if (this.canMouseupClose) this.close()
    },
  },
  computed: {
    expandedClass() {
      const expanded = this.expanded && 'select-box--expanded'
      return [ expanded ]
    },
    expandedStyle() {
      const selectedIndex = this.options.findIndex(o => o === this.selected)
      return {
        top: `-${selectedIndex * this.optionHeight}px`,
      }
    },
  },
}
</script>
