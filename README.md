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

## Arrow functions
An __arrow function__ expression (also known as fat arrow function) has a shorter syntax compared to function expressions and lexically binds the this value. Arrow functions are always anonymous.

```js
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

## References
* [ES6 Features](https://github.com/lukehoban/es6features)
* [MDN](https://developer.mozilla.org)













