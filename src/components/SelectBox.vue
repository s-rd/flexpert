<template>
  <div
    class="select-box"
    :class="expandedClass"
  >
    <div class="select-box__box" @mousedown="open">
      {{ selected }}
      <span class="select-box__arrow">
        <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="14.1px"
        	height="21.3px" viewBox="0 0 14.1 21.3" style="enable-background:new 0 0 14.1 21.3;" xml:space="preserve">
          <path class="st0" style="fill: none; stroke:#000; stroke-width:3;" d="M1.1,13.2l6,6l6-6"/>
          <path class="st0" style="fill: none; stroke:#000; stroke-width:3;" d="M13.1,8.1l-6-6l-6,6"/>
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
