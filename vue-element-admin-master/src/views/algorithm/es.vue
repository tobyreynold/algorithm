<template>
  <div class="algorithm-container">
    <h2>Reactivity</h2>
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

// const dictionary = new Dictionary()
// dictionary.set('Gandalf', 'gandalf@email.com')
// dictionary.set('John', 'johnsnow@email.com')
// dictionary.set('Tyrion', 'tyrion@email.com')

// console.log(dictionary)

// vue 3.0 Reactive core proxy
function creatReactiveObject(target) {
  if (!isObject(target)) return target

  const handler = {
    get(target, key, receiver) {
      console.log('获取')
      const res = Reflect.get(target, key, receiver)
      console.log(target)
      return res
    },

    set(target, key, value, receiver) {
      console.log('设置')
      const result = Reflect.set(target, key, value, receiver)
      console.log(target)
      return result
    },

    deleteProperty(target, key) {
      console.log('删除')
      const result = Reflect.deleteProperty(target, key)
      console.log(target)
      return result
    }
  }
  const observed = new Proxy(target, handler)
  return observed
}

function isObject(obj) {
  return typeof obj === 'object' && obj !== null
}

function reactive(object) {
  return creatReactiveObject(object)
}

const p = reactive({ name: 'lynn' })

console.log(p.name) // 获取

p.name = 'aaa' // 设置

delete p.name // 删除

function newfac(ctor, ...args) {
  if (typeof ctor !== 'function') {
    return Error('new must be a function')
  }
  const obj = new Object()
  obj.__proto__ = Object.create(ctor.prototype)
  const res = ctor.apply(...args)
  const isObject = typeof res === 'object' && typeof res !== null
  const isFunction = typeof res === 'function'
  return isObject || isFunction ? res : obj
}

function A(text) {
  console.log(text)
}

const a = newfac(A, 'aaa')
console.log(a)

const selfMap = function(fn, context) {
  const arr = Array.prototype.slice.call(this)

  return arr.reduce((pre, cur, index) => {
    return [...pre, fn.call(context, cur, index, this)]
  }, [])
}

const selfFlat = function(depth = 1) {
  const arr = Array.prototype.slice.call(this)
  if (depth === 0) return arr
  return arr.reduce((pre, cur) => {
    if (Array.isArray(cur)) {
      return [...pre, ...selfFlat.call(cur, depth - 1)]
    } else {
      return [...pre, cur]
    }
  })
}

Array.prototype.selfMap = selfMap
Array.prototype.selfFlat = selfFlat;

[1, 2, 3].selfMap(number => console.log(number * 2))

const arr = [1, [2, 3], 4]
// arr.selfFlat();
// console.log(arr);

class EventEmitter {
  constructor() {
    this.subs = {}
  }

  on(event, cb) {
    (this.subs[event] || (this.subs[event] = [])).push(cb)
  }

  trigger(event, ...args) {
    this.subs[event] &&
        this.subs[event].forEach(cb => {
          cb(...args)
        })
  }

  off(event, offCb) {
    if (this.subs[event]) {
      const index = this.subs[event].findIndex(cb => cb === offCb)
      this.subs[event].splice(index, 1)
      if (this.subs[event].length) delete this.subs[event]
    }
  }

  once(event, oneCb) {
    const cb = (...args) => {
      oneCb(...args)
      this.off(event, oneCb)
    }
    this.on(event, cb)
  }
}

const e = new EventEmitter()
// e.on('emit', (num) => {
//     console.log(num);
// })

// e.on('find', (num) => {
//     console.log(num);
// })

// e.on('find', (n) => {
//     console.log(n);
// })

// console.log(e);

// e.once('emit', 123);
// e.trigger('emit', 123);
// // e.off('emit');
// console.log(e);

function curry(fn) {
  if (fn.length <= 1) return fn
  const generator = (...args) => {
    if (fn.length === args.length) {
      return fn(...args)
    } else {
      return (...args2) => {
        return generator(...args, ...args2)
      }
    }
  }

  return generator
}

const add = (a, b) => a + b
const curryAdd = curry(add)
const result = curryAdd(5)(2)
console.log('curry result:' + result)

class scheduler {
  constructor(cout) {
    this.count = count
    this.queue = []
    this.run = []
  }

  add(task) {
    this.queue.push(task)
    return this.schedule()
  }

  schedule() {
    if (this.run.length < this.count && this.queue.length) {
		  	const task = this.queue.shift()
		  	const promise = task().then(() => {
		  		this.run.splice(this.run.indexOf(promise), 1)
		  	})
		  	this.run.push(promise)
		  	return promise
    } else {
		  	return Promise.race(this.run).then(() => this.schedule())
    }
  }
}

</script>

<style scoped>
.algorithm-container{
  position: relative;
  width: 100%;
  height: 500px;
}
</style>

