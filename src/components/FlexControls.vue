<template>
  <div class="flex-controls">
    <tab-group :tabs="tabs" :active-tab.sync="tab">

      <!-- Container -->
      <div v-show="tab === 0" class="playground__view">
        <ul class="flex-controls__group">
          <li v-for="control in controls.general" class="flex-controls__item">
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
          <li v-for="control in controls.alignment" class="flex-controls__item">
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

      <!-- Items -->
      <div v-show="tab === 1" class="playground__view">
        <ul class="flex-controls__group">
          <li v-for="control in controls.items" class="flex-controls__item">
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

      <!-- Custom -->
      <div v-show="tab === 2" class="playground__view">
        <div class="playground__placeholder">
          <p>Click on a box in the preview section to apply custom styles to it</p>
        </div>
      </div>

    </tab-group>
  </div>
</template>

<script>
import SelectBox from './SelectBox'
import TabGroup from './TabGroup'

export default {
  name: 'flex-controls',
  components: {
    SelectBox,
    TabGroup,
  },
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      controls: {
        general: [
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
        alignment: [
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
        items: [
          {
            title: 'Basis',
            attribute: 'flex-basis',
            options: [
              '50%', '1', '2', '3', '4',
            ],
            default: '1',
            value: '2',
          },
          {
            title: 'Grow',
            attribute: 'flex-grow',
            options: [
              '0', '1', '2', '3', '4',
            ],
            default: '1',
            value: '2',
          },
          {
            title: 'Shrink',
            attribute: 'flex-shrink',
            options: [
              '0', '1', '2', '3', '4',
            ],
            default: '1',
            value: '2',
          },
        ],
      },
      tabs: [
        {
          i: 0,
          title: 'Container',
        },
        {
          i: 1,
          title: 'Items',
        },
        {
          i: 2,
          title: 'Custom',
        },
      ],
      tab: 0,
    }
  },
  mounted() {
    this.$emit('update:value', this.valueOutput)
  },
  watch: {
    controls: {
      handler(newVal, oldVal) {
        this.$emit('update:value', this.valueOutput)
      },
      deep: true,
    },
  },
  computed: {
    valueOutput() {
      let controls = {
        container: {},
        items: {},
      }
      this.controls.general.forEach(c => {
        controls.container[c.attribute] = c.value
      })
      this.controls.alignment.forEach(c => {
        controls.container[c.attribute] = c.value
      })
      this.controls.items.forEach(c => {
        controls.items[c.attribute] = c.value
      })
      return controls
    },
  },
}
</script>
