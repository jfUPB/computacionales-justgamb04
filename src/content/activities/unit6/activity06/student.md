## Patrón Observer en mi proyecto

### Dónde implementé el Subject?

Implementé el **sujeto** como una clase `InputSubject` en `sketch.js`, la cual centraliza el evento de nuevos datos desde el micro\:bit o el móvil, y notifica a todos los observadores registrados:

```javascript
class InputSubject {
  constructor() {
    this.observers = [];
  }

  addObserver(observer) {
    this.observers.push(observer);
  }

  notify(data) {
    for (let obs of this.observers) {
      obs.onNotify(data);
    }
  }
}
```

### Qué clase(s) implementaron el rol de Observador?

Las clases que implementaron el rol de **Observer** fueron, por ejemplo, `ColorController` y `ShapeGenerator`. Ambas reaccionaban al input para modificar el color o tipo de figura:

```javascript
class ColorController {
  onNotify(data) {
    this.color = color(map(data.x, -1024, 1024, 0, 255), 100, 150);
  }
}
```

```javascript
class ShapeGenerator {
  onNotify(data) {
    this.shape = data.z > 1000 ? "circle" : "square";
  }
}
```

### Qué eventos notificaba el Sujeto y por qué Observer?

El `InputSubject` notificaba eventos como:

* Nuevos datos seriales del micro\:bit (`{x, y, z}`)
* Eventos táctiles del móvil (`{touchX, touchY}`)

Usé Observer para desacoplar el origen de datos de los componentes que los usan. Esto permitió tener múltiples reacciones independientes a un mismo evento sin invocar directamente funciones, lo cual mejora la escalabilidad del sistema.

### Dónde se usa notify y dónde reaccionan los observadores?

```javascript
// Dentro de serial.onData o socket.on:
serial.on('data', () => {
  let raw = serial.readLine();
  let data = parseSerial(raw); // {x, y, z}
  inputSubject.notify(data);
});
```
## Patrón Factory Method / Simple Factory

### Dónde está definido mi método factory?

Creé una clase `VisualFactory` con un método estático `createVisualObject`:

```javascript
class VisualFactory {
  static createVisualObject(type) {
    switch(type) {
      case 'circle':
        return new CircleVisual();
      case 'square':
        return new SquareVisual();
      default:
        return new TriangleVisual();
    }
  }
}
```

### Qué tipos de objetos creaba?

* `CircleVisual`, `SquareVisual`, `TriangleVisual`
  Cada uno tenía un método `draw()` con estilo propio.

### Por qué fue útil?

Me ayudó a centralizar la creación de figuras visuales y permitió cambiar fácilmente el tipo de figura generada según el estado o el input, sin romper el flujo principal del programa.

### Ejemplo de uso en el cliente

```javascript
function mousePressed() {
  let shape = VisualFactory.createVisualObject(currentShape);
  visuals.push(shape);
}
```

## Patrón State

### ¿Qué clase actuó como Contexto?

La clase `VisualApp` fue mi **contexto**. Guarda una referencia al estado actual:

```javascript
class VisualApp {
  constructor() {
    this.state = new IdleState(this);
  }

  setState(state) {
    this.state = state;
  }

  update() {
    this.state.update();
  }
}
```

### ConcreteStates implementados?

Implementé:

#### `IdleState`

```javascript
class IdleState {
  constructor(app) {
    this.app = app;
  }

  update() {
    // Solo fondo suave, sin figuras
    background(20, 20, 40, 10);
  }
}
```

#### `DrawingState`

```javascript
class DrawingState {
  constructor(app) {
    this.app = app;
  }

  update() {
    background(0);
    for (let v of visuals) {
      v.draw();
    }
  }
}
```

### Qué desencadenaba las transiciones?

Una entrada desde el móvil cambiaba el estado:

```javascript
socket.on('mobileInputForwarded', (data) => {
  if (data.touchX < width / 2) {
    visualApp.setState(new DrawingState(visualApp));
  } else {
    visualApp.setState(new IdleState(visualApp));
  }
});
```

### Por qué usar State?

Permitió separar claramente los comportamientos del sistema según su modo, sin tener que escribir múltiples `if` en una sola clase. Habría sido más engorroso manejar esto solo con `switch/case`, perdiendo modularidad.

## Definiciones Post-Experiencia

### Qué es una clase?

Una clase es un plano o plantilla que define la forma y el comportamiento de un objeto. Contiene atributos y métodos que describen cómo debe actuar un objeto cuando se crea a partir de ella.

### ¿Qué es un objeto?

Un objeto es una instancia de una clase. Tiene valores concretos y puede ejecutar los métodos definidos en la clase. Es como un “ser vivo” creado a partir del plano.

## Beneficios estructurales

El uso de los patrones **Observer**, **Factory** y **State** ayudó muchísimo a estructurar mi código:

* **Observer** permitió una comunicación desacoplada entre sensores e interfaces.
* **Factory** hizo más flexible la creación de objetos visuales, permitiendo agregar nuevos tipos fácilmente.
* **State** organizó claramente los distintos comportamientos del sistema según su modo actual.

Con esto, mi código fue más limpio, fácil de modificar y escalar. Por ejemplo, pude agregar un nuevo estado `PausedState` sin tocar casi nada del resto del programa.

