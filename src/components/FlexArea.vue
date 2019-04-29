<template>
  <div class="flex-area">
    <ul class="flex-area__box-group">
      <li class="flex-area__box" v-for="i in 5">
        {{ i }}
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
