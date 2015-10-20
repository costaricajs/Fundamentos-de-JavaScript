# Closure
Cuando una función utiliza una variable la cual fue declarada fuera de dicha función.

```javascript
var imprimir = (function(){
  var h = 'hola';         /* Se define una variable */
  function imprimirH(){
    console.log(h);       /* <- Closure: Se conserva el acceso a la variable h */
  }
  return imprimirH;
})();

imprimir(); // =>  'hola'
```