<template>
  <div class="flex-preview">
    <ul class="playground__tab-bar">
      <li class="playground__tab boxes">
        <a>
          {{ boxes }} items
          <span @click.prevent="addBox" class="add" :class="{ 'add--disabled': !canAdd }">+</span>
          <span @click.prevent="removeBox" class="remove" :class="{ 'remove--disabled': !canRemove }">-</span>
        </a>
      </li>
      <li class="playground__tab playground__tab--active">
        <a href="#">Preview</a>
      </li>
    </ul>
    <div
      class="flex-preview__content"
      :style="properties.container"
    >
      <div
        v-for="(box, index) in boxes"
        class="flex-preview__box"
        :style="properties.items"
      >
        {{ index + 1 }}
        <span @click="removeBox" class="flex-preview__box-close">
          <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="14.1px"
          	height="14.1px" viewBox="0 0 14.1 14.1" style="enable-background:new 0 0 14.1 14.1;" xml:space="preserve">
            <path class="st0" style="fill:none;stroke-width:3;" d="M1.1,1.1l6,6l6-6"/>
            <path class="st0" style="fill:none;stroke-width:3;" d="M13.1,13.1l-6-6l-6,6"/>
          </svg>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'flex-preview',
  props: {
    properties: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      boxes: 6,
      maxBoxes: 50,
      minBoxes: 1,
    }
  },
  methods: {
    addBox() {
      if (this.canAdd) this.boxes += 1
    },
    removeBox() {
      if (this.canRemove) this.boxes -= 1
    },
  },
  computed: {
    canAdd() {
      return this.boxes !== this.maxBoxes
    },
    canRemove() {
      return this.boxes !== this.minBoxes
    },
  },
}
</script>
