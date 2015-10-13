# JSFundamentals
EN: Describe the JS Fundamental Concepts which allow us to understand the abstraction of this language.
<br />
SP: Describir los Conceptos Fundamentales de JavaScript que nos permiten entender la abstraction de este lenguage.

### Table of Contents
**[Chain Functions](#chain-functions)** <br/>
**[Closure](#closure)** <br/>
**[Composition](#composition)** <br/>
**[Currying](#currying)** <br/>
**[Encapsulation](#encapsulation)** <br/>
**[Factory](#factory)** <br/>
**[Higher-Order Functions](#higher-order-functions)** <br/>
**[Inheritance](#inheritance)** <br/>
**[Object Literal](#object-literal)** <br/>
**[Polymorphism](#polymorphism)** <br/>
**[Scope](#scope)** <br/>

### Chain Functions
EN: Technique to simplify run multiple methods over a same variables and/or objects. <br />
SP: Técnica para simplificar la ejecución de múltiples métodos sobre una misma variable u objeto.

```javascript
var cal = function(num) {
  var num = num || 0;
  return {
    sum: function(num2){
      num = num + num2;
      return this;           /* return this which is the object which contains sum and subtract */
    },
    subtract: function(num2){
      num = num - num2;
      return this;          /* return this which is the object which contains sum and subtract */
    },
    displayTotal: function(){
      console.log(num);
      return this;
    }
  }
};

var calculator = cal(10);   /* num = 10 */

calculator.sum(10)          /* num = 20 */
          .subtract(2)      /* num = 18 */
          .sum(5)           /* num = 23 */
          .displayTotal();  // 23
```

### Closure
EN: When a function uses a variable defined outside that function. <br />
SP: Cuando una función utiliza una variable la cual fue declarada fuera de dicha función.

```javascript
var person = function(){
  
  var name = 'Jhon';

  return {
    showFullName: function(last){
      return name + ' ' + last; /* <-- Closure: we have access to the name variable */
    }
  }
}

var Jhon = person();
Jhon.showFullName('Doe');       // Jhon Doe
```

### Composition
EN: When you combine two or more functions in order to create a new one. <br />
SP: Cuando combinamos dos o más funciones para crear una nueva, la cual contiene las funciones anteriores.

```javascript
var walk = function walk(name) {
  console.log(name + ' is walking');
};

var talk = function talk(name) {
  console.log(name + ' is talking');
};

var person = function person(name) {
  return Object.assign({}, walk(name), talk(name));
};

var Jhon = person('Jhon');
Jhon.walk; // Jhon is walking
Jhon.talk; // Jhon is talking
```

### Currying
EN: It consists on convert a function with multiple parameters / arity in different functions with less parameters / arity. <br />
SP: Consiste en convertir una función con múltiples parámetros / arity en diferentes funciones con menos parámetros.

```javascript
// Converted From
var person = function(name, first, last) {
  return 'My Name is ' + name + ' ' + first + ' ' + last;
}
// To
var person = function (name) {
  return function (first) {
    return function (last) {
      return 'My Name is ' + name + ' ' + first + ' ' + last;
    }
  }
};

var Jhon = person('Jhon')('Doe');
Jhon('Blast'); // My Name is Jhon Doe Blast
```

### Encapsulation
EN: It allows us to conserve private and public declarations in a single object. <br />
SP: Nos permite conservar declaraciones públicas y privadas en un solo objeto.

```javascript
var security = function() {
  
  // Private
  var creditCard = '1111-2222-3333';
  
  return {
    // Public
    showCreditCard: function() {
      console.log('Your credit card is ' + creditCard);
    }
  }
  
}

var sec = security();

sec.showCreditCard();   // Your credit card is 1111-2222-3333

sec.creditCard = '11';  /* You can try to change the credit card value but It's not possible */

sec.showCreditCard();   // Your credit card is 1111-2222-3333
```

### Factory
EN: It is a function that returns a new object. <br />
SP: Es una función que retorna un nuevo objeto.

```javascript
function calculator() {
  return { 
    sum: function(num1, num2) { return num1 + num2; }
  }
}

var cal = calculator();
cal.sum(1,2);
```

### Higher-Order Functions
EN: It is a function that can take another function as parameter. <br />
SP: Es una función que puede recibir otra función como parámetro.

```javascript
function sum(num) {
  return num + 10
}

/* forEach is a function that receives another function */
[1,2,3].forEach(sum); // 11 // 12 // 13
```

### Inheritance
EN: Link methods and/or properties from one object to another. <br />
SP: Relacionar métodos y/o propiedades de un objeto a otro.

```javascript
var calculator = {
    sum: function(num1, num2) {
      return num1 + num2;
    },
    subtract: function(num1, num2) {
      return num1 - num2;
    }
}

var cal = Object.create(calculator); /* Inherit calculator */

cal.sum(2,2);      // 4
cal.subtract(2,2); // 0
```

### Object Literal
EN: It is an object which contains between curly braces properties with name:value format divided by commas. <br />
SP: Es un objecto que contiene entre llaves propiedades con formato nombre:valor separados por comas.

```javascript
var person = {
  hands : 2,
  legs  : 2,
  walk  : function() { console.log('Walking'); },
  talk  : function() { console.log('Talking'); }
}
```

### Polymorphism
EN: The possibility to call common methods between different objects without alter the result. <br />
SP: La posibilidad de llamar métodos en común de diferentes objectos sin alterar el resultado.

```javascript
function fruit(width, height) {
  var width = width, height = height;
  
  return {
  
    description: function() { 
      console.log('A. Fruit dimension w-' + width + ' / h-' + height);
    }
    
  }
};

function market(width, height, price) {
  var width = width, height = height, price = price;
  
  return {
  
    description: function() { 
      console.log('B. Fruit dimension w-' + width + ' / h-' + height + ' / $' + price);
    }
    
  }
};

function showDescription(obj) {
  if (typeof obj.description == 'function')
    obj.description(); /* <-- Polymorphism */
}

var myFruit  = fruit(50,60);
var myMarket  = market(50,60,25);

showDescription(myFruit);   // A. Fruit dimension w-50 / h-60
showDescription(myMarket);  // B. Fruit dimension w-50 / h-60 / $25
```

### Scope
EN: It is the hierarchy about how to access variables, objects and functions. <br />
SP: Es la jerarquía sobre cómo accesar las variables, objetos y funciones.

```javascript
var street = 'AVE51325';  /* Global variable */

function myScope() {
  var direction = 'SF91'; /* Just exists inside the function */
  console.log(direction); // SF91
  console.log(street);    // AVE51325
}

myScope();

console.log(street);      // AVE51325
console.log(direction);   // direction is not defined
```
