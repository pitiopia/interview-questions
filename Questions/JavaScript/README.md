# JavaScript Interview Questions

Below you can find a list of most common questions that might occur during JavaScript Interview.

This file is a part of bigger set of [IT Interview Questions](../../README.md)

# Questions

#### :exclamation: What is a prototype in JavaScript :exclamation:

* prototype is an object that defines properties for other objects inheriting it
* example of basic usage:

```javascript
function Player(firstname, lastname) {
    this.firstname = firstname; //defining property "firstname"
    this.lastname = lastname; //defining property "lastname"
    //it is possible to define prototype methods inside the prototype
    this.name = function() {  
             return  this.firstname + " " + this.lastname;
         }
} 

// we can also define methods by using the "prototype" property
Player.prototype.shoot = function() {
    return "Goooaaaalll!";
}

// Valid way to create an instance of a given prototype
var player = new Player('Piotr', 'Czaus');
player.name() //Piotr Czaus
player.shoot() //Goooaaaalll!

// This won't work as expected
var player2 = Player('Piotr', 'Czaus'); //player2 variable is undefined, not an instance of Player prototype
```

* all objects and prototypes have parent prototypes (this rule has one exception for the top level prototype )
* the below rule does not apply for primitive values like `undefined`, `null`, `boolean`, `number` and `string`
* you can retrieve prototype of a given object by using `Object.getPrototypeOf()` method or  `__proto__` accessor (later doesn't work on IE)

```javascript
var myString = new String("test string");

Object.getPrototypeOf(myString); //[object String]

myString.__proto__; //[object String]
```

* when you try to retrieve a prototype of a primitive value, it will be coerced to an proper object:

```javascript
"random String".__proto__ === String("random String").__proto__; // true
```

* 