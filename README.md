# <img src="http://www.w3devcampus.com/wp-content/uploads/logoAndOther/logo_JavaScript.png" width="100"> ECMAScript 2015 Experiments

*All examples require [jasmine](https://github.com/jasmine/jasmine) for tests*

ECMAScript 2015 experiments includes the following features:
- [Let](#let)
- [Destructuring Assignment](#destructuring-assignment)
- [Arrow functions](#arrow-functions)
- [Classes](#classes)
- [Spread](#spread)
- [Iterators For..Of](#iterators-forof)
- [Generators](#generators)

### Let
The __let__ statement declares a block scope local variable, optionally initializing it to a value.

```js
'use strict';
describe("using let", function() {
  it("block scoping", function() {
    var structure = function(args) {
      if ( args ) {
        let x = 2;
        return x;
      }
    };

    var result = structure(true);
    expect(result).toBe(2);
  });

  it("block scope with for", function() {
    var structure = function() {

      for(let i = 0; i< 10; i++) {
      }
      
      /* return i won't work */
      return 0;
    };

    var result = structure();
    expect(result).toBe(0);
  });

});
```

### Destructuring Assignment
The __destructuring__ assignment syntax is a JavaScript expression that makes it possible to extract data from arrays or objects using a syntax that mirrors the construction of array and object literals.

```js
'use strict';
describe("Destructuring assignment", function() {  
  it("destructure arrays", function() {

    var structure = function() {
      return ["Element 1", "Element 2", "Element 3"];
    };

    let [, a, b, c] = structure();

    expect(a).toBe("Element 1");
    expect(b).toBe("Element 2");
    expect(c).toBeUndefined();
  });

});
```

### Arrow functions
An __arrow function__ expression (also known as fat arrow function) has a shorter syntax compared to function expressions and lexically binds the this value. Arrow functions are always anonymous.

```js
'use strict';
describe("Arrow Functions", function() {
  it("define a function", function() {

    let add = (x, y) => {
      let sum = x + y;
      return sum;
    };

    let square = x => x * x;
    let five = () => 5;

    expect(square(add(2,five()))).toBe(49);
  });

  it("can be used with array methods", function() {
    var numbers = [1,2,3,4],
        amount = 0;

    numbers.forEach(number => amount += number);
    expect(amount).toBe(10);

    var four = numbers.map(number => number * 4);
    expect(four).toEqual([4,8,12,16]);
  });

  it("lexically binds the this value", function(finished) {
    this.name = "Diogo";

    setTimeout(() => {
      expect(this.name).toBe("Diogo");
      finished();
    }, 10);
    
  });

});
```

### Classes
The __class__ syntax is __not__ introducing a new object-oriented inheritance model to JavaScript. JS classes provide a much simpler and clearer syntax to create objects and dealing with inheritance.

```js
'use strict';
describe("define class", function() {
  it("can create a class", function() {

    class Vehicle {
      getModel() {
        return "HB20!";
      }
      getProdutor() {
        return "Hyundai";
      }
    }
    
    let v = new Vehicle();

    expect(v.getModel()).toBe("HB20!");
    expect(v.getProdutor()).toBe("Hyundai");
    expect(Vehicle.prototype.getModel.call(v)).toBe("HB20!");
  });
  
  it("getters and setters", function() {
    class Vehicle {
        constructor(produtor) {
        this.produtor = produtor;
      }

      model() {
        return "HB20!";
      }

      get produtor() {
        return this._produtor.toUpperCase();
      }
      
      set produtor(newValue) {
        this._produtor = newValue;
      }
    }

    let v1 = new Vehicle("Hyundai");
    
    expect(v1.produtor).toBe("Hyundai");
  });
  
  it("override methods", function() {
    class Vehicle {
        constructor(produtor) {
        this.produtor = produtor;
      }

      model() {
        return "HB20!";
      }

      get produtor() {
        return this._produtor.toUpperCase();
      }
      
      set produtor(newValue) {
        this._produtor = newValue;
      }
    }
    
    class Car extends Vehicle {     
      constructor(title, name) {
        super(name);
        this._title = title;        
      }

      get title() {
        return this._title;
      }

      model() {
        return "Onix";
      }

    }
    
    let c1 = new Car("Sandeiro", "Lancer");
    let v1 = new Vehicle("Corola");

    expect(v1.model()).toBe("HB20!");
    expect(c1.model()).toBe("Onix");
  });
  
});
```

### Spread
The __spread__ operator allows an expression to be expanded in places where multiple arguments (for function calls) or multiple elements (for array literals) are expected.

```js
'use strict';
describe("the spread operator", function() {
  it("spread an array parameters", function() {

    let foo = function(x, y, z) {
      return x + y + z;
    }

    var result = foo(...[1, 2, 3]);
    
    expect(result).toBe(6); 
  });

  it("can build arrays", function() {
    var a = [4, 5, 6];
    var b = [1, 2, 3, ...a, 7, 8];

    expect(b).toEqual([1,2,3,4,5,6,7,8]);
  });

});
```

### Iterators For...Of
The __for...of__ statement creates a loop Iterating over iterable objects (including Array, Map, Set, arguments object and so on), invoking a custom iteration hook with statements to be executed for the value of each distinct property.

```js
'use strict';
describe("for of", function() {
  it("working with iteratables", function() {
    let sum = 0;
    let arr = [3,4,5,6];
    arr.foo = "test";
    
    //for...in iterates over property names ex: for (let i in arr) { console.log(i); }
    //for...of iterates over property values
    for(let i of arr) {
      sum += i;
    }

    expect(sum).toBe(18);
  });

});

'use strict';
describe("iterables", function() {
  it("iterators at a low level", function() {
    let numbers = [1,2,3,4,5];
    let sum = 0;
    let iterator = numbers[Symbol.iterator]();
    let next = iterator.next();
    
    while(!next.done) {
      sum += next.value;
      next = iterator.next();
    }
    
    expect(sum).toBe(15);
  });

});
```

### Generators
The __generators__ are functions which can be excited and later re-entered. Their context (variable bindings) will be saved across re-entrances.

```js
'use strict';
describe("generators", function() {
  it("build an iterable", function() {
    let numbers = function*() {
      for(let i = 0; i <= 6; i++) {

        yield i;

        console.log(i);
      }
    };

    let sum = 0;

    for(let n of numbers()){
      sum += n;
      console.log("generator" + sum);
    }
    
    expect(sum).toBe(21);
  });

});
```

## References
* [ES6 Features](https://github.com/lukehoban/es6features)
* [MDN](https://developer.mozilla.org)
* [Fundamentals for ES6 course](https://github.com/joeeames/ES6FundamentalsCourseFiles)
