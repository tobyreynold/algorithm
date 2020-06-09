<template>
  <div class="algorithm-container">
    <h2>滑动窗口</h2>
    <h2>有效括号</h2>
    <!-- <el-input v-model="input" placeholder="请输入找零金额">
      <template slot="prepend">人民币（元）：</template>
    </el-input>
    <el-input v-model="input1" placeholder="请输入面额">
      <template slot="prepend">面额数组(逗号分隔)：</template>
    </el-input>
    <el-button type="primary" @click="count">计算</el-button>
    <el-input v-model="textarea" type="textarea" :rows="2" placeholder="请输入内容" /> -->
  </div>
</template>

<script>

export default {
  data() {
    return {
    //   input: '',
    //   input1: '',
    //   textarea: ''
    }
  },
  methods: {
    // count: function() {
    //   const value = this.input
    //   const denomination = this.input1.split(',').map(Number)
    //   const coinChange = new MinCoinChange(denomination)
    //   this.textarea = coinChange.makeChange(value)
    // }
  }
}
class SlideWindows {
  constructor(coin) {
    this.coins = coin
  }

  slide(k) {
    const nums = this.coins
    const length = nums.length
    if (length === 0 || !k) return
    const window = []
    const res = []
    for (let i = 0; i < length; i++) {
    //   console.log('第' + (i + 1) + '次循环开始')
      if (window[0] !== undefined && window[0] <= i - k) {
        // console.log('前出栈：' + window.toString())
        window.shift()
      }
      while (nums[window[window.length - 1]] < nums[i]) {
        // console.log('后出栈：' + window.toString())
        window.pop()
      }
      window.push(i)
      // console.log('入栈：' + window.toString())
      if (i >= k - 1) {
        // console.log('插入坐标：' + window[0])
        // console.log('插入值：' + nums[window[0]])
        res.push(nums[window[0]])
      }
      // console.log('第' + (i + 1) + '次循环结束')
      // console.log('-------------------')
    }
    return res
  }
}

const slideWindow = new SlideWindows([1, 3, -1, -3, 5, 3, 6, 7])
console.log(slideWindow.slide(3))

var isValid = function(s) {
  const stack = []
  for (let i = 0; i < s.length; i++) {
    if (s[i] === '(' || s[i] === '[' || s[i] === '{') {
      stack.push(s[i])
    }
    if (!stack.length) return false
    if (s[i] === ')' && stack.pop() !== '(') return false
    if (s[i] === ']' && stack.pop() !== '[') return false
    if (s[i] === '}' && stack.pop() !== '{') return false
  }
  return stack.length === 0
}

var a = '([()])'
var v = isValid(a)
console.log(v)
</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

