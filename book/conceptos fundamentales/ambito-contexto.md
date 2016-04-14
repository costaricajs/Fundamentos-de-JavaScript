# Ambito y Contexto de Ejecución

Es muy fácil confundir el ámbito con el contexto, pero no son lo mismo. Para ser justos, el tema es menos turbio si partimos y escarbamos cada concepto por separado.

## Ambito es sobre acceso a variables

Básicamente, por cada invocación a una función se asocia un:

 - `Ambito` basado en `Funciones`.

 - `Contexto` basado en `Objetos`.

## Ambito

El ámbito es un acceso único a la variable de una `Función` cuando esta se invoca.

```javascript
var ambito = 'Vivo en el contexto global.';

function hacerAlgo() {
  var ambito = 'Vivo y me declararon en un contexto local.';
  console.log(ambito);
}

function hacerOtraCosa() {
  ambito = 'Siendo de un contexto global me modificaron en un contexto local.';
  console.log(ambito);
}

// Vivo en un contexto local.
hacerAlgo();

// Siendo de un contexto global me modificaron en un contexto local.
hacerOtraCosa();

// Siendo de un contexto global me modificaron en un contexto local.
console.log(ambito);
```

## Contexto

El contexto siempre es el valor de `this`, que es una referencia al objeto que "posee" el código que se esté ejecutando en el momento.

## Ambiente de Variables

Una variable se puede definir en cualquier ámbito:

 - Global

 - Local

esto establece el `acceso` a las variables en diferentes ámbitos durante el tiempo de ejecución.

### Globales

Cualquier variable global declarada fuera del cuerpo de una función vivirá durante todo el tiempo de ejecución y puede ser accesada y alterada desde cualquier ámbito.

### Locales

Las variables locales sólo existen dentro del cuerpo de la función en que hayan sido declaradas y siempre tendrán un ámbito diferente por cada invocación que se realice a la función donde viven. Por lo tanto, sólo pueden ser recuperadas, asignadas y manipuladas dentro de esa llamada y no son accesibles fuera de ese ámbito.

### Ambito de Bloque / "Block Scope"

Es la capacidad de definir una variable para el ámbito de un bloque:

 - Una sentencia `if` o `switch`.

 - Un bucle `for` o `while`.

### ES5 - Ambito de Función

> Motores de JavaScript compatibles con el estándar ECMAScript 5 no son amigables con el concepto de "Ambito de Bloque". Sin embargo el estándar ECMAScript 2015 (ES6) sí lo soporta con la introducción y el uso de la sentencia `let`.

Dentro de la Compatibilidad con el estándar ECMAScript 5 y usando `var` permite que las variables definidas dentro de un bloque sean accesibles fuera del bloque.

> Brendan Eich: 10 días no dejaron tiempo para habilitar el ámbito de bloque. También muchos "lenguajes de script" de a mediados de los años 90's con costos tenían ámbito, además más tarde crecieron.

```javascript
var soyGlobal = 'Vivo en el ámbito global';
tambienSoyGlobal = 'Tambíen vivo en el ámbito global';

if (true) {
  soyGlobal = 'Sigo viviendo en el ámbito global.'
  var soyDeBloque = 'Soy global, pero nací dentro de un bloque.';
}

soyDeBloque = 'Siempre he sido global.'

console.log(soyGlobal);    // Sigo viviendo en el ámbito global.
console.log(soyDeBloque);  // Siempre he sido global.
```

Si estamos en una función `var` crea una variable local, "sin var" el motor de JavaScript buscará en la cadena de ámbito hasta que encuentre la variable llegue el ámbito global (momento en el que la creará si no existía en el acadena de ámbito).

```javascript
// Ambas variables son globales.
var orson = 'Orson Global';
mork = 'Orson Global';

function estudiarComportamiento() {
  var orson = 'Orson Local';       // Local.
  mork = 'Mork Global en Función'; // Global.

  // Función anónima auto-ejecutada.
  (function() {
    var fred = 'Fred Local';    // Local.
    orson = 'Orson que Hereda'; // Hereda de la cadena de ámbito (crea un closure).
    mindy = 'Mindy Global';     // Global.
  }())
}

estudiarComportamiento();

console.log(orson);  // Orson Global.
console.log(mork);   // Mork Global en Función.
console.log(mindy);  // Mindy Global.
```

### ES6 - Ambito de Bloque

