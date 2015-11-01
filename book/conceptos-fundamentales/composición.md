# Composición
Cuando combinamos dos o más funciones para crear una nueva, la cual contiene las funciones anteriores.

```javascript
const caminador = (nombre) => ({
  caminar: () => console.log(nombre + ' está caminando'),
});

const hablador = (nombre) => ({
  hablar: () => console.log(nombre + ' está hablando'),
});

const persona = (nombre) => Object.assign({}, caminador(nombre), hablador(nombre));

const jhon = persona('Jhon');
jhon.caminar(); // Jhon está caminando
jhon.hablar();  // Jhon está hablando
```