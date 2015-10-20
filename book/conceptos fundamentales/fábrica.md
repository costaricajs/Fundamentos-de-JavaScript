# Fábrica
Es una función que retorna un nuevo objeto.

```javascript
function calculadora() {
  return { 
    sumar: function(num1, num2) { return num1 + num2; }
  }
}

var cal = calculadora();
cal.sumar(1,2);
```