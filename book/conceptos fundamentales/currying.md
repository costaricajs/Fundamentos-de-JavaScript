# Currying
Consiste en convertir una función con múltiples parámetros / arity en diferentes funciones con menos parámetros.

```javascript
// función sin formato currying (SC = sin currying)
const personaSC =
  (nombre, primerApellido, segundoApellido) =>
    'Mi nombre es ' + nombre + ' ' + primerApellido + ' ' + segundoApellido;

personaSC('Jhon', 'Doe', 'Blast'); // Mi nombre es Jhon Doe Blast

// función con formato currying (CC = con currying)
const personaCC =
  (nombre) =>
    (primerApellido) =>
      (segundoApellido) =>
        'Mi nombre es ' + nombre + ' ' + primerApellido + ' ' + segundoApellido;

const jhon = personaCC('Jhon')('Doe');
jhon('Blast'); // Mi nombre es Jhon Doe Blas
```