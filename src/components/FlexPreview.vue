<template>
  <div class="flex-preview">
    <ul class="playground__tab-bar">
      <li class="playground__tab boxes">
        <a href="#">
          {{ boxes }} boxes
          <span @click.prevent="addBox" class="add">+</span>
          <span @click.prevent="removeBox" class="remove">-</span>
        </a>
      </li>
      <li class="playground__tab playground__tab--active">
        <a href="#">Preview</a>
      </li>
    </ul>
    <div class="flex-preview__content" :style="properties">
      <div v-for="(box, index) in boxes" class="flex-preview__box">
        {{ index + 1 }}
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
    }
  },
  methods: {
    addBox() {
      this.boxes += 1
    },
    removeBox() {
      this.boxes -= 1
    },
  },
}
</script>
