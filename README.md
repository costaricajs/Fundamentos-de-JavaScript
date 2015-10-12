# JSFundamentals
EN: Describe the JS Fundamental Concepts which allow us to understand the abstraction of this language.
<br />
SP: Describir los Conceptos Fundamentales de JavaScript que nos permiten entender la abstraction de este lenguage.

### Table of Contents
**[Closure](#closure)** <br/>
**[Composition](#composition)** <br/>
**[Currying](#currying)** <br/>
**[Encapsulation](#encapsulation)** <br/>
**[Factory](#factory)** <br/>
**[Inheritance](#inheritance)** <br/>

### Closure
EN: When a function uses a variable defined outside that function. <br />
SP: Cuando una función utiliza una variable la cual fue declarada fuera de dicha función.

```javascript
var name = 'Jhon';

function fullName(){
  name = name + ' Doe';
  return name;
}
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
// Convert From
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
<h1>N/D</h1>

### Factory
<h1>N/D</h1>

### Inheritance
<h1>N/D</h1>
