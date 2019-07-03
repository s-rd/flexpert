<template>
  <div class="select-box">
    <div class="select-box__box">
      {{ options[0] }}
      <span class="select-box__arrow">
        <svg width="16" height="11" viewBox="0 0 16 11" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M2 2L8 8L14 2" stroke="black" stroke-width="3"/>
        </svg>
      </span>
    </div>
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
  },
  data() {
    return {

    }
  },
}
</script>
