# Comportamiento Hoisting

> Hoisting cae en uno de esos conceptos que traducido al español simplemente no se siente bien.

Antes de entender el comportamiento hoisting propio del motor de JavaScript, es necesario tener claro que todo comportamiento puede derivar en un "resultado inesperado" si no se conoce el funcionamiento interno de la declaración y la asignación de variables en relación con su propio alcance de acuerdo al `ámbito/scope` en el que se encuentre.

En realidad JavaScript no es raro o inesperado, es sólo adaptable e increíble. Si se conocen las perillas adecuadas se puede controlar su comportamiento y eso es algo destacable de su motor. Escarbemos un poco más profundo jugando con la consola:

```
console.log(no);
```

`ReferenceError: no is not defined`

```
no;
```

`ReferenceError: no is not defined`

## Asignación

Una variable se puede usar antes de haber sido declarada:

```
si = 1;
```

`1`

```
console.log(si);
```

`1`

## Declaración

Es válido que una variable se declare después de haber sido usada.

```
var si;

console.log(si);
```

`1`

```
var tampoco;

console.log(tampoco);
```

`undefined`

## Declararación y Asignación

```
var hmm = 'pensando...';

console.log(hmm);
```

`'pensando...'`

```
var con = 'libros';

console.log(con, hay)
```

`ReferenceError: hay is not defined`

```
var hay = 'progreso'

console.log('Con ' + con + ' hay ' + hay)
```

`Con libros hay progreso`

## Comportamiento Hoisting

Hoisting no se trata de mover manualmente todas las declaraciones de variables al inicio del ambiente actual. Esto es algo que el motor de JavaScript hace por nosotros, se puede pensar en esta transformación como el resultado de un comportamiento interno propio de JavaScript.

Hoisting es más fácil de masticar con un ejemplo:

```javascript
elevarExperimento();

function elevarExperimento() {
  invocarOtraFuncion();

  // Variable en el ámbito local a la función.
  var gato = 'Schrödinger.';

  console.log(gato);
}

function invocarOtraFuncion() {
  console.log('Por alguna razón alguién me invocó.');
}
```

el cuerpo de la función `elevarExperimento()` de manera automática se interpreta como:

```javascript
function elevarExperimento() {
  var gato;

  invocarOtraFuncion();

  gato = 'Schrödinger';

  console.log(gato);
}
```

Una forma sencilla de alterar el comportamiento de hoisting se logra sólo con introducir una variable en el ámbito global:

```javascript
// Variable en el ámbito global.
var gato = 'No estoy ni muerto ni vivo, soy un perro que está fuera de la caja.';

function elevarExperimento() {
  console.log(gato); // undefined
  invocarOtraFuncion();
  var gato = 'Schrödinger';
  console.log(gato);
}

function invocarOtraFuncion() {
  console.log('Por alguna razón alguién me invocó.');
}

elevarExperimento();
```

en el primer `console.log()` esperabamos ver el valor global, pero no sucede porque internamente el motor de JavaScript interpreta que debe elevar la declaración de `var gato` al inicio de la función:

```javascript
function elevarExperimento() {
  var gato;

  console.log(gato); // undefined
  invocarOtraFuncion();

  gato = 'Schrödinger';

  console.log(gato);
}
```

Una manera bastante interesante de alterar el comportamiento "hoisting" del motor de JavaScript se puede comprobar pasando la variable del ámbito global como parametro de la función, por ejemplo:

```javascript
var gato = 'No estoy ni muerto ni vivo, soy un perro que está fuera de la caja.';

function elevarExperimento(gato) {
  console.log(gato); // 'No estoy ni ... fuera de la caja.'
  invocarOtraFuncion();
  var gato = 'Schrödinger';
  console.log(gato);
}

function invocarOtraFuncion() {
  console.log('Por alguna razón alguién me invocó.');
}

elevarExperimento(gato);
```

Por esta razón la mayoría de desarrolladores recomiendan brindar legibilidad al código declararando las variables al principio de su ámbito, esto también permite detectar `comportamientos desconocidos` o errores con mayor facilidad.

```javascript
function soyUnDesarrolladorCivilizado() {
  var nombre = 'Hattori Hanzō';
  var posicion = 'Ninja';
  var habilidad = 'Invisibilidad';
  var extension = 'Katana';

  liderarUnClan();
  unirUnaNacion();
}
```

En el fondo este tema es mucho más extenso, si se juega y escarba un poco más se pueden descubrir más `comportamientos desconocidos`, que suena mucho mejor que `raro` o `inesperado`.
