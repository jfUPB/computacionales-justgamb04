### **Concepto del Patrón State**

El **Patrón State** permite a un objeto alterar su comportamiento cuando su estado interno cambia, haciendo que el objeto parezca cambiar de clase. Este patrón es útil cuando un objeto debe comportarse de manera diferente dependiendo de su estado interno. En lugar de usar múltiples bloques `if/else` o `switch` para manejar diferentes comportamientos, el patrón encapsula cada comportamiento en una clase separada y permite que el objeto delegue la ejecución a su objeto de estado actual.

### **Componentes Clave**

1. **Context (Contexto)**: Es el objeto que mantiene una referencia al estado actual y delega las solicitudes de operación al estado correspondiente.
2. **State (Estado)**: Define una interfaz común para todos los estados concretos. Este interfaz declara los métodos que representan las operaciones dependientes del estado.
3. **ConcreteState (Estado Concreto)**: Cada subclase implementa un comportamiento asociado con un estado del contexto. Cada estado concreto encapsula un comportamiento específico (por ejemplo, NormalState, AttractState, RepelState, StopState).

### **Análisis del Caso de Estudio**

#### **Identificación de los Componentes**

* **Context (Contexto)**: En este caso, el contexto es la clase `Particle`, que mantiene el estado actual de la partícula.
* **State (Estado)**: La interfaz común para los estados es la clase abstracta `State`, que tiene métodos como `update`, `onEnter` y `onExit`.
* **ConcreteState (Estado Concreto)**: Las clases `NormalState`, `AttractState`, `RepelState` y `StopState` son las implementaciones concretas de los estados que encapsulan los diferentes comportamientos de las partículas.

#### **Delegación del Comportamiento**

* El método `Particle::update()` delega el comportamiento a la clase de estado actual. Dependiendo del estado actual de la partícula, se llamará al método `update()` correspondiente del estado.
* Las clases concretas, como `NormalState::update()`, `AttractState::update()`, `RepelState::update()` y `StopState::update()`, encapsulan comportamientos diferentes. Cada una de estas clases implementa su propia lógica de actualización, lo que hace que el comportamiento de la partícula cambie según el estado en el que se encuentre.

#### **Transiciones de Estado**

* Una partícula cambia de estado utilizando el método `setState()`, que se encarga de gestionar la transición entre estados.
* Dentro de `Particle::setState()`, se realiza el cambio de estado, y los métodos `onEnter` y `onExit` se utilizan para gestionar la entrada y salida de un estado. Esto puede incluir inicialización o limpieza de recursos asociados con un estado.
* Un evento externo, como la presión de una tecla, desencadena el cambio de estado de la partícula.

### **Diagrama de Estados de la Clase Particle**

A continuación, un **diagrama de estados** simplificado para la clase `Particle`:

```
+------------------+    'n'    +-----------------+
|   NormalState    | ---------> |  AttractState  |
+------------------+           +-----------------+
         ^                           |
         | 'r'                       | 'a'
         |                           v
+------------------+    's'    +-----------------+
|  RepelState      | <-------- |   StopState     |
+------------------+           +-----------------+
```

* **Transiciones de Estado:**

  * De `NormalState` a `AttractState` con la tecla 'n'.
  * De `AttractState` a `RepelState` con la tecla 'r'.
  * De `RepelState` a `StopState` con la tecla 's'.
  * De `StopState` a `NormalState` con la tecla 'n'.

### **Ventajas de Usar el Patrón State**

El **Patrón State** mejora la cohesión, ya que cada clase concreta encapsula un comportamiento específico, reduciendo la necesidad de tener grandes bloques de código condicional dentro de la clase `Particle::update()`.

#### **Ventajas:**

1. **Cohesión**: Cada estado es manejado por su propia clase, lo que mejora la organización y claridad del código.
2. **Extensibilidad**: Si se desea agregar un nuevo estado, como un "pausedState", se puede hacer fácilmente sin modificar el código existente.
3. **Principio Abierto/Cerrado (Open/Closed Principle)**: La clase `Particle` está abierta para la extensión (agregar nuevos estados) pero cerrada para la modificación (no se necesita modificar el código existente).

#### **Alternativa con `if/else` o `switch`:**

Si no se utilizara el patrón State, el comportamiento de la partícula dependería de un miembro como `std::string estadoActual`, y un bloque grande de `if/else` o `switch` dentro de `Particle::update()` manejaría el comportamiento. Esto resultaría en un código menos organizado, más difícil de mantener y extender.

### **Métodos `onEnter` y `onExit`**

Los métodos `onEnter` y `onExit` permiten manejar tareas adicionales al entrar o salir de un estado. Por ejemplo, si una partícula cambia a `AttractState`, el método `onEnter` podría inicializar variables o cambiar propiedades de la partícula. De manera similar, `onExit` podría limpiar recursos o restablecer valores al salir de un estado.

#### Ejemplo de Uso de `onEnter`/`onExit`:

* **`onEnter` para `AttractState`**: Podría activar una animación o cambiar el color de la partícula para reflejar el cambio a un estado de atracción.
* **`onExit` para `StopState`**: Podría detener cualquier animación y poner la partícula en un estado inactivo.

### **Reflexión sobre el Patrón State**

El patrón **State** es útil cuando un objeto tiene varios comportamientos que dependen de su estado, y cada estado tiene su propio conjunto de reglas. Ayuda a evitar bloques de código complejos y hace que el código sea más modular y fácil de mantener.
