<template>
  <div class="dashboard-editor-container"> home page </div>
</template>

<script>

export default {
  name: 'DashboardAdmin',

  components: { },

  data() {
    return { color: '#409EFF' }
  },

  methods: { }
}
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;
}

@media (max-width: 1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>
