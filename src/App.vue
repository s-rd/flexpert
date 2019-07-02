<template>
  <div id="app" class="home">

    <nav-bar/>

    <div class="playground">
      <flex-controls/>
      <flex-output/>
      <flex-preview/>
    </div>

  </div>
</template>

<script>
import NavBar from './components/NavBar'
import FlexControls from './components/FlexControls'
import FlexOutput from './components/FlexOutput'
import FlexPreview from './components/FlexPreview'

export default {
  name: 'app',
  components: {
    NavBar,
    FlexControls,
    FlexOutput,
    FlexPreview,
  },
}
</script>
