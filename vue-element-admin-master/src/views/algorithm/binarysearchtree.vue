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

// tree.postOrderTraverse((value) => {
//   console.log(value)
// })

var m = tree.min()
console.log(m.element)

var max = tree.max()
console.log(max)

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

