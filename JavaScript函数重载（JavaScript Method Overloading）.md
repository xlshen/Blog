### JavaScript函数重载
> 大神John Resig关于JS模拟函数重载的原文：<a href="https://johnresig.com/blog/javascript-method-overloading/">https://johnresig.com/blog/javascript-method-overloading/</a>

**Core function**：
```js
function addMethod(object, name, fn){
  var old = object[name]; // 记录不同参数对应上一个处理函数，第一次为undefined, 第二次为第一次处理函数...
  object[name] = function(){ // 返回闭包函数
    if(arguments.length === fn.length){
      return fn.apply(this, arguments); // 如果函数传入参数与最后添加函数参数相同，则直接处理
    }else if(typeof old === "function"){ 
      return old.apply(this, arguments); // 迭代前一个old函数处理，找到参数相等或不满足条件返回undefined
    }
  };
}
```
**Method overloading function**
```js
function Users(){
  addMethod(this, "find", function(){ console.log("Nothing!")} );
  addMethod(this, "find", function(name){ console.log(name)} );
  addMethod(this, "find", function(name, age){ console.log(name, age)} );
}
```
**Call function**
```js
 var user = new Users();
 user.find("xlshen"); // xlshen
 user.find("xlshen", 18); // xlshen 18
```
**注意事项**
1. 模拟重载实现的只是参数的不同，没有区分参数的类型
2. 因为是闭包的层层调用，如果要求性能的话，请慎用
