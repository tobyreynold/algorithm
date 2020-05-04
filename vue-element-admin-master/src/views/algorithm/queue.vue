<template>
  <div class="algorithm-container">
    <h2>模拟队列</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

class Stack {
  constructor() {
    this.items = []
  }

  push(element) {
    this.items.push(element)
  }

  pop() {
    return this.items.pop()
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

var s = new Stack()
s.push(1)
s.push(2)
s.push(3)
s.push(4)

console.log(s)
console.log(s.isEmpty)
console.log(s.size)
s.print()
s.pop()
s.pop()
s.pop()
s.pop()
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

