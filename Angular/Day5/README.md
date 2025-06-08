### Why is let and const required when we have var?

var is global and function scoped, whereas let and const are global and block scoped.
Sometimes when declaring a variable as var and later in code same variable name is used it might create an unwanted bug by changing the value of existing variable with same name.

### What is hoisting for var, let and const?

javascript hoist a variable declared in the end of its scope to the starting of the scope. For var it is hoisted on the start of function and initialized as undefined. for let and const it is hoisted at the start of block and left uninitialized.


## Closure

A closure is a funtion which has access to its own scope, outer function's scope and global scope even after the function has returned

```js
function outerFunction() {
  let outerVariable = 'I am outside!';

  function innerFunction() {
    console.log(outerVariable); // ✅ innerFunction has access to outerVariable
  }

  return innerFunction;
}

const closureFunc = outerFunction();  // outerFunction runs and returns innerFunction
closureFunc();  // Output: I am outside!
```

