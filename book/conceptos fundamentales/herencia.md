# Herencia
Relacionar métodos y/o propiedades de un objeto a otro.

```javascript
var calculadora = {
    sumar: function(num1, num2) {
      return num1 + num2;
    },
    restar: function(num1, num2) {
      return num1 - num2;
    }
}

var cal = Object.create(calculadora); /* Hereda las propiedades de calculadora */

cal.sumar(2,2);  // 4
cal.restar(2,2); // 0
```