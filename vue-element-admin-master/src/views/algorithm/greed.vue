<template>
  <div class="algorithm-container">
    <h2>贪心算法之找零钱</h2>
    <el-input v-model="input" placeholder="请输入找零金额">
      <template slot="prepend">人民币（元）：</template>
    </el-input>
    <el-input v-model="input1" placeholder="请输入面额">
      <template slot="prepend">面额数组(逗号分隔)：</template>
    </el-input>
    <el-button type="primary" @click="count">计算</el-button>
    <el-input v-model="textarea" type="textarea" :rows="2" placeholder="请输入内容" />
  </div>
</template>

<script>

export default {
  data() {
    return {
      input: '',
      input1: '',
      textarea: ''
    }
  },
  methods: {
    count: function() {
      const value = this.input
      const denomination = this.input1.split(',').map(Number)
      const coinChange = new MinCoinChange(denomination)
      this.textarea = coinChange.makeChange(value)
    }
  }
}
class MinCoinChange {
  constructor(coin) {
    this.coins = coin
  }

  makeChange(target) {
    const change = []
    let total = 0
    this.coins.sort((a, b) => b - a).forEach(coin => {
      while ((total + coin) <= target) {
        change.push(coin)
        total += coin
      }
    })
    return change.toString()
  }
}

// const coinChange = new MinCoinChange([1, 2, 5, 10, 20, 50, 100])
// console.log(coinChange.makeChange(159))
</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

