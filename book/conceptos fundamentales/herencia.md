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

# "Herencia" con Object.create()

```javascript
var Abuela = { ojos: 'Verdes' }

var Padre = Object.create(Abuela);
```

```javascript
Abuela

Object {ojos: "Verdes"}
```

```javascript
Padre

Object {
  __proto__: {
    ojos: "Verdes"
  }
}
```

```javascript
// __proto__
Padre.ojos

"Verdes"
```

```javascript
Padre.cabello = 'Colochos';
```

```javascript
Padre

Object {
  cabello: "Colochos",
  Object __proto__: {
    ojos: "Verdes"
  }
}
```

```javascript
Abuela.cabello
undefined

Padre.cabello
"Colochos"
```

```javascript
var Hija = Object.create(Padre);

Hija.labios = 'Gruesos';
```

```javascript
Hija

Object {
  labios: "Gruesos",
  Object __proto__ {
    cabello: "Colochos",
    Object __proto__ {
      ojos: "Verdes"
    }
  }
}
```

```javascript
Hija.ojos
"Verdes"

Hija.cabello
"Colochos"

Hija.labios
"Gruesos"
```

```javascript
Hija.piernas = 'Largas';
```

```javascript
Hija

Object {
  labios: "Gruesos",
  piernas: "Largas",
  Object __proto__ {
    cabello: "Colochos",
    Object __proto__ {
      ojos: "Verdes"
    }
  }
}
```

```javascript
Hija.ojos
"Verdes"

Hija.cabello
"Colochos"

Hija.labios
"Gruesos"

Hija.piernas
"Largas"
```

```javascript
Abuela.ojos
"Verdes"

Abuela.cabello
undefined

Abuela.piernas
undefined
```

```javascript
Padre.cabello = 'Lacio'

console.log(Hija.ojos, Hija.cabello, Hija.labios, Hija.piernas);
// Verdes Colochos Gruesos Largas
```

```javascript
Abuela.ojos = 'Azules'

console.log(Hija.ojos, Hija.cabello, Hija.labios, Hija.piernas);
// Azules Colochos Gruesos Largas
```

# Herencia Múltiple con Mixins

```javascript
function constructor() {
    this.nombre = '';
    this.apellido = [];
    this.email = '';
}

function Padre(hijo, apellido) {
    hijo.apellido[0] = apellido;
}

function Madre(hijo, apellido) {
    hijo.apellido[1] = apellido;
}

function Hijo(nombre, apellido) {
    constructor.call(this);

    this.nombre = nombre;  
    Padre(this, apellido[0]);
    Madre(this, apellido[1]);
}

Hijo.prototype = Object.create(constructor.prototype);
```

```javascript
// Sólo con el primer apellido.
var vos = new Hijo('Hattori', ['Hanzō']);

var tu = new Hijo('Fujibayashi', ['Goemon', 'Muneyoshi']);

// Sólo con el segundo apellido.
var el = new Hijo('Fūma', [, 'Kotarō']);
```

```javascript
vos.apellido[1] = 'Chiyome';
vos.email = 'hattori@hanzo.vos';
vos.edad = 105;

vos

hijo {nombre: "Hattori", apellido: Array[2], email: "hattori@hanzo.vos", edad: 105}
```
