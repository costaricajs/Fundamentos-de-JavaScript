# Pila

JavaScript es un lenguaje que corre sobre un único hilo, es decir, sólo una tarea a la vez se puede correr. Cuando el motor de JavaScript corre código, entra por primera vez a un `contexto de ejecución global`. Cada invocación de una función a partir de este punto dará lugar a la creación de un `nuevo contexto de ejecución`.

Conceptos clave sobre la `Pila`:

 - Corre sobre un solo proceso o hilo.
 - Su ejecución es sincrónica.
 - Sólo hay un único Contexto Global.
 - Pueden haber muchos Contextos de Ejecución.
 - Cada inovación a una función crea un nuevo Contexto de Ejecución, incluso una llamada a sí misma.

```javascript
// Contexto de Ejecucion Global.

function user() {          // Nuevo Contexto de Ejecución.

  function email() {       // Nuevo Contexto de Ejecución.
    // ...
  }

  function geolocation() { // Nuevo Contexto de Ejecución.
    // ...
  }
}
```

El término "contexto de ejecución" en realidad se refiere más al ámbito y no al contexto.

```
+------------------------------+
| contexto de ejecución actual |
+------------------------------+
| contexto de ejecución n + 2  |
+------------------------------+
| contexto de ejecución n + 1  |
+------------------------------+
| contexto de ejecución global |
+------------------------------+
```

# Contextos de ejecución

Cada vez que un nuevo contexto de ejecución se crea, este se agrega a la parte superior de la pila de ejecución. Nuestro navegador Web siempre ejecutará el contexto de ejecución actual, el que esté en la cima de la pila de ejecución. Una vez completado, se retira de la parte superior de la pila y el control volverá al contexto de ejecución siguiente.

El `contexto de ejecución` se puede dividir en dos fases:

 - Fase 1 - Creación:
    - Crea la cadena de ámbito.
    - Crea la variables, las funciones y los argumentos.
    - Determina el valor de `this`.
 - Fase 1 - Ejecución:
   - Asigna valoress
   - Crea referencias a functiones.
   - Interpreta / Corre código.

`Objeto de Activación [OA] / Variable de Objecto [VO]`

En la fase de creación, el intérprete de JavaScript lo primero que hace es crear una `variable de objeto`, también llamada `objeto de activación`, que se compone de todas las variables, declaraciones de funciones y argumentos definidos dentro de ese contexto de ejecución. A partir de ahí la `cadena de ámbito/scope chain` se inicializa, por último se determina el valor de `this`. Seguidamente, en la fase de ejecución, el código es interpretado y ejecutado.

## La cadena de ámbito

Para cada `contexto de ejecución` hay una `cadena de ámbito` junto con este. La cadena de ámbito contiene la variable objeto por cada contexto de ejecución en la pila de ejecución. Se utiliza para determinar el acceso a variables y para la resolución de identificadores. Por ejemplo:

```javascript
var cero = 0;

function primero() {
  var uno = 1;
  segundo();

  function segundo() {
    var dos = 2;
    tercero();

    function tercero() {
      var tres = 3;
      var uno = 'uno';
      cuarto();

      /**
       * cuarto() tiene acceso a todas las variables globales y también a
       * todas las variables definidas dentro de todas las funciones anteriores.
       */
      function cuarto() {
        console.log(cero);  // 0
        console.log(uno);   // uno
        console.log(dos);   // 2
        console.log(tres);  // 3
      }
    }
  }   
}

primero();
```

Cada vez que se intente acceder a una variable desde el contexto de ejecución de una función, el proceso de consulta siempre comenzará con su propia `variable objeto`. Si el identificador no se encuentra en su propia variable objeto, la búsqueda continúa en la `cadena de ámbito`. Sube por la cadena de ámbito y examina la variable objeto de cada `contexto de ejecución` en busca de una coincidencia con el nombre de la variable.
