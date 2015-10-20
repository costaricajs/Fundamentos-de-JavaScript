# Funciones de Orden Mayor 
Es una función que puede recibir otra función como parámetro, la cúal puede ser invocada por la función de order mayor.

```javascript
function sumar(num) {
  return num + 10
}

/* map es una función de Array que recibe otra función. 
   retorna un nuevo arreglo con los resultado de ejecutar la función recibida 
   con cada uno de los elementos del arreglo como parámetro  */
var totalSuma = [1,2,3].map(sumar); // [11, 12, 13]
```

Las funciones que son enviadas como parámetros muchas veces son llamadas __callbacks__. 