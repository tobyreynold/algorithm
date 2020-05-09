<template>
  <div class="algorithm-container">
    <h2>模拟队列</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

class Queue {
  constructor() {
    this.items = []
  }

  enqueue(element) {
    this.items.push(element)
  }

  shift() {
    return this.items.shift()
  }

  get size() {
    return this.items.length
  }

  get isEmpty() {
    return !this.items.length
  }

  clear() {
    this.items = []
  }

  print() {
    console.log(this.items.toString())
  }
}

var s = new Queue()
s.enqueue(1)
s.enqueue(2)
s.enqueue(3)
s.enqueue(4)

console.log(s)
console.log(s.isEmpty)
console.log(s.size)
s.print()
s.shift()
s.shift()
s.shift()
s.shift()
console.log(s.size)
console.log(s.isEmpty)
</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

