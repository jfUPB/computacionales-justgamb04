### **Descripción del Proyecto**

**Evolución de Partículas**

La idea central del proyecto es crear una simulación interactiva donde partículas reaccionan a los cambios de estado y la interacción del usuario. Las partículas tienen diferentes comportamientos que dependen de su estado (por ejemplo, movimiento normal, atracción, repulsión o detención) y de los eventos que ocurren en el sistema.

El usuario podrá interactuar con la simulación utilizando el teclado para cambiar el estado de las partículas y con el ratón para influir en su posición y comportamiento.

### **Diseño con Patrones**

#### **Observer:**

* **Sujeto (Subject):** El **Contexto de Partículas** es el Sujeto. Este objeto se encarga de gestionar los cambios en las partículas y notificar a los observadores cuando algún evento ocurre, como cuando el usuario cambia el estado de las partículas.

* **Observadores:** Los **Comportamientos de Partículas** son los Observadores. Estos reaccionan a los cambios de estado, como la activación de una atracción o repulsión, modificando el comportamiento de las partículas.

* **Eventos Notificados:** Los eventos notificados son los cambios de estado, como presionar una tecla para alternar entre los diferentes estados (Normal, Attract, Repel, Stop).

**Código clave para Observer:**

```cpp
class ParticleSystem {
private:
    vector<Particle*> particles;
    vector<Observer*> observers;
public:
    void addObserver(Observer* observer) {
        observers.push_back(observer);
    }

    void notifyObservers() {
        for (auto& observer : observers) {
            observer->onNotify();
        }
    }

    void changeState(ParticleState* newState) {
        currentState = newState;
        notifyObservers();
    }
};

class Particle : public Observer {
public:
    void onNotify() override {
        // Cambio de comportamiento basado en el evento
        currentState->update();
    }
};
```

* **Prueba:** Utilicé `std::cout` para verificar que los observadores recibían la notificación correctamente cada vez que el estado cambiaba.

#### **Factory Method:**

* **Clase Factory:** La clase `ParticleFactory` es responsable de crear diferentes tipos de partículas (por ejemplo, partículas normales, partículas de atracción y partículas de repulsión).

* **Método Factory:** El método `createParticle()` de `ParticleFactory` decide qué tipo de partícula crear dependiendo del estado y comportamiento deseado.

**Código clave para Factory:**

```cpp
class ParticleFactory {
public:
    static Particle* createParticle(string type) {
        if (type == "Normal") {
            return new NormalParticle();
        } else if (type == "Attract") {
            return new AttractParticle();
        } else if (type == "Repel") {
            return new RepelParticle();
        }
        return nullptr;
    }
};
```

* **Prueba:** Imprimí mensajes de depuración para asegurarme de que el método `createParticle()` estaba creando las partículas correctas según el tipo solicitado.

#### **State:**

* **Contexto (Contexto):** La clase **Particle** es el contexto, ya que mantiene una referencia al estado actual y delega las actualizaciones de comportamiento a ese estado.

* **Estados (ConcreteState):** Los estados son `NormalState`, `AttractState`, `RepelState` y `StopState`. Cada uno encapsula el comportamiento correspondiente a ese estado (por ejemplo, movimiento normal, movimiento hacia el centro, movimiento en dirección contraria, etc.).

* **Transiciones:** Las transiciones entre estados se manejan con el método `setState()`.

**Código clave para State:**

```cpp
class ParticleState {
public:
    virtual void update(Particle* particle) = 0;
};

class NormalState : public ParticleState {
public:
    void update(Particle* particle) override {
        // Comportamiento normal de la partícula
    }
};

class AttractState : public ParticleState {
public:
    void update(Particle* particle) override {
        // Comportamiento de atracción de la partícula
    }
};

// Función de transición de estado
void Particle::setState(ParticleState* newState) {
    currentState->onExit();
    currentState = newState;
    currentState->onEnter();
}
```

* **Prueba:** Verifiqué que la partícula cambiaba correctamente de estado al presionar las teclas correspondientes y que el comportamiento cambiaba como se esperaba.

### **Integración de los Tres Patrones**

Los tres patrones interactúan de la siguiente manera:

1. **Observer:** Cuando el usuario presiona una tecla, el sistema **notifica** a las partículas sobre el cambio de estado.
2. **Factory Method:** Cuando se cambia el estado de las partículas, el sistema usa una fábrica para crear diferentes tipos de partículas con comportamientos únicos según el estado.
3. **State:** Las partículas tienen un estado interno que determina cómo se comportan. Cuando el estado cambia, las partículas modifican su comportamiento de acuerdo con el nuevo estado (por ejemplo, movimiento hacia el centro o repulsión).

**Flujo de información/control:**

* El usuario presiona una tecla → El `ParticleSystem` **notifica** a las partículas → Las partículas cambian su comportamiento a través del patrón **State** → Si es necesario, se **crean nuevas partículas** usando el patrón **Factory**.

### **Desafíos y Soluciones**

* **Desafío:** La integración de los tres patrones fue desafiante, especialmente al asegurarme de que las transiciones de estado fueran coherentes con las notificaciones del Observer.
* **Solución:** Implementé pruebas paso a paso, asegurándome de que cada patrón funcionara de forma independiente antes de integrarlos. Utilicé `std::cout` y logs para verificar las transiciones y las notificaciones.

### **Conclusión**

Este proyecto me permitió consolidar mis conocimientos sobre los patrones Observer, Factory Method y State. La integración de estos patrones de diseño me ayudó a organizar el código de manera modular, lo que facilitó su extensión y mantenimiento.

