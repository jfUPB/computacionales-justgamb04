### Propósito del patrón Observer

El **patrón Observer** resuelve el problema de mantener actualizados a varios objetos (observadores) cuando el estado de otro objeto (el sujeto) cambia, sin que estén fuertemente acoplados entre sí. Es decir, el Sujeto **no necesita saber qué objetos están escuchando ni cómo responderán**, simplemente les avisa.

Este patrón es ideal cuando múltiples objetos dependen del estado de otro y se quiere una **arquitectura flexible y desacoplada**.

Ejemplo cotidiano: una tienda online que te notifica cuando un producto vuelve a estar disponible, en lugar de que tengas que revisar constantemente.

### Identificación de roles en el caso de estudio

#### ¿Qué clase actúa como la interfaz **Observer**?

* `Observer` (posiblemente una clase abstracta o una interfaz definida en el código base).
* Método clave: `onNotify(std::string event)`.

#### ¿Qué clase actúa como el **Subject**?

* `Subject` (clase base o plantilla).
* Métodos:

  * `addObserver(Observer* o)`
  * `removeObserver(Observer* o)`
  * `notify(std::string event)`

#### ¿Qué clase es el **ConcreteSubject**?

* `ofApp` (la clase principal del ciclo de vida de la aplicación).
* Es quien recibe los eventos de teclado y decide cuándo notificar.

#### ¿Qué clase(s) actúan como **ConcreteObserver**?

* `Particle`
* Implementa `onNotify(event)` y cambia su estado (State) según el evento recibido.

### Flujo del evento: tecla ‘r’

1. El usuario presiona la tecla `'r'`.
2. `ofApp::keyPressed(int key)` es llamado.
3. Se detecta que la tecla presionada es `'r'`.
4. `notify("repel")` es llamado desde `ofApp`, que hereda de `Subject`.
5. El método `notify` recorre la lista de observadores (partículas) y les llama `onNotify("repel")`.
6. Cada instancia de `Particle` recibe el evento y llama a `setState(new RepelState())`.
7. En el siguiente `update()`, el nuevo estado de la partícula calcula un vector que la aleja del cursor del mouse.

### Registro y eliminación de observadores

#### ¿Dónde se añaden las partículas como observadores?

En `ofApp::setup()`:

```cpp
particles.push_back(p);
addObserver(p);
```

Cada partícula se registra al ser creada.

#### ¿Dónde se podrían eliminar observadores?

En `ofApp::exit()` o el destructor:

```cpp
removeObserver(p);
```

Esto es útil si se destruye una partícula (por ejemplo, por tiempo de vida o colisión). **Evita llamadas a punteros nulos** en la función `notify()`.

### Diagrama de clases simplificado

```
    +--------------+               +-----------------+
    |   Subject    |<>------------>|    Observer     |
    +--------------+   notify()    +-----------------+
    |+addObserver()|               |+onNotify(event) |
    |+notify()     |               +-----------------+
    +--------------+
         ^
         |
         |
     +-------+
     | ofApp |   ConcreteSubject
     +-------+
         |
         | creates and notifies
         v
   +-------------+
   |  Particle   |   ConcreteObserver
   +-------------+
   | +onNotify() |
   | +setState() |
   +-------------+
```

### Comparación con alternativa sin Observer

**Sin Observer:** `ofApp::update()` debería recorrer todas las partículas y verificar una variable global que indique el estado actual (por ejemplo, `currentMode = "repel"`), y luego actuar en consecuencia.

**Con Observer:**

* Cada partícula se suscribe una sola vez.
* `ofApp` solo necesita notificar, sin saber detalles de implementación.
* El sistema es **más extensible**: se pueden agregar nuevos tipos de observadores (por ejemplo, enemigos, luces, efectos) sin modificar `ofApp`.
* **Bajo acoplamiento**: el `Subject` no depende directamente de las clases que lo observan.

### Conclusión

El patrón Observer permite un diseño limpio y modular. En el caso de estudio, facilita la interacción entre el controlador principal (`ofApp`) y las partículas, sin que se acoplen directamente. Si se quisieran agregar más tipos de entidades que respondan a los eventos (por ejemplo, un sistema de sonido o efectos visuales), solo tendrían que implementar `onNotify()`, sin alterar la lógica de `ofApp`.
