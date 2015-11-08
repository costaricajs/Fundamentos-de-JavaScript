# Funciones en Cadena [Method Chaining]

Técnica para simplificar la ejecución de múltiples métodos sobre una misma variable u objeto.

```javascript
const cal = (num) => {
  let total = num || 0;
  return {
    sumar(num2) {
      total = total + num2;
      return this;           /* retorna this el cual contine sumar, restar e imprimirTotal */
    },
    restar(num2) {
      total = total - num2;
      return this;          /* retorna this el cual contine sumar, restar e imprimirTotal */
    },
    imprimirTotal() {
      console.log(total);
      return this;          /* retorna this el cual contine sumar, restar e imprimirTotal */
    },
  };
};

const calculator = cal(10);   /* num = 10 */

calculator.sumar(10)        /* num = 20 */
          .restar(2)        /* num = 18 */
          .sumar(5)         /* num = 23 */
          .imprimirTotal(); // 23
```