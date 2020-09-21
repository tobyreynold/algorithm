<template>
  <div class="algorithm-container">
    <!--  <h2>数组、栈、队列类型题目衍生（典型的线性结构迭代）</h2> -->
    <h3>滑动窗口</h3>
    <h3>有效括号</h3>
    <h3>完全平方数</h3>
    <h3>数组中第K大的元素</h3>
    <h3>单词接龙</h3>
    <h3>IP复原</h3>
    <h3>最长子串</h3>
    <h3>最长公共前缀</h3>
    <h3>全排列</h3>
    <h3>买卖股票的最佳时机</h3>
    <h3>买卖股票的最佳时机II</h3>
    <h3>数据去重之不开辟新空间</h3>
    <h3>盛水最多容器</h3>
    <h3>括号生成</h3>
    <h3>全排列</h3>
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
console.log(slideWindow.slide(4))

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

var isParenthesesValid = function(s) {
  var reg = /(\(\))|(\{\})|(\[\])/g
  while (s.match(reg)) {
    s = s.replace(reg, '')
  }
  return s === ''
}

var a = '()'
var v = isValid(a)
console.log(v)

var numSquares = function(n) {
  const queue = []
  const map = new Map()
  queue.push([n, 0])
  map.set(n, true)
  while (queue.length) {
    const [num, step] = queue.shift()
    for (let i = 1; ; i++) {
      const nextNum = num - i * i
      if (nextNum < 0) break
      if (nextNum === 0) return step + 1
      if (!map.get(nextNum)) {
        queue.push([nextNum, step + 1])
        map.set(nextNum, true)
      }
    }
  }
}

var cc = 18
var result = numSquares(cc)
console.log(cc + '的完全平方最少需要' + result + '步')

var getNum = function(arr, k) {
  arr.sort((a, b) => b - a)
  const uni = Array.from(new Set(arr))
  const tar = uni[k - 1]
  return tar
}
const arr = [3, 2, 3, 1, 2, 4, 5, 5, 6]
console.log(getNum(arr, 4))

var ladderlength = function(beginWord, endWord, wordList) {
  const isSimilar = (a, b) => {
    let diff = 0
    for (let i = 0; i < a.length; i++) {
      if (a.charAt(i) !== b.charAt(i)) diff++
      if (diff > 1) return false
    }
    return true
  }
  const queue = [beginWord]
  const index = wordList.indexOf(beginWord)
  if (index !== -1) wordList.splice(index, 1)
  let res = 2
  while (queue.length) {
    let size = queue.length
    while (size--) {
      const front = queue.shift()
      for (let i = 0; i < wordList.length; i++) {
        if (!isSimilar(front, wordList[i])) continue
        if (wordList[i] === endWord) {
          return res
        } else {
          queue.push(wordList[i])
        }
        wordList.splice(i, 1)
        i--
        console.log(queue)
      }
    }
    res += 1
  }
  return 0
}
var beginWord = 'hit'
var endWord = 'cog'
var wordList = ['hot', 'dot', 'dog', 'lot', 'log', 'cog']

var step = ladderlength(beginWord, endWord, wordList)
console.log('单词接龙步数：' + step)

var restoreIpAddr = function(s) {
  const backtrace = (str, start, array, res) => {
    const remainLength = str.length - start
    if (array.length === 4) {
      if (remainLength === 0) {
        res.push(array.join('.'))
      }
      return
    }
    if (remainLength > (4 - array.length) * 3) {
      return
    }
    for (let i = 1; i < str.length && i <= 3; i++) {
      const substr = str.substr(start, i)
      if (i === 3 && +substr > 255) {
        continue
      } else if (i > 1 && substr.indexOf('0') === 0) {
        continue
      } else {
        array.push(substr)
        backtrace(str, start + i, array, res)
        array.pop()
      }
    }
  }
  const res = []
  backtrace(s, 0, [], res)
  return res
}
var ip = restoreIpAddr('25525511135')
console.log(ip)

var lengthOfLongestSubstring = function(s) {
  if (s.length === 0) {
    return 0
  }
  var sArr = s.split('')
  var resArr = [sArr[0]]
  var res = 1
  var longStr = ''
  var item
  for (var i = 0; i < s.length; i++) {
    item = sArr[i]
    var indexOf = resArr.indexOf(item) /*        如果下一个字符包含在目前 的字符串中，就截取已有字符串中，从该字符串后面的。*/
    if (indexOf > -1) {
      resArr = resArr.splice(indexOf + 1)
    }
    resArr.push(item)
    // res = resArr.length > res ? resArr.length : res
    if (resArr.length > res) {
      res = resArr.length
      longStr = resArr.join('')
    }
  }
  return [res, longStr]
}

var ap = 'abcdabcbb'
var ll = lengthOfLongestSubstring(ap)
console.log(ll)

// var longestCommonPrefix = function(strs) {
//     if (strs.length === 0) {
//         return '';
//     } /*    第一个全部看成前缀*/
//     var pre = strs[0].split('');
//     strs.forEach(function(v, i) {
//         if (i == 0) {
//             return;
//         }
//         var j = 0;
//         var vArr = v.split('');
//         while (j <= vArr.length && j <= pre.length) {
//             if (vArr[j] != pre[j]) {
//                 pre = pre.slice(0, j);
//                 break;
//             }
//             j++;
//         }
//     });
//     return pre.join('');
// }

