<template>
  <div class="flex-preview">
    <ul class="playground__tab-bar">
      <li class="playground__tab boxes">
        <a href="#">
          {{ boxes }} boxes
          <span @click.prevent="addBox" class="add" :class="{ 'add--disabled': !canAdd }">+</span>
          <span @click.prevent="removeBox" class="remove" :class="{ 'remove--disabled': !canRemove }">-</span>
        </a>
      </li>
      <li class="playground__tab playground__tab--active">
        <a href="#">Preview</a>
      </li>
    </ul>
    <div class="flex-preview__content" :style="properties">
      <div v-for="(box, index) in boxes" class="flex-preview__box">
        {{ index + 1 }}
        <span @click="removeBox" class="close">x</span>
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
