<template>
  <div class="algorithm-container">
    <h2>二叉排序树</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

class Node {
  constructor(element) {
    this.element = element
    this.left = null
    this.right = null
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null
  }

  insert(element) {
    const temp = new Node(element)
    var insertNode = function(root, node) {
      if (node.element > root.element) {
        if (root.right === null) {
          root.right = node
        } else {
          insertNode(root.right, node)
        }
      } else {
        if (root.left === null) {
          root.left = node
        } else {
          insertNode(root.left, node)
        }
      }
    }
    if (!this.root) {
      this.root = temp
    } else {
      insertNode(this.root, temp)
    }
  }

  inOrderTraverse(callback) {
    const inOrderTraverseNode = (node, callback) => {
      if (node !== null) {
        inOrderTraverseNode(node.left, callback)
        callback(node.element)
        inOrderTraverseNode(node.right, callback)
      }
    }
    inOrderTraverseNode(this.root, callback)
  }

  preOrderTraverse(callback) {
    const preOrderTraverseNode = (node, callback) => {
      if (node !== null) {
        callback(node.element)
        preOrderTraverseNode(node.left, callback)
        preOrderTraverseNode(node.right, callback)
      }
    }
    preOrderTraverseNode(this.root, callback)
  }

  postOrderTraverse(callback) {
    const postOrderTraverseNode = (node, callback) => {
      if (node !== null) {
        postOrderTraverseNode(node.left, callback)
        postOrderTraverseNode(node.right, callback)
        callback(node.element)
      }
    }
    postOrderTraverseNode(this.root, callback)
  }

  levelOrderTraverse(callback) {
    const levelOrder = (node, callback) => {
      const queue = []
      const result = []
      queue.push(node)
      let pointer = 0
      while (pointer < queue.length) {
        const cnode = queue[pointer++]
        result.push(cnode.element)
        callback(cnode.element)
        cnode.left && queue.push(cnode.left)
        cnode.right && queue.push(cnode.right)
      }
      return result
    }
    return levelOrder(this.root, callback)
  }

  min() {
    const minNode = node => {
      return node ? (node.left ? minNode(node.left) : node) : null
    }
    return minNode(this.root)
  }

  max() {
    const maxNode = node => {
      return node ? (node.right ? maxNode(node.right) : node) : null
    }
    return maxNode(this.root)
  }

  search(key) {
    const searchNode = (node, key) => {
      if (node === null) return
      if (node.element === key) {
        return node
      } else {
        return searchNode((key < node.element) ? node.left : node.right, key)
      }
    }
    return searchNode(this.root, key)
  }

  maxDep() {
    const maxDepth = root => {
      if (root == null) return 0
      return Math.max(maxDepth(root.left) + 1, maxDepth(root.right) + 1)
    //   const queue = [root]
    //   let level = 0
    //   while (queue.length) {
    //     let size = queue.length
    //     while (size--) {
    //       const front = queue.shift()
    //       if (front.left) queue.push(front.left)
    //       if (front.right) queue.push(front.right)
    //     }
    //     level++
    //   }
    //   return level
    }
    return maxDepth(this.root)
  }

  minDep() {
    const minDepth = root => {
      if (root == null) return 0
      return Math.min(minDepth(root.left) + 1, minDepth(root.right) + 1)
    }
    return minDepth(this.root)
  }
}

const tree = new BinarySearchTree()
tree.insert(11)
tree.insert(7)
tree.insert(5)
tree.insert(3)
tree.insert(9)
tree.insert(8)
tree.insert(10)
tree.insert(13)
tree.insert(12)
tree.insert(14)
tree.insert(20)
tree.insert(18)
tree.insert(25)
console.log(tree)

// tree.inOrderTraverse((value) => {
//   console.log(value)
// })

// tree.preOrderTraverse((value) => {
//   console.log(value)
// })

var result = tree.levelOrderTraverse((value) => {
  console.log(value)
})
console.log(result)

var depth = tree.maxDep()
console.log('最大深度为：' + depth)

var dep = tree.minDep()
console.log('最小深度为：' + dep)

// var m = tree.min()
// console.log(m.element)

// var max = tree.max()
// console.log(max)

var r = tree.search(12)
console.log(r)

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

