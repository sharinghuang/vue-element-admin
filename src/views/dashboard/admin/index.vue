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
        <el-popover
          v-for="(item, index) in colorBlocks"
          :key="index"
          ref="popover"
          class="color-block"
          placement="top"
          trigger="click"
        >
          <p>选中的颜色是 {{ item.color }}</p>
          <div style="text-align: right; margin: 0">
            <el-button
              v-show="false"
              size="mini"
              type="text"
              @click="addFavourite(item, index)"
            >收藏</el-button>
            <el-button
              v-show="false"
              size="mini"
              type="text"
              @click="addOrderList(item, index)"
            >加入清单</el-button>
            <el-button
              type="mini"
              size="text"
              @click="adjustmentColor(item, index)"
            >调整</el-button>
          </div>
          <el-button
            slot="reference"
            class="button-color-block"
            :style="{ background: item.color }"
            @click="handleButtonColorblockClick(item)"
          />
        </el-popover>
      </div>
    </el-main>
  </el-container>
</template>

<script>
import axios from 'axios'

var colorCardData1 = [
  { color: '#517061' },
  { color: '#001000' },
  { color: '#002000' },
  { color: '#003000' },
  { color: '#004000' },
  { color: '#005000' },
  { color: '#006000' },
  { color: '#007000' },
  { color: '#008000' },
  { color: '#008000' },
  { color: '#010000' },
  { color: '#011000' },
  { color: '#012000' },
  { color: '#013000' },
  { color: '#014000' },
  { color: '#015000' },
  { color: '#016000' },
  { color: '#017000' },
  { color: '#018000' },
  { color: '#019000' },
  { color: '#020000' },
  { color: '#021000' },
  { color: '#022000' },
  { color: '#023000' },
  { color: '#024000' },
  { color: '#025000' }
]

var colorCardData2 = [
  { color: '#517000' },
  { color: '#401000' },
  { color: '#402000' },
  { color: '#403000' },
  { color: '#404000' },
  { color: '#405000' },
  { color: '#406000' },
  { color: '#407000' },
  { color: '#408000' },
  { color: '#408000' },
  { color: '#410000' },
  { color: '#411000' },
  { color: '#412000' },
  { color: '#413000' },
  { color: '#414000' },
  { color: '#415000' },
  { color: '#416000' },
  { color: '#417000' }
]

var colorCustomerCardData1 = [
  { color: '#600000' },
  { color: '#601000' },
  { color: '#602000' },
  { color: '#603000' },
  { color: '#604000' },
  { color: '#605000' },
  { color: '#606000' },
  { color: '#607000' },
  { color: '#608000' },
  { color: '#608000' },
  { color: '#610000' },
  { color: '#611000' },
  { color: '#612000' },
  { color: '#613000' },
  { color: '#614000' },
  { color: '#615000' },
  { color: '#616000' },
  { color: '#617000' }
]

var colorCustomerCardData2 = [
  { color: '#300000' },
  { color: '#301000' },
  { color: '#302000' },
  { color: '#303000' },
  { color: '#304000' },
  { color: '#305000' },
  { color: '#306000' },
  { color: '#307000' },
  { color: '#308000' },
  { color: '#308000' },
  { color: '#310000' },
  { color: '#311000' },
  { color: '#312000' },
  { color: '#313000' },
  { color: '#314000' },
  { color: '#315000' },
  { color: '#316000' },
  { color: '#317000' },
  { color: '#310000' },
  { color: '#311000' },
  { color: '#312000' },
  { color: '#313000' },
  { color: '#314000' },
  { color: '#315000' },
  { color: '#316000' },
  { color: '#317000' }
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

  created() {
    this.initColorData()
  },

  methods: {
    initColorData() {
      console.log('fetchColorCardList is start ')
      // 请求的URL地址
      var url = 'http://mo.movingtech.online:7890'
      // 要提交到服务器的数据
      var dataObj = { GetAllColors: '0' }
      // 调用axios.post()发起POST请求
      axios.defaults.withCredentials = true
      axios.post(url, dataObj).then(function(res) {
        console.log(res.data)
      })
    },

    handleCustomerColorCardClick(val) {
      console.log('handleCustomerColorCardClick val is ', val)
      if (val.id === '1') {
        this.$data.colorBlocks = colorCustomerCardData1
      } else {
        this.$data.colorBlocks = colorCustomerCardData2
      }
      this.selectColorBlockName = val.name
    },
    handleColorCardClick(val) {
      console.log('handleColorCardClick val is  ', val)
      if (val.id === '1') {
        this.colorBlocks = colorCardData1
      } else {
        this.colorBlocks = colorCardData2
      }
      this.selectColorBlockName = val.name
    },
    addFavourite(val, index) {
      this.$refs.popover[index].showPopper = false
    },
    addOrderList(val, index) {
      console.log('addOrderList val is  ', val)
      this.$refs.popover[index].showPopper = false
    },
    adjustmentColor(val, index) {
      console.log('adjustmentColor val is  ', val)
      this.$refs.popover[index].showPopper = false
      // 跳转到adjustment 界面
      this.$router.push({
        path: '/documentation/index',
        query: { adjustPushColor: val.color }
      })
    },
    handleButtonColorblockClick(val) {}
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
.button-color-block {
  width: 50px;
  height: 50px;
}
.color-block-root {
  display: flex;
  flex-wrap: wrap;
}
</style>
