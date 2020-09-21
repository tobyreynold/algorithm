<template>
  <div class="algorithm-container">
    <h2>ALL kinds of sort</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

var a = [1, 3, 6, 3, 23, 76, 1, 34, 222, 6, 456, 221, 556, 75, 30]

// eslint-disable-next-line no-extend-native
Array.prototype.bubbleSort = function() {
  for (let i = 0; i < this.length; i++) {
    for (let j = 0; j < i; j++) {
      if (this[i] < this[j]) {
        const temp = this[j]
        this[j] = this[i]
        this[i] = temp
      }
    }
  }
}

// eslint-disable-next-line no-extend-native
Array.prototype.selectSort = function() {
  let min
  for (let i = 0; i < this.length; i++) {
    min = i
    for (let j = i; j < this.length; j++) {
      if (this[min] > this[j]) {
        min = j
      }
    }

    if (min !== i) {
      const temp = this[i]
      this[i] = this[min]
      this[min] = temp
    }
  }
}

// eslint-disable-next-line no-extend-native
Array.prototype.insertSort = function() {
  for (let i = 1; i < this.length; i++) {
    let j = i
    const temp = this[i]
    while (j > 0 && this[j - 1] > temp) {
      this[j] = this[j - 1]
      j--
    }
    this[j] = temp
    console.log(this.join('，'))
  }
  return this
}

// eslint-disable-next-line no-extend-native
Array.prototype.quickSort = function() {
  const partition = (array, left, right) => {
    var pivot = array[Math.floor((right + left) / 2)]
    let j = right
    let i = left
    while (i <= j) {
      while (array[i] < pivot) {
        i++
      }
      while (array[j] > pivot) {
        j--
      }
      if (i <= j) {
        const aux = array[i]
        array[i] = array[j]
        array[j] = aux
        i++
        j--
      }
    }
    return i
  }
  const quick = (array, left, right) => {
    let index
    if (array.length > 1) {
      index = partition(array, left, right)
      if (left < index - 1) {
        quick(array, left, index - 1)
      }
      if (index < right) {
        quick(array, index, right)
      }
    }
    console.log(array.join('，'))
  }
  quick(this, 0, this.length - 1)
  return this
}

// eslint-disable-next-line no-extend-native
Array.prototype.quickSortt = function() {
  const quick = function(arr) {
    if (arr.length <= 1) { return arr }
    const pivotIndex = Math.floor(arr.length / 2)
    const pivot = arr.splice(pivotIndex, 1)[0]
    const left = []
    const right = []
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] > pivot) {
        right.push(arr[i])
      } else {
        left.push(arr[i])
      }
    }
    return quick(left).concat([pivot], quick(right))
  }
  return quick(this)
}

// eslint-disable-next-line no-extend-native
Array.prototype.mergeSort = function() {
  const merge = (right, left) => {
    const result = []
    let il = 0
    let ir = 0
    while (il < left.length && ir < right.length) {
      if (left[il] < right[ir]) {
        result.push(left[il++])
      } else {
        result.push(right[ir++])
      }
    }
    while (il < left.length) {
      result.push(left[il++])
    }
    while (ir < right.length) {
      result.push(right[ir++])
    }
    console.log(result)
    return result
  }
  const mergeSort = array => {
    if (array.length === 1) { return array }
    const mid = Math.floor(array.length / 2)
    const left = array.slice(0, mid)
    const right = array.slice(mid, array.length)
    return merge(mergeSort(left), mergeSort(right))
  }
  return mergeSort(this)
}

// eslint-disable-next-line no-extend-native
Array.prototype.binarySearch = function(item) {
  let low = 0
  let mid = null
  let element = null
  let high = this.length - 1
  while (low <= high) {
    mid = Math.floor((low + high) / 2)
    element = this[mid]
    if (item > element) {
      low = mid + 1
    } else if (item < element) {
      high = mid - 1
    } else {
      return mid
    }
  }
  return -1
}
// a.quickSort()
console.log(a)

a.insertSort()
console.log(a)
// console.log(b)
var index = a.binarySearch(556)
console.log(index)

// eslint-disable-next-line no-extend-native
Array.prototype.heap_sort = function(top) {
  var arr = this.slice(0)
  var len = arr.length
  var k
  top ? k = len - top - 1 : k = 0

  function swap(i, j) {
    var temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
  }
  function max_heapify(start, end) {
    var dad = start
    var son = dad * 2 + 1
    if (son >= end) return
    if (son + 1 < end && arr[son] < arr[son + 1]) {
      son++
    }
    if (arr[dad] <= arr[son]) {
      swap(dad, son)
      max_heapify(son, end)
    }
  }

  for (var i = Math.floor(len / 2) - 1; i >= 0; i--) max_heapify(i, len)
  for (var j = len - 1; j > k; j--) {
    swap(0, j)
    max_heapify(0, j)
  }
  return arr
}

var aaa = [12, 55, 22, 13, 14, 3, 5, 3, 0, 8, 6, 1, 5, 2, 1, 5, 2, 1, 5, 2, 9]
var top = 5
var heap = aaa.heap_sort(top)
console.log(heap)
console.log(heap[heap.length - top])

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

