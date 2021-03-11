### 队列
> 队列 遵循的原则 是先进先出（FIFO）（将队列想象成排队买票, 先到先服务）
```Javascript
class Queue {
  constructor() {
    this.count = 0
    this.lowestCount = 0
    this.items = {}
  }
  // 向队列尾部添加一个(或多个)新的项
  enqueue(element) {
    this.items[this.count] = element
    this.count++
  }
  // 移除队列的第一项(即排在队列最前面的项)并返回被移除的元素
  dequeue() {
    if (this.isEmpty()) {
      return undefined
    }
    const result = this.items[this.lowestCount]
    delete this.items[this.lowestCount]
    this.lowestCount++
    return result
  }
  // 返回队列中第一个元素 最先被添加，也将是最先被移除的元素，队列不做任何变动
  peek() {
    if (this.isEmpty()) {
      return undefined
    }
    return this.items[this.lowestCount]
  }
  // 队列中不包含任何元素 返回true
  isEmpty() {
    return this.size() === 0
  }
  // 队列元素的个数
  size() {
    return this.count - this.lowestCount
  }
  toString() {
    if (this.isEmpty()) {
      return ''
    }
    let objString = `${this.items[this.lowestCount]}`
    for (let i = this.lowestCount + 1; i < this.count; i++) {
      objString = `${objString}, ${this.items[i]}`
    }
    return objString
  }
  clear() {
    this.count = 0
    this.lowestCount = 0
    this.items = {}
  }
}
const queue = new Queue()
```
> 双端队列
```Javascript
class Deque {
  constructor() {
    this.count = 0
    this.lowestCount = 0
    this.items = {}
  }
  addFront(element) {
    if (this.isEmpty()) {
      this.addBack(element)
    } else if (this.lowestCount > 0) {
      this.lowestCount--
      this.items[this.lowestCount] = element
    } else {
      for (let i = this.count; i > 0; i--) {
        this.items[i] = this.items[i - 1]
      }
      this.items[0] = element
      this.lowestCount = 0
      this.count++
    }
  }
  addBack(element) {
    this.items[this.count] = element
    this.count++
  }
  removeFront() {
    if (this.isEmpty()) {
      return undefined
    }
    const result = this.items[this.lowestCount]
    delete this.items[this.lowestCount]
    this.lowestCount++
    return result
  }
  removeBack() {
    if (this.isEmpty()) {
      return undefined
    }
    this.count--
    const result = this.items[this.count]
    delete this.items[this.count]
    return result
  }
  peekFront() {
    return this.items[this.lowestCount]
  }
  peekBack() {
    return this.items[this.count - 1]
  }
  isEmpty() {
    return this.size() === 0
  }
  size() {
    return this.count - this.lowestCount
  }
  toString() {}
}

const deque = new Deque()
```
### 栈
> 栈 遵循的原则：先进后出（LIFO）（将栈看作弹夹，往里压子弹。先打出的是最后压进去的子弹）
 * 栈是一种遵循后进先出(LIFO)原则的有序集合，
 * 新添加或待删除的元素都保存再栈的同一端，称作栈顶
 * 另一端就叫栈底,新元素都靠近栈顶,旧元素都靠近栈底
1. 用对象的形式存储

```Javascript
class Stack {
  constructor() {
    this.count = 0
    this.items = {}
  }
  push(element) {
    this.items[this.count] = element
    this.count++
  }
  pop() {
    if (this.isEmpty()) {
      return undefined
    }
    this.count--
    const popVal = this.items[this.count]
    delete this.items[this.count]
    return popVal 
  }
  peek() {
    if (this.isEmpty()) {
      return undefined
    }
    return this.items[this.count - 1]
  }
  isEmpty() {
    return this.count === 0
  }
  size() {
    return this.count
  }
  clear() {
    this.items = {}
    this.count = 0
  }
  toString() {
    if (this.isEmpty()) {
      return ''
    }
    let objString = `${this.items[0]}`
    for (let i = 1; i < this.count; i++) {
      objString = `${objString}, ${this.items[i]}`
    }
    return objString
  }
}

const stack = new Stack()
```

2. 用数组的形式存储

```Javascript
class Stack {
  constructor() {
    this.items = []
  }
  // 添加一个(或多个)新元素到栈顶
  push(element) {
    this.items.push(element)
  }
  // 移除栈顶的元素, 同时返回被删除的元素
  pop() {
    return this.items.pop()
  }
  // 返回栈顶的元素, 仅仅返回栈顶元素.不做任何修改
  peek() {
    return this.items[this.items.length - 1]
  }
  // 如果栈里没有任何元素 返回 true 否则 返回 false
  isEmpty() {
    return this.items.length === 0
  }
  // 清除栈里的所有元素
  clear() {
    this.items = []
  }
  // 返回栈里元素的个数, 和数组的length方法很类似
  size() {
    return this.items.length
  }
}
const stack = new Stack()
```
### 单向链表
> 链表数据结构 当前的数据存放着指向下一个数据的指针，指针为null就到末尾
```Javascript
// 单向数据链表

class LinkedList {
	constructor(equalsFn = defaultEquals) {
		this.count = 0
		this.head = null
		this.equalsFn = defaultEquals
	}
	// 项链表追加元素
	push(element) {
		const node = new Node(element)
		if (this.head === null) {
			this.head = node
		} else {
			let current = this.head
			while(current.next !== null) {
				current = current.next
			}
			current.next = node
		}
		this.count++
	}
	// 指定位置插入 元素
	insert(element, index) {
		if (index >= 0 && index <= this.count) {
			let node = new Node(element)
			let current = this.head
			if (index === 0) {
				node.next = current
				this.head = node
			} else {
				const previous = this.getElementAt(index - 1)
				current = previous.next
				node.next = current
				previous.next = node
			}
			this.count++
			return true
		}
		return false
	}
	// 根据元素删除节点
	remove(element) {
		const index = this.indexOf(element)
		return this.removeAt(index)
	}
	// 根据索引删除节点
	removeAt(index) {
		if (index >= 0 && index < this.count) {
			let current = this.head
			if (index === 0) {
				this.head = current.next
			} else {
				const previous = this.getElementAt(index - 1)
				current = previous.next
				previous.next = current.next
			}
			this.count--
			return current.element
		}
		return undefined
	}
	// 查找该元素在链表中的索引 并返回 未找到 返回 -1
	indexOf(element) {
		let current = this.head
		for (let i = 0; i < this.count && this.head !== null; i++) {
			if (this.equalsFn(element, current.element)) {
				return i
			}
			current = current.next
		}
		return -1
	}
	// 根据索引返回当前的链表节点
	getElementAt(index) {
		if (index >= 0 && index <= this.count) {
			let current = this.head
			for (let i = 0; i < index && current !== null; i++) {
				current = current.next
			}
			return current
		}
		return undefined
	}
	// 链表中不包含任何元素 返回true
	isEmpty() {
		return this.size() === 0
	}
	// 返回链表个数
	size() {
		return this.count
	}
	// 返回链表中所有的元素
	toString() {
		let objString = `${this.head.element}`
		let node = this.head.next
		for (let i = 1; i < this.count && node !== null; i++) {
			objString = `${objString}, ${node.element}`
			node = node.next
		}
		return objString
	}
}
```
