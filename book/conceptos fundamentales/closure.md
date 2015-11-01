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

## Re-utilización inteligente del código

El acceso a las variables fuera del `ámbito léxico` inmediato crea un `cierre`. En otras palabras, se forma un `closure` cuando una función anidada se define dentro de otra función, permitiendo el acceso a las variables de las función externa.

El hecho de retornar una función anidada permite mantener el acceso a las variables locales, argumentos y declaraciones de funciones internas de la función externa.

```javascript
function encapsulacion() {
  var _unaPropiedadPrivada = 'una propiedad privada';

  function _metodoPrivado(arg){
    return 'Soy un método privado alterando ' + arg;
  }

  return function metodoPublico() {
    return _metodoPrivado(_unaPropiedadPrivada);
  }
}

var obtenerVariable = encapsulacion();
obtenerVariable() // 'Soy un método privado alterando una propiedad privada'.
```

## Para minimizar colisiones

Este tipo de encapsulación básico nos permite `ocultar` y `preservar` el contexto de ejecución de ámbitos externos, al mismo tiempo `expone` una interfaz pública que pueda ser compartida y reutilizada en el futuro.

Uno de los tipos más populares de `closures` es el famoso `patrón de módulo`; el cual permite emular miembros públicos, privados y también privilegiados:

> El patrón de módulo se definió para proporcionar algo parecido a la encapsulación privada y pública de clases de la ingeniería convencional de software.

## Closures en Patrón de Módulo

El `patrón de módulo` encapsula "privacidad", estado y organización utilizando `closures`.

Sirve para proporcionar una manera sencilla de envolver, mezclar variables, tener piezas privadas y exponer métodos mediante una especie de interfaz pública.

### Privacidad

Proteje a ciertas piezas de filtrarse en el ámbito global y de chocar accidentalmente con alguna otra interfaz. Con el patrón de módulo, solamente se devuelve una API pública, manteniendo todo lo demás dentro del `closure` privado.

```javascript
var Modulo = (function() {
  var _unaPropiedadPrivada = 'una propiedad privada';

  function _unMetodoPrivado(args) {
    console.log('_unMetodoPrivado => ', args);
  }

  // Retorna un objeto literal.
  return {
    unaPropiedadPubica: 'una propiedad pública',

    unMetodoPublico: function(args) {
      console.log('unMetodoPublicoPuro => ', args);
    },

    unMetodoPrivilegiado: function(args) {
      return _unMetodoPrivado(args);
    }
  };
})();

var config = {
  expandir: true
};

console.log(Modulo.unaPropiedadPubica); // una propiedad pública

Modulo.unMetodoPublico(config);         // unMetodoPublico =>  { expandir: true }

Modulo.unMetodoPrivilegiado(config);    // _unMetodoPrivado =>  { expandir: true }
```

### Interfaz Pública

El `patrón de módulo` expone una interfaz que otras partes de nuestra aplicación pueden utilizar. Este patrón es muy similar a una expresión funcional inmediatamente-invocada (`IIFE`), excepto que en este caso devolvemos un objeto en lugar de una función.

### ¿Que permite () al final de la función?

El módulo actúa como si fuera un `singleton`, corre tan pronto como el compilador lo interpreta, por eso, la apertura y cierre de paréntesis al final de la función. Los únicos miembros disponibles fuera del contexto de ejecución del `closure` son sus métodos y propiedades ubicadas en el objeto público que se retorna. Sin embargo, todas las propiedades y métodos privados vivirán toda la vida de la aplicación mientras el contexto de ejecución se preserve, esto signifca que las variables pueden llegar a ser objeto de interacción via los métodos públicos.

## IIFE - Expresión de Función Inmediatamente-Invocada

Otro tipo más de `closure` es `IIFE`, que no es más que una función anónima auto-invocada que en este caso corre en el contexto de `window`:

```javascript
(function(window) {

  var _unaPropiedadPrivadaa;

  function _unMetodoPrivado() {
    console.log('_unMetodoPrivado');
  }

  window.Module = {

    public: function() {
      // do something
    }
  };

})(this);
```

## Interfaz Global

Este tipo de expresión es bastante útil cuando se trata de preservar el `espacio de nombres global`/`namespace` así como las variables declaradas dentro del cuerpo de la función serán locales al `closure` y viviran a lo largo de todo su tiempo de ejecución.

```javascript
(function(window) {
  var _unaPropiedadPrivadaa;

  function _unMetodoPrivado(args) {
    console.log('_unMetodoPrivado => ', args);
  }

  window.Modulo = {

    unMetodoPublico: function(args) {
      console.log('unMetodoPublico => ', args);
    },

    unMetodoPrivilegiado: function(args) {
      _unMetodoPrivado(args);
    }
  };

  this.Modulo.unMetodoPublico('IIFE');
  window.Modulo.unMetodoPublico('IIFE');

  this.Modulo.unMetodoPrivilegiado('IIFE');
  window.Modulo.unMetodoPrivilegiado('IIFE');
})(this);

this.Modulo.unMetodoPublico('AFUERA');
window.Modulo.unMetodoPublico('AFUERA');

this.Modulo.unMetodoPrivilegiado('AFUERA');
window.Modulo.unMetodoPrivilegiado('AFUERA');

// unMetodoPublico  =>  IIFE
// unMetodoPublico  =>  IIFE
// _unMetodoPrivado =>  IIFE
// _unMetodoPrivado =>  IIFE
// unMetodoPublico  =>  AFUERA
// unMetodoPublico  =>  AFUERA
// _unMetodoPrivado =>  AFUERA
// _unMetodoPrivado =>  AFUERA
```

## Closure agrega interacción

Con `closures` se puede encapsular código, por esta razón esta técnica la re-utilizan una gran basta cantidad de aplicaciones, librerías y `frameworks`. Por lo general se usa para exponer una `interfaz global`, esto permite a nuestra aplicación y probablemente a otras aplicaciones el poder interactuar con una `interfaz pública` fácil de re-usar y configurar.
