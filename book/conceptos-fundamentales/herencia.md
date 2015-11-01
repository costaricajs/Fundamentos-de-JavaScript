# Herencia
Relacionar métodos y/o propiedades de un objeto a otro.

```javascript
const calculadora = {
  sumar(num1, num2) {
    return num1 + num2;
  },
  restar(num1, num2) {
    return num1 - num2;
  },
};

const cal = Object.create(calculadora); /* Hereda las propiedades de calculadora */

cal.sumar(2, 2);  // 4
cal.restar(2, 2); // 0
```