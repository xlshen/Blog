#### Go->Experience
##### 1. New Function()
使用Function构造器生成的函数，并不会在创建它们的上下文中创建闭包；  
它们一般在全局作用域中被创建。当运行这些函数的时候，它们只能访问自己的本地变量和全局变量，不能访问Function构造器被调用生成的上下文的作用域。【调用时才进行参数传递，形不成闭包】这和使用带有函数表达式代码的 eval 不同。
##### 2. eval()
##### 尾递归优化
```js
function trampoline(f) {
  var accumulated = [];
  var signal = false;
  var value;
  return function() {
    accumulated.push(arguments);
    if (!signal) {
      signal = true;
      while (accumulated.length) {
        value = f.apply(this, accumulated.shift());
      }
      signal = false;
      return value;
    }
  };
}
var sum = trampoline(function(x, y) {
  if (y > 0) {
    return sum(x + 1, y - 1);
  } else {
    return x;
  }
});
console.log(sum(1, 20));

```
