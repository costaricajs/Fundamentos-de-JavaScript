# Currying
Consiste en convertir una función con múltiples parámetros / arity en diferentes funciones con menos parámetros.

```javascript
// función sin formato currying
var persona = function(nombre, primerApellido, segundoApellido) {
  return 'Mi nombre es ' + nombre + ' ' + primerApellido + ' ' + segundoApellido;
}
// función con formato currying
var persona = function (nombre) {
  return function (primerApellido) {
    return function (segundoApellido) {
      return 'Mi nombre es ' + nombre + ' ' + primerApellido + ' ' + segundoApellido;
    }
  }
};

var Jhon = persona('Jhon')('Doe');
Jhon('Blast'); // Mi nombre es Jhon Doe Blast
```