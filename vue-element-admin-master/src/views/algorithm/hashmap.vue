<template>
  <div class="algorithm-container">
    <h2>两数之和</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

var a = [1, 8, 11, 15]
var target = 23

var toSum = function(nums, target) {
  var map = {}

  for (let i = 0; i < nums.length; i++) {
    if (map[nums[i]] !== undefined) {
      return [map[nums[i]] + 1, i + 1]
    } else {
      map[target - nums[i]] = i
    }
  }
}

console.log('初始数组' + a)
console.log('目标值' + target)
var result = toSum(a, target)
console.log('对应的数组位置分别为' + result)

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

