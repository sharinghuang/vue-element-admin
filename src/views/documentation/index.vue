<template>
  <div class="app-container documentation-container">
    <h3>Please select color:</h3>
    <v-input-colorpicker
      v-model="originInputColor"
      class="v-input-colorpicker"
      @change="handleColorPickerChange"
    />
    <el-row :gutter="32">
      <el-col :xs="24" :sm="24" :lg="6">
        <div
          :style="{ background: originInputColor }"
          class="chart-wrapper"
          @click="resetAdjustmentColor"
        />
        <chrome-picker
          v-show="false"
          ref="chromePickerOrigin"
          v-model="originInputColor"
        />
        <h3>HEX: {{ originInputColor }}</h3>
        <h3>RGB: {{ originColorRgba }}</h3>
        <h3>HSV: {{ originColorHsv }}</h3>
        <h3>HSL: {{ originColorHsl }}</h3>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="6">
        <div
          :style="{ background: adjustmentColor.hex }"
          class="chart-wrapper"
          @click="handleShowColor"
        />
        <h3>HEX: {{ adjustmentColor.hex }}</h3>
        <h3>RGB: {{ adjustmentColorRgba }}</h3>
        <h3>HSV: {{ adjustmentColorHsv }}</h3>
        <h3>HSL: {{ adjustmentColorHsl }}</h3>
      </el-col>

      <el-col :xs="24" :sm="24" :lg="10">
        <div class="chart-wrapper">
          <div v-show="colorShow">
            <chrome-picker
              ref="chromePickerAdjustment"
              v-model="adjustmentColor"
              class="chrome-picker-adjustment"
              @input="chromePickerAdjustmentInput"
            />
          </div>
        </div>
        <h3>
          Hue:
          <el-input-number
            v-model="adjustmentColor.hsl.h"
            :precision="2"
            :min="0"
            :max="360"
            @change="handleHueChange"
          />
        </h3>

        <h3>
          Saturation:
          <el-input-number
            v-model="adjustmentColor.hsl.s"
            :precision="2"
            :step="0.01"
            :max="1"
            @change="handleSaturationChange"
          />
        </h3>

        <h3>
          Lightness:
          <el-input-number
            v-model="adjustmentColor.hsl.l"
            :precision="2"
            :step="0.01"
            :min="0"
            :max="1"
            @change="handleLightnessChange"
          />
        </h3>
      </el-col>
    </el-row>
  </div>
</template>

<script>