/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
  if (strs.length === 0) {
    return ''
  }

  var pre = strs[0].split('')

  for (let i = 0; i < strs.length; i++) {
    if (i === 0) {
      continue
    }
    var vArr = strs[i].split('')
    for (let j = 0; j <= vArr.length && j <= pre.length; j++) {
      if (pre[j] !== vArr[j]) {
        pre = pre.slice(0, j)
        break
      }
    }
  }
  return pre.join('')
}

var stre = ['flower', 'flow', 'flight']
var commonlong = longestCommonPrefix(stre)
console.log(commonlong)

/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var swap = function(nums, i, j) {
  const tmp = nums[i]
  nums[i] = nums[j]
  nums[j] = tmp
}

var dfs = function(result, nums, start) {
  // 出口条件
  if (start === nums.length) {
    result.push([...nums])
  }

  for (let i = start; i < nums.length; i++) {
    swap(nums, start, i) // 剩余数组中的元素，分别于剩余数组中第一个元素，交换，那么剩下的进行递归的全排列； 剩余数组会逐渐减小至没有
    dfs(result, nums, start + 1)
    // 交换回来，因为在dfs嵌套中，序列是被改变了的，所以，在返回到外一层嵌套的时候，需要将数组复位
    swap(nums, start, i)
  }
}

var permute = function(nums) {
  const result = []
  dfs(result, nums, 0)
  return result
}

var ccc = [1, 2, 3]
var alll = permute(ccc)
console.log(alll)

var maxProfit = function(price) {
  var length = price.length
  var maxpro = 0
  if (length < 2) {
    return maxpro
  }

  var min = price[0]
  for (let i = 1; i < length; i++) {
    const temp = price[i]
    if (temp <= min) {
      min = temp
    } else {
      maxpro = Math.max(temp - min, maxpro)
    }
  }
  return maxpro
}

var price = [7, 1, 5, 3, 6, 4]
var profit = maxProfit(price)
console.log('最大利润为：' + profit)

var maxProfitt = function(prices) {
  var len = prices.length
  if (len < 2) { return 0 }

  var min = prices[0]
  var profit = 0
  for (let i = 1; i < len; i++) {
    var temp = prices[i]
    var pre = prices[i - 1]
    if (temp < pre) {
      min = temp
    } else {
      profit = profit + (temp - pre)
    }
  }
  return profit
}

var pricess = [1, 2, 6, 4, 88]
var profitt = maxProfitt(pricess)
console.log('最大利润II为：' + profitt)

var removeDuplicates = function(nums) {
  var okStr = ''
  for (var i = 0; i < nums.length;) {
    const item = nums[i]
    if (okStr.match('_' + item + '_')) {
      nums.splice(i, 1)
    } else {
      okStr = okStr + '_' + item + '_'
      i++
    }
  }
  return nums.length
}

var removeDuplicate = function(nums) {
  if (!nums || !nums.length) return 0
  for (let j = 0; j < nums.length; j++) {
    if (nums[j] === nums[j + 1]) {
      nums.splice(j, 1)
      j--
    }
  }
  return nums.length
}

var ararar = [0, 3, 1, 4, 1, 2, 2, 3, 3, 4, 4]
removeDuplicates(ararar)
console.log(ararar)

var maxArea = function(height) {
  let head = 0
  let tail = height.length - 1
  let max = 0
  while (head < tail) {
    const min = Math.min(height[head], height[tail])
    max = Math.max(min * (tail - head), max)
    if (height[head] < height[tail]) {
      head++
    } else {
      tail--
    }
  }
  return max
}

var water = [1, 8, 6, 2, 5, 4, 8, 3, 7]
console.log('盛水最大体积：' + maxArea(water))

var generateParenthesis = function(n) {
  var arr = []

  function generate(cur, left, right) {
    if (cur.length === 2 * n) {
      arr.push(cur)
      return
    }
    if (left < n) {
      generate(cur + '(', left + 1, right)
    }
    if (left > right) {
      generate(cur + ')', left, right + 1)
    }
  }

  generate('', 0, 0)
  return arr
}
var parenthesis = 2
console.log(generateParenthesis(parenthesis))

var permute = function(nums) {
  const res = []
  dfs([])

  function dfs(path) {
    if (path.length === nums.length) {
      res.push([...path])
    }

    for (const num of nums) {
      if (path.includes(num)) continue
      path.push(num)
      dfs(path)
      path.pop()
    }
  }
  return res
}

var numsss = [1, 2, 3]
var ssss = permute(numsss)
console.log(ssss)

var permuteUnique = function(nums) {
  const arr = []
  const temp = []
  const global = {}

  function dfs(level) {
    const visited = {}
    if (level === nums.length) {
      arr.push([...temp])
      return
    }
    for (let i = 0; i < nums.length; i++) {
      if (!visited[nums[i]] && !global[i]) {
        temp.push(nums[i])
        global[i] = true
        visited[nums[i]] = true
        dfs(level + 1)
        global[i] = false
        temp.pop()
      }
    }
  }
  dfs(0)
  return arr
}

var numss = [1, 1, 3]
var sss = permuteUnique(numss)
console.log(sss)

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

