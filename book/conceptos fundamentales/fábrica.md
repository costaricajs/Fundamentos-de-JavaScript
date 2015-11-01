# Fábrica
Es una función que retorna un nuevo objeto.

```javascript
function calculadora() {
  return {
    sumar: (num1, num2) => { return num1 + num2; },
  };
}

const cal = calculadora();
cal.sumar(1, 2);
```