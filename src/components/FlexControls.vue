<template>
  <div class="flex-controls">
    <ul class="playground__tab-bar">
      <li
        v-for="tab in tabs"
        class="playground__tab"
        :class="activeTabId === tab.id && 'playground__tab--active'"
      >
        <a href="#" @click="setactivetab(tab.id)">{{ tab.title }}</a>
      </li>
    </ul>
    <ul class="flex-controls__group">
      <li v-for="control in generalControls" class="flex-controls__item">
        <div class="flex-controls__item-content">
          <h3 class="flex-controls__item-title">{{ control.title }}</h3>
          <h4 class="flex-controls__item-attribute">{{ control.attribute }}</h4>
        </div>
        <select-box
          :options="control.options"
          :default="control.default"
          :value.sync="control.value"
        />
      </li>
    </ul>
    <ul class="flex-controls__group">
      <h2 class="flex-controls__group-title">Alignment</h2>
      <li v-for="control in alignmentControls" class="flex-controls__item">
        <div class="flex-controls__item-content">
          <h3 class="flex-controls__item-title">{{ control.title }}</h3>
          <h4 class="flex-controls__item-attribute">{{ control.attribute }}</h4>
        </div>
        <select-box
          :options="control.options"
          :default="control.default"
          :value.sync="control.value"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import SelectBox from './SelectBox'

export default {
  name: 'flex-controls',
  components: {
    SelectBox,
  },
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      generalControls: [
        {
          title: 'Direction',
          attribute: 'flex-direction',
          options: [
            'row', 'row-reverse', 'column', 'column-reverse',
          ],
          default: 'row',
          value: 'column',
        },
        {
          title: 'Wrap',
          attribute: 'flex-wrap',
          options: [
            'nowrap', 'wrap', 'wrap-reverse',
          ],
          default: 'nowrap',
          value: 'wrap',
        },
      ],
      alignmentControls: [
        {
          title: 'Horizontal',
          attribute: 'justify-content',
          options: [
            'flex-start', 'flex-end', 'center', 'space-around', 'space-between',
          ],
          default: 'flex-start',
          value: 'center',
        },
        {
          title: 'Vertical',
          attribute: 'align-items',
          options: [
            'stretch', 'baseline', 'center', 'flex-start', 'flex-end',
          ],
          default: 'stretch',
          value: 'stretch',
        },
        {
          title: 'Vertical (rows)',
          attribute: 'align-content',
          options: [
            'stretch', 'center', 'flex-start', 'flex-end', 'space-around', 'space-between',
          ],
          default: 'stretch',
          value: 'stretch',
        },
      ],
      tabs: [
        {
          id: 1,
          title: 'container',
        },
        {
          id: 2,
          title: 'items',
        },
        {
          id: 3,
          title: 'custom',
        },
      ],
      activeTabId: 1,
    }
  },
  methods: {
    setActiveTab(id) {
      this.activeTabId = id
    },
  },
  mounted() {
    this.$emit('update:value', this.valueOutput)
  },
  watch: {
    generalControls: {
      handler(newVal, oldVal) {
        this.$emit('update:value', this.valueOutput)
      },
      deep: true,
    },
    alignmentControls: {
      handler(newVal, oldVal) {
        this.$emit('update:value', this.valueOutput)
      },
      deep: true,
    },
  },
  computed: {
    activeTab() {
      return this.tabs[this.activeTabId]
    },
    valueOutput() {
      let controls = {}
      this.generalControls.forEach(c => {
        controls[c.attribute] = c.value
      })
      this.alignmentControls.forEach(c => {
        controls[c.attribute] = c.value
      })
      return controls
    },
  },
}
</script>
