- Implementing stack and Queue in JavaScript
```
let stack = [];
stack.push(1); // push to stack
stack.push(2);
stack.push(3);
console.log(stack); // [1,2,3]
let topValue = stack.pop(); // topValue === 3, stack is now [1,2]

let queue = [];
queue.add = queue.push;
queue.remove = queue.shift;
queue.add('a');
queue.add('b');
console.log(queue); // ['a', 'b']
let qValue = queue.remove(); // qValue === 'a', queue is now ['b']
```