# Funciones en Cadena

Técnica para simplificar la ejecución de múltiples métodos sobre una misma variable u objeto.

```javascript
var cal = function(num) {
  var num = num || 0;
  return {
    sumar: function(num2){
      num = num + num2;
      return this;           /* retorna this el cual contine sumar, restar e imprimirTotal */
    },
    restar: function(num2){
      num = num - num2;
      return this;          /* retorna this el cual contine sumar, restar e imprimirTotal */
    },
    imprimirTotal: function(){
      console.log(num);
      return this;          /* retorna this el cual contine sumar, restar e imprimirTotal */
    }
  }
};

var calculator = cal(10);   /* num = 10 */

calculator.sumar(10)        /* num = 20 */
          .restar(2)        /* num = 18 */
          .sumar(5)         /* num = 23 */
          .imprimirTotal(); // 23
```