<template>
  <div class="algorithm-container">
    <h2>模拟链表</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }
class Node {
  constructor(element) {
    this.element = element
    this.next = null
  }
}

class LinkedList {
  constructor() {
    this.head = null
    this.length = 0
  }

  append(element) {
    const node = new Node(element)
    let current = null
    if (this.head == null) {
      this.head = node
    } else {
      current = this.head
      while (current.next) {
        current = current.next
      }
      current.next = node
    }
    this.length++
  }

  insert(position, element) {

  }

  removeAt(position) {
  }

  findIndex(element) {
    let current = this.head
    let index = -1
    while (current) {
      if (current.element === element) {
        return index + 1
      }
      index++
      current = current.next
    }
    return -1
  }

  remove(element) {
  }

  get size() {
    return this.length
  }

  get isEmpty() {
    return !this.length
  }

  toString() {
    let current = this.head
    let slink = ''
    while (current) {
      slink += `${current.element}-`
      current = current.next
    }
    return slink
  }
}

var s = new LinkedList()
s.append(1)
s.append(2)
s.append(3)
s.append(4)

console.log(s)
console.log(s.isEmpty)
console.log(s.size)
var index = s.findIndex(4)
console.log('在当前链表的位置为:' + index)
var st = s.toString()
console.log('当前链表链接成字符串' + st)
</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