Dentro de la Compatibilidad con el estándar ECMAScript 2015 (ES6) y usando `let` cualquier variable con ámbito de bloque es imposible de acceder desde afuera de la apertura y el cierre de sus llaves.

```javascript
if (true) {
  const platon = 'Constante con ámbito de bloque.';
  let aristoteles = 'Constante con ámbito de bloque.';
}

console.log(platon);      // not defined error.
console.log(aristoteles); // not defined error.
```

```javascript
let soyGlobal = 'Vivo en el ámbito global';

if (true) {
  // var soyGlobal; // Duplicate declaration "soyGlobal".
  let soyGlobal = 'Vivo en el ámbito local a un bloque y soy diferente al global.'
  let soyDeBloque = 'Vivo en el ámbito local a un bloque.';
}

console.log(soyGlobal);    // Vivo en el ámbito global.

soyDeBloque = 'Yo no estoy seguro de nada.'

console.log(soyDeBloque);  // soyDeBloque is not defined.
```

## Peculiaridades

Javascript es un lenguaje bastante interesante, siempre y cuando seamos conscientes de sus peculiaridades.

```javascript
var clan = ['Hattori Hanzō', 'Fūma Kotarō', 'Fujibayashi Nagato'];

for(var i = 0; i < clan.length; i++) {
  var ninja = clan[i];
  console.log(ninja);
}
// Hattori Hanzō.
// Fūma Kotarō.
// Fujibayashi Nagato.
```

### Ambito de Bloque en Funciones de Primer Orden

El siguiente fragmento de código utiliza: `Funciones de Primer Orden`. Las funciones son valores que se pueden asignar o empujar en una variable, incluyendo los arreglos también.

```javascript
var clan = ['Hattori Hanzō', 'Fūma Kotarō', 'Fujibayashi Nagato'];
var arregloDeFuncionesDePrimeraClase = [];

for (var i = 0; i < clan.length; i++) {
  var ninja = clan[i];

  /**
   * Se construye un arreglo llamado arregloDeFuncionesDePrimeraClase con funciones adentro
   * que imprimen un elemento de la lista.
   */
  arregloDeFuncionesDePrimeraClase.push(function() {
    console.log('ninja => ', ninja);
  });
}

/**
 * Mediante `arregloDeFuncionesDePrimeraClase` es que podremos elegir e
 * invocar cualquierade las funciones del arreglo construido en el bucle for.
 *
 * ¿En el fondo esto tiene buena pinta?
 */

// arregloDeFuncionesDePrimeraClase =>  [ [Function], [Function], [Function] ]
console.log('arregloDeFuncionesDePrimeraClase => ', arregloDeFuncionesDePrimeraClase);

// arregloDeFuncionesDePrimeraClase.length =>  3
console.log('arregloDeFuncionesDePrimeraClase.length => ', arregloDeFuncionesDePrimeraClase.length);

// Invoca la primera función del arreglo de funciones.
arregloDeFuncionesDePrimeraClase[0](); // ninja =>  Fujibayashi Nagato.

// Invoca la segunda función.
arregloDeFuncionesDePrimeraClase[1](); // ninja =>  Fujibayashi Nagato.

// Invoca la última.
arregloDeFuncionesDePrimeraClase[2](); // ninja =>  Fujibayashi Nagato.

// Invoca una función inexistente dentro del arreglo de funciones.
arregloDeFuncionesDePrimeraClase[3]();
// TypeError: arregloDeFuncionesDePrimeraClase[3] is not a function.
```

Hmm, todas las funciones invocadas imprimieron el valor: `Fujibayashi Nagato.`

Esto sucede porque el bucle `for` no posee `ámbito de bloque`. En el caso anterior, una vez finalizado el bucle `for` se invocan las funciones del arreglo, entonces el valor de `ninja` va a estar apuntando al último valor del índice `i` que haya hecho finalizar al bucle `for`.

```javascript
var i;

// "i" siempre ha sido una variable global dentro de un bloque sin ámbito.
for (i = 0; i < clan.length; i++)
```

## Ambito Artificial

Implica crear una nueva función que debe ser automáticamente invocada de inmediato, también conocida como una `función anónima auto-invocada`.

```javascript
var ninjas = ['Hattori Hanzō', 'Fūma Kotarō', 'Fujibayashi Nagato'];
var clan = [];

for (var i = 0; i < ninjas.length; i++) {
  /**
  * Define una función anónima e inmediatamente la invoca.
  */
  (function() {
    var ninja = ninjas[i];
    clan.push(function() {
      console.log(ninja);
    });
  }());
}

// Sólo una alternativa que sirve para optimizar el bucle for.
for (var i = 0, l = ninjas.length; i !== l; i++) {
  clan[i]();
}
// Hattori Hanzō.
// Fūma Kotarō.
// Fujibayashi Nagato.
```

