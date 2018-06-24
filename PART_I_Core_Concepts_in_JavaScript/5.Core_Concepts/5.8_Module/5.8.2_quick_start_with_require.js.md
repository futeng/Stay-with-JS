# Quick Start with Require.js

WebStrom is a great IDE. We basically use it as a simple Web Server in this demo.

A glance at the directory of this demo:

```shell
.
├── index.html
└── js
    ├── garage.js
    └── main.js
```

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>

<script src="https://cdn.bootcss.com/require.js/2.3.5/require.js" data-main="js/main"></script>

</body>
</html>
```

Import the `require.js` in the very beginning. 

And there is a wired paremeter `data-main`, for load the main js by `require.js`, like an entrance. All your module code should arranged in `main.js` file.

Notice: Value of `data-main`, is a relative path to import JS file, so you can omit the `js` suffix. Just follow your intuition.

**main.js**


```js
/**
 * Created by futeng on 2018/6/21.
 */

require(['garage'], function (garage) {
    garage.print();
    garage.add('Polo').add('focus').print();

});

```

`main.js` is an entrance module and there is where your bootstrap code maintance here.

- `require` function allows two parameters, one is an array with module name. 
- Once loaded, the module enter into the callback function as an input parameters. It's ok for litter confuse here, cause you shoud see more in the module buiding place.
- Then all your fantastic logical code flows here with the help of module.

**garage.js**

`garage.js` defined your module.

Only different between normal IIFE with module and `require.js` is you have to write your module as a callback inside an function called `define`. (See more to google AMD principal).

```js
/**
 * Created by futeng on 2018/6/21.
 */

define(function garage() {
    var data = ['malibu', 'YUSHENG'];

    function printData() {
        console.log(data);
    }

    function addCars(carName) {
        if(carName) {
            data.push(carName);
        }
        return this;
    }

    return {
        add: addCars,
        print: printData
    }
})
```



So. 

1. Import `require.js` and assign your main.js as an entrance.
2. Define your module.js.
3. Define your `main.js` then you can work with your module with simple reference.