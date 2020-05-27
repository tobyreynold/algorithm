<template>
  <div class="algorithm-container">
    <h2>模拟Graph</h2>
  </div>
</template>

<script>

// export default {
//   name: 'stack',
// }

class Dictionary {
  constructor() {
    this.items = {}
  }

  set(key, value) {
    this.items[key] = value
  }

  remove(key) {
    delete this.items[key]
  }

  get(key) {
    return this.items[key]
  }

  get value() {
    return Object.values(this.items)
  }

  get keys() {
    return Object.keys(this.items)
  }
}

class Graph {
  constructor() {
    this.vertices = []
    this.adjlist = new Dictionary()
  }

  addVertex(v) {
    this.vertices.push(v)
    this.adjlist.set(v, [])
  }

  addEdge(v, w) {
    this.adjlist.get(v).push(w)
    this.adjlist.get(w).push(v)
  }

  toString() {
    return this.vertices.reduce((r, v, i) => {
      return this.adjlist.get(v).reduce((r, w, i) => {
        return r + `${w}`
      }, `${r}\n${v} =>`)
    }, '')
  }
  /* Breadth-First-Search */
  bfs(v, callback) {
    const read = []
    const adjList = this.adjlist
    const pending = [v || this.vertices[0]]
    const readVertices = vertices => {
      vertices.forEach(key => {
        read.push(key)
        pending.shift()
        adjList.get(key).forEach(v => {
          if (!pending.includes(v) && !read.includes(v)) {
            pending.push(v)
          }
        })
        if (callback) callback(key)
        if (pending.length) readVertices(pending)
      })
    }
    readVertices(pending)
  }
  /* Depth-First-Search */
  dfs(callback) {
    const read = []
    const adjList = this.adjlist
    const readVertices = vertices => {
      vertices.forEach(key => {
        if (read.includes(key)) return
        read.push(key)
        if (callback) callback(key)
        if (this.vertices.length !== read.length) {
          readVertices(adjList.get(key))
        }
      })
    }
    readVertices(adjList.keys)
  }
}

const gra = new Graph()

;['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'].forEach(c => gra.addVertex(c))
gra.addEdge('A', 'B')
gra.addEdge('A', 'C')
gra.addEdge('A', 'D')
gra.addEdge('C', 'D')
gra.addEdge('C', 'G')
gra.addEdge('D', 'G')
gra.addEdge('D', 'H')
gra.addEdge('B', 'E')
gra.addEdge('B', 'F')
gra.addEdge('E', 'I')
// dictionary.set('Gandalf', 'gandalf@email.com')
// dictionary.set('John', 'johnsnow@email.com')
// dictionary.set('Tyrion', 'tyrion@email.com')
console.log(gra.toString())
// console.log(gra.vertices[0])
gra.bfs(gra.vertices[0], value => console.log('BFS Visited vertex:' + value))
console.log(gra)
gra.dfs(v => console.log('DFS Visited vertex:' + v))

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

