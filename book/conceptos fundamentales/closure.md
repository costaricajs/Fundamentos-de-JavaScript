# Closure
Cuando una función utiliza una variable la cual fue declarada fuera de dicha función.

```javascript
const imprimir = (() => {
  const saludo = 'hola';         /* Se define una variable */
  function imprimirSaludo() {
    console.log(saludo);       /* <- Closure: Se conserva el acceso a la variable h */
  }
  return imprimirSaludo;
})();

imprimir(); // =>  'hola'
```