# Encapsulación
Nos permite conservar declaraciones públicas y privadas en un mismo objeto.

```javascript
const seguridad = () => {
  // Declaraciones Privadas
  const tarjetaCredito = '1111-2222-3333';

  return {
    // Declaraciones Públicas
    mostrarTarjetaCredito: () => {
      console.log('Tu tarjeta de crédito es ' + tarjetaCredito);
    },
  };
};

const sec = seguridad();

sec.mostrarTarjetaCredito();   // Tu tarjeta de crédito es 1111-2222-3333

sec.tarjetaCredito = '11';     /* Si intentas cambiar el valor ... No es posible */

sec.mostrarTarjetaCredito();   // Tu tarjeta de crédito es 1111-2222-3333
```