<template>
  <div class="algorithm-container">
    <h2>模拟字典</h2>
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

const dictionary = new Dictionary()
dictionary.set('Gandalf', 'gandalf@email.com')
dictionary.set('John', 'johnsnow@email.com')
dictionary.set('Tyrion', 'tyrion@email.com')

console.log(dictionary)

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