Lo que sucedió es que por cada iteración del bucle `for` se utiliza un ámbito nuevo, que contiene una variable `ninja` propia, lo que permite que las funciones referencien a un `ninja` diferente. Por esta razón, al invocar `clan[2]()` se obtiene el resultado pensado.

## El contexto de "this"

```javascript
var rootScope = this;

if (rootScope === this) {
  console.log('Somos lo mismo');
}

// window es el contexto por defecto.
if (window === this) {
  console.log('También somos lo mismo');
}
```

En general el contexto se determina por cómo se invoca una función. Cuando una función se invoca como un método de un objeto, `this` referencia al objeto del método del cual es llamado.

> Un objeto literal es una lista que envuelve entre llaves una colección de pares de nombre:valor separados por coma.

```javascript
var autor = {
  nombre: 'Édith Piaf',
  cancion: 'La Vie En Rose',
  pais: 'Francia'
}
```

> Los valores de las propiedades de un objeto literal pueden ser de cualquier tipo de datos, por ejemplo: arreglos, funciones, incluso otros objetos literales anidados.

```javascript
var unObjetoLiteral = {
  compare: function(){
    console.log(this === unObjetoLiteral);    
  }
};

unObjetoLiteral.compare(); // true
```

El mismo principio se aplica al invocar una función con el operador `new` que sirve para crear una nueva instancia de un objeto. Cuando se invoca de esta manera, el valor de `this` dentro del ámbito de la función referencia a la instancia recién creada:

```javascript
function invocar() {
  console.log(' => ', this);
}

invocar()       // => Window Object. Undefined en modo 'strict'.

new invocar()   // => invocar {}.
```

## El contexto se puede alterar con Call() y Apply()

```javascript
var unObjetoLiteral = {
  compare: function(arg1, arg2, arg3) {
    console.log('arg1', arg1);
    console.log('arg2', arg2);
    console.log('arg3', arg3);
    console.log('----------');    
    console.log('(this === unObjetoLiteral) ', this === unObjetoLiteral);
    console.log('(this === window) ', this === window);
    console.log('----------');    
  }
};

unObjetoLiteral.compare(); // true

// Cambiar el contexto que va a disparar "this"
var arg1 = 'Call usa un argumento';
unObjetoLiteral.compare.call(window, arg1); // false

// Cambiar el contexto que va a disparar "this"
var args = ['Apply usa', 'un arreglo de', 'argumentos'];
unObjetoLiteral.compare.apply(window, args); // false
```

`Resultado`:

```javascript
arg1 undefined
arg2 undefined
arg3 undefined
----------
(this === unObjetoLiteral)  true
(this === window)  false
----------
arg1 Call usa un argumento
arg2 undefined
arg3 undefined
----------
(this === unObjetoLiteral)  false
(this === window)  true
----------
arg1 Apply usa
arg2 un arreglo de
arg3 argumentos
----------
(this === unObjetoLiteral)  false
(this === window)  true
----------
```

## Bind()

La función `bind()` crea una nueva función (`"una función ligada"`) con el mismo cuerpo de la función que posee la función a la que se está invocando con el valor de `this` ligado al primer argumento de bind().

Con `bind()` también es posible pasar argumentos a la función objetivo cuando es invocada. Una `función ligada` también puede ser creada usando el operador `new`: hacerlo hace que actúe como si la función de destino ya hubiera sido construida. El valor proporcionado de `this` se ignora, mientras que los argumentos se proporcionan a la función que se emula.

```javascript
var unObjetoLiteral = {
  compare: function(arg1, arg2, arg3) {
    console.log('arg1', arg1);
    console.log('arg2', arg2);
    console.log('arg3', arg3);
    console.log('----------');    
    console.log('(this === unObjetoLiteral) ', this === unObjetoLiteral);
    console.log('(this === window) ', this === window);
    console.log('----------');    
  }
};

var funcionQueEngoma = unObjetoLiteral.compare.bind(window);

var args = ['Bind usa', 'argumentos', 'separados por coma'];
funcionQueEngoma(args[0], args[1], args[2]); // (this === window)  true

unObjetoLiteral.compare(); // (this === unObjetoLiteral)  true
```
