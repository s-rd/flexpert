<template>
  <div class="flex-output">
    <tab-group :tabs="tabs" :active-tab.sync="tab">
      <div v-show="tab === 0">
        No CSS output yet ¯\_(ツ)_/¯
      </div>
      <div v-show="tab === 1">
        <pre><code>.container {{ input.container }}

.item {{ input.items }}

#item-1 {
     flex: 1;
}</code>
        </pre>
      </div>
    </tab-group>
  </div>
</template>

<script>
import TabGroup from './TabGroup'

export default {
  name: 'flex-ouput',
  props: {
    input: {
      type: Object,
      required: true,
    },
  },
  components: {
    TabGroup,
  },
  data() {
    return {
      tabs: [
        {
          i: 0,
          title: 'CSS Output',
        },
        {
          i: 1,
          title: 'SCSS Output',
        },
      ],
      tab: 1,
    }
  },
  computed: {
    sassOutput() {
      return ''
    },
  },
}
</script>
