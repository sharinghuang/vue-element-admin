<template>
  <div class="app-container documentation-container">
    <el-color-picker
      v-model="color"
      size="small"
      show-alpha
      :predefine="predefineColors"
      @change="colorChange"
    />
    <el-row :gutter="32">
      <el-col :xs="24" :sm="24" :lg="6">
        <div class="chart-wrapper">
          <div class="color-block" :style="{ background: color }" />

          <div class="color-block-tips">
            <li style="padding: 6px">RGB: {{ color }}</li>
            <li style="padding: 6px">HEX:</li>
            <li style="padding: 6px">HSV:</li>
            <li style="padding: 6px">Lab:</li>
            <li style="padding: 6px">CMYK:</li>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="6">
        <div class="chart-wrapper">
          <div class="color-block" :style="{ background: color }" />

          <div class="color-block-tips">
            <li style="padding: 6px">RGB: {{ color }}</li>
            <li style="padding: 6px">HEX:</li>
            <li style="padding: 6px">HSV:</li>
            <li style="padding: 6px">Lab:</li>
            <li style="padding: 6px">CMYK:</li>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="10">
        <div class="chart-wrapper">
          <div class="progress-bar-block">
            <p>深度调整</p>
            <el-slider
              v-model="progressValueA"
              style="padding: 8px"
              show-input
            />

            <p>色向调整</p>
            <el-slider
              v-model="progressValueB"
              style="padding: 8px"
              show-input
            />

            <p>饱和度调整</p>
            <el-slider
              v-model="progressValueC"
              style="padding: 8px"
              show-input
            />
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>

export default {
  name: 'Documentation',
  components: {},
  data() {
    return {
      progressValueA: 10,
      progressValueB: 20,
      progressValueC: 30,
      color: 'rgba(255, 69, 0, 1)',
      predefineColors: [
        '#ff4500',
        '#ff8c00',
        '#ffd700',
        '#90ee90',
        '#00ced1',
        '#1e90ff',
        '#c71585',
        'rgba(255, 69, 0, 0.68)',
        'rgb(255, 120, 0)',
        'hsv(51, 100, 98)',
        'hsva(120, 40, 94, 0.5)',
        'hsl(181, 100%, 37%)',
        'hsla(209, 100%, 56%, 0.73)'
      ]
    }
  },
  methods: {
    colorChange(a) {
      console.log(this)
      console.log(a)
    }
  }
}
</script>

<style lang="scss" scoped>
.documentation-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;
}
.color-block-tips {
  width: 80%;
  margin: auto;
  padding-top: 16px;
  padding-bottom: 16px;
}
.progress-bar-block {
  margin-top: 20%;
}
.color-block {
  height: 320px;
  width: 80%;
  margin: auto;
}

.chart-wrapper {
  background: #fff;
  min-height: 480px;
  padding: 16px 16px 0;
}
</style>
