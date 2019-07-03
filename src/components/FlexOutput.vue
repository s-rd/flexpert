<template>
  <div class="flex-output">
    <ul class="playground__tab-bar">
      <li
        v-for="tab in tabs"
        class="playground__tab"
        :class="activeTabId === tab.id && 'playground__tab--active'"
      >
        <a href="#" @click="setactivetab(tab.id)">{{ tab.title }}</a>
      </li>
    </ul>

    <pre>
<code>.container {
     flex-direction: row;
     flex-wrap: nowrap;
     justify-content: center;
     align-items: center;
     align-content: center;
}

.child {
     flex: 0 1 auto;
}

#child-1 {
     flex: 1;
}</code>
    </pre>
  </div>
</template>

<script>
export default {
  name: 'flex-ouput',
  data() {
    return {
      tabs: [
        {
          id: 1,
          title: 'CSS Output',
        },
        {
          id: 2,
          title: 'Sass output',
        },
      ],
      activeTabId: 2,
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
