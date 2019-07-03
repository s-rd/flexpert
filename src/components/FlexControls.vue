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
  </div>
</template>

<script>
export default {
  name: 'flex-controls',
  data() {
    return {
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
  computed: {
    activeTab() {
      return this.tabs[this.activeTabId]
    },
  },
}
</script>
