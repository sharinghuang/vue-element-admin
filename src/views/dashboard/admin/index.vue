<template>
  <el-container style="height: 500px; border: 2px solid #eee">
    <el-aside>
      <el-menu :default-openeds="['1', '2']">
        <el-submenu index="1">
          <template slot="title"><i class="el-icon-menu" />供应商色卡</template>
          <el-menu-item
            v-for="colorCard in colorCards"
            :key="colorCard.id"
            :title="colorCard.name"
            @click="handleColorCardClick(colorCard)"
          >
            {{ colorCard.name }}
          </el-menu-item>
        </el-submenu>
        <el-submenu index="2">
          <template slot="title"><i class="el-icon-menu" />自定义色卡</template>
          <el-menu-item
            v-for="customerColorCard in customerColorCards"
            :key="customerColorCard.id"
            :title="customerColorCard.name"
            @click="handleCustomerColorCardClick(customerColorCard)"
          >{{ customerColorCard.name }}</el-menu-item>
        </el-submenu>
        <el-submenu index="3" />
      </el-menu>
    </el-aside>
    <el-main>
      <h3>当前色卡: {{ selectColorBlockName }}</h3>
      <div class="color-block-root">
        <div
          v-for="(item, index) in colorBlocks"
          :key="index"
          class="color-block"
          :style="{ background: item.color }"
          @click="colorBlockClick(item)"
        />
      </div>
    </el-main>
  </el-container>
</template>

<script>
var colorCardData1 = [
  { color: '#000' },
  { color: '#001' },
  { color: '#002' },
  { color: '#003' },
  { color: '#004' },
  { color: '#005' },
  { color: '#006' },
  { color: '#007' },
  { color: '#008' },
  { color: '#008' },
  { color: '#010' },
  { color: '#011' },
  { color: '#012' },
  { color: '#013' },
  { color: '#014' },
  { color: '#015' },
  { color: '#016' },
  { color: '#017' },
  { color: '#018' },
  { color: '#019' },
  { color: '#020' },
  { color: '#021' },
  { color: '#022' },
  { color: '#023' },
  { color: '#024' },
  { color: '#025' }
]

var colorCardData2 = [
  { color: '#400' },
  { color: '#401' },
  { color: '#402' },
  { color: '#403' },
  { color: '#404' },
  { color: '#405' },
  { color: '#406' },
  { color: '#407' },
  { color: '#408' },
  { color: '#408' },
  { color: '#410' },
  { color: '#411' },
  { color: '#412' },
  { color: '#413' },
  { color: '#414' },
  { color: '#415' },
  { color: '#416' },
  { color: '#417' }
]

var colorCustomerCardData1 = [
  { color: '#600' },
  { color: '#601' },
  { color: '#602' },
  { color: '#603' },
  { color: '#604' },
  { color: '#605' },
  { color: '#606' },
  { color: '#607' },
  { color: '#608' },
  { color: '#608' },
  { color: '#610' },
  { color: '#611' },
  { color: '#612' },
  { color: '#613' },
  { color: '#614' },
  { color: '#615' },
  { color: '#616' },
  { color: '#617' }
]

var colorCustomerCardData2 = [
  { color: '#300' },
  { color: '#301' },
  { color: '#302' },
  { color: '#303' },
  { color: '#304' },
  { color: '#305' },
  { color: '#306' },
  { color: '#307' },
  { color: '#308' },
  { color: '#308' },
  { color: '#310' },
  { color: '#311' },
  { color: '#312' },
  { color: '#313' },
  { color: '#314' },
  { color: '#315' },
  { color: '#316' },
  { color: '#317' }
]

export default {
  name: 'DashboardAdmin',

  components: {},

  data() {
    return {
      selectColorBlockName: '请先选择',
      colorBlocks: [],
      colorCards: [
        {
          id: '1',
          name: 'PANTONE光面铜版纸C色板'
        },
        {
          id: '2',
          name: 'RAL-K7劳尔经典色板'
        }
      ],
      customerColorCards: [
        {
          id: '1',
          name: '春季项目色卡集'
        },
        {
          id: '2',
          name: '秋季项目色卡集'
        }
      ]
    }
  },
  computed: {},

  methods: {
    handleCustomerColorCardClick(val) {
      console.log('handleCustomerColorCardClick val is ', val)
      if (val.id === 1) {
        this.colorBlocks = colorCustomerCardData1
      } else {
        this.colorBlocks = colorCustomerCardData2
      }
      this.selectColorBlockName = val.name
    },
    handleColorCardClick(val) {
      console.log('handleColorCardClick val is  ', val)
      if (val.id === 1) {
        this.colorBlocks = colorCardData1
      } else {
        this.colorBlocks = colorCardData2
      }
      this.selectColorBlockName = val.name
    },
    colorBlockClick(val) {
      console.log('colorBlockClick val is  ', val)
    }
  }
}
</script>

<style lang="scss" scoped>
.el-aside {
  width: 320px;
  min-height: 500px;
  background-color: transparent;
}
.color-block {
  width: 50px;
  height: 50px;
  margin: 16px;
}
.color-block-root {
  display: flex;
  flex-wrap: wrap;
}
</style>
