### JavaScript函数重载
> 大神John Resig关于JS模拟函数重载的原文：<a href="https://johnresig.com/blog/javascript-method-overloading/">https://johnresig.com/blog/javascript-method-overloading/</a>

**Core function**：
```js
function addMethod(object, name, fn){
  var old = object[name];
  object[name] = function(){
    if(arguments.length === fn.length){
      return fn.apply(this, arguments);
    }else if(typeof old === "function"){
      return old.apply(this, arguments);
    }
  };
}
```