import { Chrome } from 'vue-color'
// https://www.npmjs.com/package/tinycolor2
import tinycolor from 'tinycolor2'
export default {
  name: 'Documentation',
  components: { 'chrome-picker': Chrome },
  data() {
    return {
      originInputColor: '#194d33',
      originColor: {
        hex: '#194d33',
        hex8: '#194D33A8',
        hsl: { h: 150, s: 0.5, l: 0.2, a: 1 },
        hsv: { h: 150, s: 0.66, v: 0.30, a: 1 },
        rgba: { r: 25, g: 77, b: 51, a: 1 },
        a: 1
      },
      adjustmentColor: {
        hex: '#194d33',
        hex8: '#194D33A8',
        hsl: { h: 150, s: 0.5, l: 0.2, a: 1 },
        hsv: { h: 150, s: 0.66, v: 0.30, a: 1 },
        rgba: { r: 25, g: 77, b: 51, a: 1 },
        a: 1
      },
      countHslColor: { h: 150, s: 0.5, l: 0.2 },
      colorShow: false
    }
  },
  computed: {
    originColorRgba() {
      return this.originColor.rgba.r + '   ' + this.originColor.rgba.g + '   ' + this.originColor.rgba.b
    },
    originColorHsl() {
      return this.originColor.hsl.h.toFixed(2) + '   ' + this.originColor.hsl.s.toFixed(2) + '   ' + this.originColor.hsl.l.toFixed(2)
    },
    originColorHsv() {
      return this.originColor.hsv.h.toFixed(2) + '   ' + this.originColor.hsv.s.toFixed(2) + '   ' + this.originColor.hsv.v.toFixed(2)
    },
    adjustmentColorRgba() {
      return this.adjustmentColor.rgba.r + '   ' + this.adjustmentColor.rgba.g + '   ' + this.adjustmentColor.rgba.b
    },
    adjustmentColorHsl() {
      return this.adjustmentColor.hsl.h.toFixed(2) + '   ' + this.adjustmentColor.hsl.s.toFixed(2) + '   ' + this.adjustmentColor.hsl.l.toFixed(2)
    },
    adjustmentColorHsv() {
      return this.adjustmentColor.hsv.h.toFixed(2) + '   ' + this.adjustmentColor.hsv.s.toFixed(2) + '   ' + this.adjustmentColor.hsv.v.toFixed(2)
    }
  },
  methods: {
    handleColorPickerChange(value) {
      const chromePickerOriginData = this.$refs.chromePickerOrigin.val
      console.log('handleColorPickerChange is ', chromePickerOriginData)
      this.originColor.hex = value
      this.originColor.hsv = chromePickerOriginData.hsv
      this.originColor.hsl = chromePickerOriginData.hsl
      this.originColor.rgba = chromePickerOriginData.rgba
      this.adjustmentColor.hex = value
      this.adjustmentColor.hsv = chromePickerOriginData.hsv
      this.adjustmentColor.hsl = chromePickerOriginData.hsl
      this.adjustmentColor.rgba = chromePickerOriginData.rgba
    },
    chromePickerAdjustmentInput() {
      const chromePickerAdjustmentData = this.$refs.chromePickerAdjustment.val
      console.log('chromePickerAdjustmentInput is ', chromePickerAdjustmentData)
    },
    handleShowColor() {
      if (this.colorShow) {
        this.colorShow = false
      } else {
        this.colorShow = true
      }
    },
    resetAdjustmentColor() {
      this.adjustmentColor = this.originColor
    },
    chromePickerCountUpdate(value) {
      const chromePickerCountUpdate = this.$refs.chromePickerCount
      console.log('chromePickerCountUpdate is ', chromePickerCountUpdate)
    },
    handleHueChange(value) {
      console.log('handleHueChange is ', this)
      this.adjustmentColor.hsl.h = value
      var color = tinycolor(this.adjustmentColor.hsl)
      this.adjustmentColor.hex = color.toHexString()
      this.adjustmentColor.hex8 = color.toHex8String()
      this.adjustmentColor.rgba = color.toRgb()
      this.adjustmentColor.hsl = color.toHsl()
      this.adjustmentColor.hsv = color.toHsv()

      var chromePickerAdjustmentData = this.$refs.chromePickerAdjustment.val
      chromePickerAdjustmentData.hex = color.toHexString()
      chromePickerAdjustmentData.hex8 = color.toHex8String()
      chromePickerAdjustmentData.rgba = color.toRgb()
      chromePickerAdjustmentData.hsl = color.toHsl()
      chromePickerAdjustmentData.hsv = color.toHsv()
    },
    handleSaturationChange(value) {
      this.adjustmentColor.hsl.s = value
      var color = tinycolor(this.adjustmentColor.hsl)
      this.adjustmentColor.hex = color.toHexString()
      this.adjustmentColor.hex8 = color.toHex8String()
      this.adjustmentColor.rgba = color.toRgb()
      this.adjustmentColor.hsl = color.toHsl()
      this.adjustmentColor.hsv = color.toHsv()

      var chromePickerAdjustmentData = this.$refs.chromePickerAdjustment.val
      chromePickerAdjustmentData.hex = color.toHexString()
      chromePickerAdjustmentData.hex8 = color.toHex8String()
      chromePickerAdjustmentData.rgba = color.toRgb()
      chromePickerAdjustmentData.hsl = color.toHsl()
      chromePickerAdjustmentData.hsv = color.toHsv()
    },
    handleLightnessChange(value) {
      this.adjustmentColor.hsl.l = value
      var color = tinycolor(this.adjustmentColor.hsl)
      this.adjustmentColor.hex = color.toHexString()
      this.adjustmentColor.hex8 = color.toHex8String()
      this.adjustmentColor.rgba = color.toRgb()
      this.adjustmentColor.hsl = color.toHsl()
      this.adjustmentColor.hsv = color.toHsv()

      var chromePickerAdjustmentData = this.$refs.chromePickerAdjustment.val
      chromePickerAdjustmentData.hex = color.toHexString()
      chromePickerAdjustmentData.hex8 = color.toHex8String()
      chromePickerAdjustmentData.rgba = color.toRgb()
      chromePickerAdjustmentData.hsl = color.toHsl()
      chromePickerAdjustmentData.hsv = color.toHsv()
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
.v-input-colorpicker {
  width: 80px;
  margin-bottom: 16px;
}

.chrome-picker-adjustment {
  width: 80%;
}

.progress-bar-block {
  margin-top: 20%;
}

.chart-wrapper {
  background: #fff;
  min-height: 420px;
  padding: 16px 16px 0;
}
</style>
