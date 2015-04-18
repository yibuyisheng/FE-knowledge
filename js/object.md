* 对象属性特性（ property attributes ）：

  - 可写（ writable attribute ）。
  - 可枚举（ enumerable attribute ），表明是否可以通过 for/in 循环返回该属性。
  - 可配置（ configurable attribute ），表明是否可以删除该属性或修改该属性的其他特性。如果属性是不可配置的，则不能修改它的可配置性和可枚举性，不能将可写性从 false 改为 true ，但可以从 true 改为 false ；如果存取器是不可配置的，则不能修改其 getter 和 setter 方法，也不能将它转换为存取器属性；
  
* 在 ECMAScript 5 之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。

* 对象特性（ object attribute ）：

 - **对象的原型**指向另外一个对象，本对象的属性继承自它的原型对象。
 - **对象的类**是一个标识对象类型的字符串。
 - **对象的扩展标记**指明了（在 ECMAScript 5 中）是否可以向该对象添加新属性。
 
* 一些概念：

  - 内置对象
  - 宿主对象
  - 自定义对象
  - 自有属性
  - 继承属性
  
* propertyIsEnumerable()： 是自有属性且属性可枚举，返回 true 。

* Object.keys() 返回对象中可枚举的自有属性。

* Object.getOwnPropertyNames() 返回对象所有自有属性的名称。
  
* 给对象直接量定义存取器属性：

  ```js
  var random = {
    get octet() { return Math.floor(Math.random() * 256); },
    get name() { return this._name; },
    set name(value) { this._name = value; }
  };
  ```
 
* 一个数据属性包含一个名字和4各特性（值、可写性、可枚举性、可配置性）。存取器属性的4各特性是读取（ get ）、写入（ set ）、可枚举性和可配置性。

* Object.getOwnPropertyDescriptor() 可以获得某个对象特定属性的属性描述符：

  ```js
  Object.getOwnPropertyDescriptor({x:1}, "x"); // 返回 {value: 1, writable: true, enumerable: true. configurable: true}
  
  // random 是上文中的 random 对象
  Object.getOwnPropertyDescriptor(random, 'octet'); // 返回 {get: /*func*/, set: undefined, enumerable: true, configurable: true}
  ```
  
* 设置属性的特性：

  ```js
  var o = {};
  // 添加一个不可枚举的属性
  Object.defineProperty(o, 'x', {
    value: 1,
    writable: true,
    enumerable: false,
    configurable: true
  });
  
  // 修改为只读
  Object.defineProperty(o, 'x', {writabale: false});
  
  // 从数据属性修改为存取器属性
  Object.defineProperty(o, 'x', {get: function () {return 0;}});
  
  // 同时修改和创建多个属性
  var p = Object.defineProperties({}, {
    x: {value: 1, writable: true, enumerable: true, configurable: true},
    y: {value: 1, writable: true, enumerable: true, configurable: true},
    r: {
      get: function () { return Math.sqrt(this.x * this.x + this.y * this.y) },
      enumerable: true,
      configurable: true
    }
  });
  ```
  
* Object.getPrototypeOf() 查询对象原型。

* isPrototypeOf() 检测一个对象是否是另一个对象的原型（或处于另一个对象的原型链中）。

* Object.isExtensible() 判断对象是否可扩展。

* Object.preventExtensions() 将对象转换为不可扩展的。一旦对象转换为不可扩展，就无法转换回可扩展了。该函数只影响到对象本身的可扩展性，如果给一个不可扩展的对象的原型添加属性，这个不可扩展的对象同样会继承这些新属性。

* Object.seal() 将对象设置为不可扩展的，并且将对象所有属性设为不可配置的。对于已经封闭（ sealed ）起来的对象是不能解封的。可以使用 Object.isSealed() 来检测对象是否封闭。

* Object.freez() 将对象设置为不可扩展的，并且将对象所有属性设为不可配置和只读（如果对象的存取器属性具有 setter 方法，存取器属性将不受影响，仍可以通过给属性赋值调用它们）。Object.isFrozen() 检测对象是否冻结。

* JSON.stringify() 只能序列化对象可枚举的自有属性。