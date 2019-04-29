<template>
  <div id="app" class="home">
    <nav-bar/>
    <search-box/>
    <flex-area/>
  </div>
</template>

<script>
import NavBar from './components/NavBar'
import SearchBox from './components/SearchBox'
import FlexArea from './components/FlexArea'

export default {
  name: 'app',
  components: {
    NavBar,
    SearchBox,
    FlexArea,
  },
}
</script>
