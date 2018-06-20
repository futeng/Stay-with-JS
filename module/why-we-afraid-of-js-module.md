# Why We Afraid of JS Module

## Truly Afraid List

- Module was never familiar to you both in form and in practise.
- Can you explain why we need *Name binding*, *Scope*, *Lexical Scope*, *Closure* and *Call Back*. 

I know :) , but at least we know where we are.

So, please follow my step, break the fear and level up. （If anything wrong please check the basic concept.）

Be cool!

## 7 Step to Stay with JS Module

### level 1 : Encapsulate date with Function 

```js
function foo() {
    var name = "futeng and his frinds";
    var cars = ['Mazda 3', 'Malibu','YUSHENG'];
    function getName() {
        return name;
    }
    function getCars() {
        return cars;
    }
}
foo();// nothing happened
```

Function `foo` sealed data and do something functionality, but why we here?

To understand JavaScript is a Lexical Scope language like crysitally understand the inner function can access (RHS) the data outside (in foo scope, like `name`) and all it happened in Lexical time (NOT run time). 

And it will give you the permission denied (ReferenceError) when you try to access the data in function scope from outside.

### level 2 : Expose data by inner function (API) 

```js
function foo() {
    var name = "futeng and his frinds";
    var cars = ['Mazda 3', 'Malibu','YUSHENG'];
    function getName() {
        return name;
    }
    function getCars() {
        return cars;
    }
    return {
        name:getName,
        cars:getCars
    }
}

var f = foo();
f.name() + " have those cars: " + f.cars(); //"futeng and his frinds have those cars: Mazda 3,Malibu,YUSHENG"
```

Inner function `getName` and `getCars` are expose the private data from themself: through an inner function, and we can name it **API function**.

Why we here, I can not see any tricks here?

- Trick 1：There is a closure happened immediately when `foo` function called by outside (`var f = foo();`) . Something like the API function want to reference the data from `foo` scope, so the full `foo` function content have to save to memory forever (released until no reference at all). 
- Trick 2: (It's easy to omit such a wonderful feature. Sad.)  We can finally access data in function from outsite. (like a trick against to Lexical scope)

Notice: Once we call the `foo`() function, it will generate an Object to return. The point is every time you call, you get a brand new Object.

### Level 3 : Singleton with IIFE 

```js
var f = (function foo() {
    var name = "futeng and his frinds";
    var cars = ['Mazda 3', 'Malibu','YUSHENG'];
    function getName() {
        return name;
    }
    function getCars() {
        return cars;
    }
    return {
        name:getName,
        cars:getCars

    }
})();

f.name(); // "futeng and his frinds"
f.cars(); // (3) ["Mazda 3", "Malibu", "YUSHENG"]
```

One explain can give you free from **IIFE** (*Immediately Invoked Function Expression*) : 

Bracket `()` is live to let the interpretor to resolve anything inside as an ==Expression==.

```js
3 // 3 simple exression with a Number
(3)  // 3  simple exression with a bracket 
+3 // 3 (cool)

(function(){console.log("GOOD");}) //ƒ (){console.log("GOOD");}
// yeah. treat like an expression, and the caculate result is an function itself.
```

IIFE make the scope singleton. So there is no notice this time.

### Level 4: Like a normal function to deal with parametes

```js
var f = (function foo() {
    var name = "futeng and his frinds";
    var cars = ['Mazda 3', 'Malibu','YUSHENG'];
    function getName() {
        return name;
    }
    function getCars() {
        return cars;
    }
    function addNewCar(newCar) {
        cars.push(newCar);
    }
    return {
        name:getName,
        cars:getCars,
        addNewCar:addNewCar
        
    }
})();

f.cars(); // (3) ["Mazda 3", "Malibu", "YUSHENG"]
f.addNewCar("Bat Car");
f.cars(); // (4) ["Mazda 3", "Malibu", "YUSHENG", "Bat Car"]
```

We generate a new API (function) to allow us to change the data in closure.

This one is an extra rewards.

### Level 5: Build your module API like jQuery with chain

```js
var $ = (function foo() {
    
    var name = "futeng and his frinds";
    var cars = ['Mazda 3', 'Malibu','YUSHENG'];
    function getName() {
        return name;
    }
    function getCars() {
        return cars;
    }
    function addNewCar(newCar) {
        cars.push(newCar);
        return this;
    }
    return {
        name:getName,
        cars:getCars,
        addNewCar:addNewCar
        
    }
})();
$.addNewCar("Bat Car").addNewCar("Rocket").cars(); 
// (5) ["Mazda 3", "Malibu", "YUSHENG", "Bat Car", "Rocket"]
```

You got it and konw It's cool :).

And more exiting is probably we smell somethings of the compositon of jQuery.

See more in [Module in Practise] , contains the next 2 levels. 