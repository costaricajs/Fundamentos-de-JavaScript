# Composición
Cuando combinamos dos o más funciones para crear una nueva, la cual contiene las funciones anteriores.

```javascript
var caminar = function caminar(nombre) {
  console.log(nombre + ' está caminando');
};

var hablar = function hablar(nombre) {
  console.log(nombre + ' está hablando');
};

var persona = function persona(nombre) {
  return Object.assign({}, caminar(nombre), hablar(nombre));
};

var Jhon = persona('Jhon');
Jhon.caminar; // Jhon está caminando
Jhon.hablar; // Jhon está hablando
```