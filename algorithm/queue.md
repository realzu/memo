# Queue

```javascript
Class Queue() {
  constructor() {
    this.items = {}
    this.headIndex = 0;
    this.tailIndex = 0;
  }
  
  enqueue(item) {
    this.items[thisl.tailIndex] = items;
    this.tailIndex++;
  }
  
  dequeue() {
    const deletedItem = this.items[this.headIndex];
    delete this.items[this.headIndex];
    this.headIndex++;
    return deletedItem;
  }
  
  peek() {
    return this.items[this.headIndex]
  }
  
  getLength() {
    return this.tailIndex - this.headIndex;
  }
}
```
