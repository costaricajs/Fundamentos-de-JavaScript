# Conceptos Fundamentales en JavaScript

_Por favor notar que este documento en proceso de creación, las contribuciones son bienvenidas._  

Descripción los Conceptos Fundamentales de JavaScript que nos permiten entender la abstraction de este lenguage.

### Tabla de Contenidos
**[Funciones en Cadena](#funciones-en-cadena)** <br/>
**[Closure](#closure)** <br/>
**[Composición](#composición)** <br/>
**[Currying](#currying)** <br/>
**[Encapsulación](#encapsulación)** <br/>
**[Fábrica](#fábrica)** <br/>
**[Funciones de Orden Mayor](#funciones-de-orden-mayor)** <br/>
**[Herencia](#herencia)** <br/>
**[Objectos Literales](#objectos-literales)** <br/>
**[Polimorfismo](#polimorfismo)** <br/>
**[Alcance](#alcance)** <br/>

### Funciones en Cadena

Técnica para simplificar la ejecución de múltiples métodos sobre una misma variable u objeto.

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
Cuando una función utiliza una variable la cual fue declarada fuera de dicha función.

```javascript
var print = (function(){
  var h = 'hola';
  function printH(){
    console.log(h);
  }
  return printH;
})();

print(); // =>  'hola'
```

### Composición
Cuando combinamos dos o más funciones para crear una nueva, la cual contiene las funciones anteriores.

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
Consiste en convertir una función con múltiples parámetros / arity en diferentes funciones con menos parámetros.

```javascript
// function without currying format
var person = function(name, first, last) {
  return 'My Name is ' + name + ' ' + first + ' ' + last;
}
// function with currying format
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

### Encapsulación
Nos permite conservar declaraciones públicas y privadas en un solo objeto.

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

### Fábrica
Es una función que retorna un nuevo objeto.

```javascript
function calculator() {
  return { 
    sum: function(num1, num2) { return num1 + num2; }
  }
}

var cal = calculator();
cal.sum(1,2);
```

### Funciones de Orden Mayor 
Es una función que puede recibir otra función como parámetro, la cúal puede ser invocada por la función de order mayor.

```javascript
function sum(num) {
  return num + 10
}

/* map es una función de Array que recibe otra función y retorna un nuevo array con los resultado de ejecutar la función recibida con cada uno de elementos del arreglo */
var summedNumbers = [1,2,3].map(sum); // [11, 12, 13]
```

Las funciones que son enviadas como parámetros muchas veces son llamadas __callbacks__. 

### Herencia
Relacionar métodos y/o propiedades de un objeto a otro.

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

### Objectos Literales
Es un objecto que contiene entre llaves propiedades con formato nombre:valor separados por comas.

```javascript
var person = {
  hands : 2,
  legs  : 2,
  walk  : function() { console.log('Walking'); },
  talk  : function() { console.log('Talking'); }
}
```

### Polimorfismo
La posibilidad de llamar métodos en común de diferentes objectos sin alterar el resultado.

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

### Alcance
Es la jerarquía sobre cómo accesar las variables, objetos y funciones.

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
