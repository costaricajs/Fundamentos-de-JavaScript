# Polimorfismo
La posibilidad de llamar métodos en común de diferentes objectos sin alterar el resultado.

```javascript
function fruta(ancho, alto) {
  return {
    descripcion() {
      console.log('A. Dimensión de Fruta: ancho-' + ancho + ' / alto-' + alto);
    },
  };
}

function mercado(ancho, alto, precio) {
  return {
    descripcion() {
      console.log('B. Dimensión de Fruta: ancho-' + ancho + ' / alto-' + alto + ' / $' + precio);
    },
  };
}

function mostrarDescripcion(obj) {
  if (typeof obj.descripcion === 'function') {
    obj.descripcion(); /* <-- Polimorfismo */
  }
}

const miFruta = fruta(50, 60);
const miMercado = mercado(50, 60, 25);

mostrarDescripcion(miFruta);    // A. Dimensión de Fruta: ancho-50 / alto-60
mostrarDescripcion(miMercado);  // B. Dimensión de Fruta: ancho-50 / alto-60 / $25
```