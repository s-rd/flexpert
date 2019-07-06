<template>
  <div>

    <!-- Tab bar -->
    <ul class="playground__tab-bar">
      <li
        v-for="tab in tabs"
        class="playground__tab"
        :class="activeTab === tab.i && 'playground__tab--active'"
      >
        <a href="#" @click="setActiveTab(tab.i)">{{ tab.title }}</a>
      </li>
    </ul>

    <!-- Tabs -->
    <slot/>

  </div>
</template>

<script>
export default {
  name: 'tab-group',
  props: {
    tabs: {
      type: Array,
      required: true,
    },
    activeTab: {
      type: Number,
      required: true,
    },
  },
  methods: {
    setActiveTab(index) {
      this.$emit('update:activeTab', index)
    },
  },
}
</script>
