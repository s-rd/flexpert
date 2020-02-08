<template>
  <nav class="nav-bar">

    <a href="#" class="nav-bar__logo">Flexpert</a>
    <h3 class="nav-bar__slogan">CSS Flexbox Playground</h3>
    <a href="https://twitter.com/kvasimon" target="_blank" class="nav-bar__link">@kvasimon</a>

    <div class="nav-bar__mobile-note" v-if="showNote">
      <p>
        This thing works on virtually any modern device, but it'll
        probably be more valuable on a device with a larger display.
        <a class="nav-bar__mobile-close" @click="closeNote">Sure, whatever</a>
      </p>
    </div>

  </nav>
</template>

<script>
export default {
  name: 'nav-bar',
  data() {
    return {
      showNote: true,
    }
  },
  mounted() {
    this.detectShowNote()
  },
  methods: {
    closeNote() {
      this.showNote = false
      localStorage.setItem('mobileNote', false)
    },
    detectShowNote() {
      if (localStorage.getItem('mobileNote')) {
        this.showNote = JSON.parse(localStorage.getItem('mobileNote'))
      } else {
        this.showNote = true
        localStorage.setItem('mobileNote', true)
      }
    },
  },
}
</script>
