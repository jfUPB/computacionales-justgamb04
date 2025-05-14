### Propósito del patrón Factory Method

El **Factory Method** es un patrón de diseño creacional que permite **delegar la creación de objetos a una clase especializada**, evitando que el código cliente tenga que saber qué clase concreta debe instanciar ni cómo configurarla. Esto hace que el código sea **más limpio, organizado, reutilizable y extensible**.

En el caso de estudio, se aplica como una **fábrica estática (Simple Factory)**: una clase `ParticleFactory` tiene un método que recibe un string con el tipo de partícula y devuelve una instancia configurada de `Particle`.

### Identificación de la Factory en el caso de estudio

#### ¿Qué clase actúa como la fábrica?

* `ParticleFactory`

#### ¿Cuál es el método factory?

* `static Particle* createParticle(std::string type, ofVec2f pos);`
* Es un **método estático**, lo cual permite usarlo sin instanciar `ParticleFactory`.

#### ¿Qué tipo de objeto devuelve?

* Devuelve un puntero a `Particle`.

### Proceso de creación

En `createParticle(type, pos)`:

1. Usa un `if` o `switch` para decidir qué configuración usar, dependiendo de `type`.
2. Crea un nuevo `Particle` con posición `pos`.
3. Ajusta sus propiedades como `color`, `radius` y `velocity` según el tipo.
4. Si el tipo no es reconocido, devuelve `nullptr` (en algunos casos).

**Datos necesarios para crear una partícula:**

* El `type` (string como `"star"`, `"planet"`, etc.)
* La posición inicial (`ofVec2f pos`)

**Mejora posible:**

* Devolver una partícula por defecto si el tipo es inválido, o imprimir una advertencia con `ofLogWarning()`.

### Uso en `ofApp::setup()`

```cpp
for (int i = 0; i < numParticles; i++) {
    Particle* p = ParticleFactory::createParticle("star", randomPos);
    particles.push_back(p);
    addObserver(p);
}
```

#### ¿Qué pasaría si no existiera la Factory?

El código sería algo así:

```cpp
Particle* p = new Particle(randomPos);
p->setColor(ofColor::yellow);
p->setRadius(2);
p->setVelocity(ofVec2f(ofRandom(-1, 1), ofRandom(-1, 1)));
particles.push_back(p);
```

Esto **duplica lógica en `ofApp`** y **viola el principio de responsabilidad única (SRP)**.

### Ventajas de usar `ParticleFactory`

* **Organización**: la lógica de creación está en un solo lugar.
* **Extensibilidad**: para agregar nuevos tipos solo se modifica la Factory, no el código cliente.
* **Legibilidad**: `createParticle("planet", pos)` es más claro que múltiples líneas de configuración.
* **Desacoplamiento**: `ofApp` no necesita saber cómo se configura cada tipo de partícula.

### Añadiendo una partícula "black\_hole"

Características:

* Tamaño: grande
* Color: negro
* Velocidad: muy lenta

#### Pasos para añadirla:

1. Ir a `ParticleFactory.cpp`
2. En `createParticle(...)`, añadir:

```cpp
else if (type == "black_hole") {
    Particle* p = new Particle(pos);
    p->setRadius(20);
    p->setColor(ofColor::black);
    p->setVelocity(ofVec2f(0.1, 0.1));
    return p;
}
```

#### ¿Hay que modificar `ofApp::setup()`?

**No**, siempre que el tipo `"black_hole"` sea pasado como parámetro a `createParticle`. El código en `ofApp` no cambia, lo que demuestra la utilidad del patrón.

### Métodos estáticos vs. de instancia

#### Ventajas de método **estático**:

* Fácil de usar sin necesidad de crear objetos (`ParticleFactory::createParticle(...)`).
* Ideal cuando no se necesita mantener estado en la factory.

#### Desventajas:

* **Menos flexible**: no puedes tener distintas "configuraciones" de la fábrica.
* **Difícil de testear/mocking** en entornos avanzados (por ejemplo, si quisieras usar una subclase especializada en testing).

#### Alternativa: método de instancia

Tener:

```cpp
class ParticleFactory {
public:
    Particle* createParticle(std::string type, ofVec2f pos);
};
```

Permite:

* Heredar la factory para distintos contextos (testing, simulaciones, niveles).
* Inyectar diferentes fábricas como dependencias.

### Conclusión

El patrón **Factory Method**, en su forma **Simple Factory estática**, ofrece **gran organización, claridad y extensibilidad** en el caso de estudio. Permite que `ofApp` se centre en el ciclo de vida de la aplicación, mientras `ParticleFactory` se encarga de crear y configurar objetos. Agregar nuevas partículas es sencillo, y el código se mantiene limpio y fácil de mantener.
