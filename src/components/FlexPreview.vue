<template>
  <div class="flex-preview">
    <ul class="playground__tab-bar">
      <li class="playground__tab playground__tab--active">
        <a href="#">Preview</a>
      </li>
    </ul>
    <div class="flex-preview__content">
      <div v-for="(box, index) in boxes" class="flex-preview__box">
        {{ index + 1 }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'flex-preview',
  data() {
    return {
      boxes: 5,
    }
  },
}
</script>
