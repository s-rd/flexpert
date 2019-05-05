<template>
  <div class="flex-area">
    <!-- <span class="flex-area__placeholder">Flex playground</span> -->
    <ul class="flex-area__box-group">
      <li class="flex-area__box" v-for="i in 5">
        <span>{{ i }}</span>
      </li>
    </ul>
    <div class="flex-area__controls">

    </div>
  </div>
</template>

<script>
export default {
  name: 'flex-area',
  data () {
    return {
    }
  }
}
</script>
