# <img src="http://www.w3devcampus.com/wp-content/uploads/logoAndOther/logo_JavaScript.png" width="100"> ECMAScript 6 Experiments

*All examples require [jasmine](https://github.com/jasmine/jasmine) for tests*

## Let
The __let__ statement declares a block scope local variable, optionally initializing it to a value. [Let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

```js
describe("using let", function() {

  it("block scoping", function() {

    var structure = function(args) {
      if(args){
        let x = 2;
        return x;
      }
    };

    var result = structure(true);
    expect(result).toBe(2);
  });

  it("block scope with for", function(){

    var structure = function(){

      for(let i = 0; i< 10; i++){
      }
      
      /* return i won't work */
      return 0;   
    };

    var result = structure();
    expect(result).toBe(0);
  });

});
```
## Destructuring Assignment
The __destructuring__ assignment syntax is a JavaScript expression that makes it possible to extract data from arrays or objects using a syntax that mirrors the construction of array and object literals.

```js
'use strict';
describe("Destructuring assignment", function() {  
  it("destructure arrays", function() {

    var structure = function(){
      return ["Element 1", "Element 2", "Element 3"];
    };

    let [, a, b, c] = structure();

    expect(a).toBe("Element 1");
    expect(b).toBe("Element 2");
    expect(c).toBeUndefined();
  });

});
```


## References
* [ES6 Features](https://github.com/lukehoban/es6features)













