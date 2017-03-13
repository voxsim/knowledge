List implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

class List {
  constructor() {
    this.memory = [];
    this.length = 0;
  }

  get(address) {
    return this.memory[address];
  }

  push(value) {
    this.memory[this.length] = value;
    this.length++;
  }

  pop() {
    if(this.length === 0) return;

    this.length--;
    let value = this.memory[this.length];
    delete this.memory[this.length];

    return value;
  }

  unshift(value) {
    this.memory = [value, ...this.memory];
    this.length++;
  }

  shift() {
    if(this.length === 0) return;

    let value = this.memory[0];
    [_, ...this.memory] = this.memory;
    this.length--;

    return value;
  }
}
```
