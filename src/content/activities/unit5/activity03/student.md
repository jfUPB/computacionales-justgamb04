## Código fuente completo del caso de estudio modificado

Se realizaron las siguientes modificaciones al caso de estudio original:

### Nuevos tipos de partículas:

Se agregaron dos nuevas clases que heredan de `Particle`:

#### **HorizontalParticle** (se desplaza en línea recta horizontal):

```cpp
class HorizontalParticle : public Particle {
public:
    HorizontalParticle(ofVec2f position) {
        this->position = position;
        velocity = ofVec2f(ofRandom(1, 3), 0);
    }

    void update(float dt) override {
        position += velocity * dt;
    }

    void draw() override {
        ofSetColor(0, 255, 0);
        ofDrawCircle(position, 3);
    }
};
```

#### **SpiralParticle** (se mueve en espiral):

```cpp
class SpiralParticle : public Particle {
private:
    float angle;
    float radius;

public:
    SpiralParticle(ofVec2f position) {
        this->position = position;
        angle = 0;
        radius = 0;
    }

    void update(float dt) override {
        angle += dt * 3;
        radius += dt * 20;
        position.x += cos(angle) * radius * dt;
        position.y += sin(angle) * radius * dt;
    }

    void draw() override {
        ofSetColor(255, 0, 255);
        ofDrawCircle(position, 4);
    }
};
```

### Nuevo modo de explosión:

Se implementó una nueva clase que hereda de `ExplosionParticle` llamada `MultiPatternExplosion`, la cual genera partículas de todos los tipos disponibles:

```cpp
class MultiPatternExplosion : public ExplosionParticle {
public:
    MultiPatternExplosion(ofVec2f position) {
        this->position = position;
        for (int i = 0; i < 5; i++) {
            subParticles.push_back(new RisingParticle(position));
            subParticles.push_back(new HorizontalParticle(position));
            subParticles.push_back(new SpiralParticle(position));
        }
    }

    void update(float dt) override {
        for (auto& p : subParticles) {
            p->update(dt);
        }
    }

    void draw() override {
        for (auto& p : subParticles) {
            p->draw();
        }
    }

    ~MultiPatternExplosion() {
        for (auto& p : subParticles) {
            delete p;
        }
        subParticles.clear();
    }

private:
    std::vector<Particle*> subParticles;
};
```

### Cambios en `ofApp` para usar las nuevas partículas

En `mousePressed`, se agregó la posibilidad de crear una `MultiPatternExplosion` al hacer clic con el botón derecho:

```cpp
void ofApp::mousePressed(int x, int y, int button) {
    if (button == 0) {
        particles.push_back(new CircularExplosion(ofVec2f(x, y)));
    } else if (button == 2) {
        particles.push_back(new MultiPatternExplosion(ofVec2f(x, y)));
    }
}
```

## Lista de pruebas realizadas

### Prueba 1: Movimiento horizontal

* **Qué intenté probar:** El comportamiento de `HorizontalParticle`.
* **Qué esperaba obtener:** Que la partícula se moviera en línea recta horizontalmente.
* **Qué resultado obtuve:** Movimiento correcto hacia la derecha.
* **Resultado:** Correcto, no fue necesario corregir.

### Prueba 2: Movimiento en espiral

* **Qué intenté probar:** El comportamiento de `SpiralParticle`.
* **Qué esperaba obtener:** Movimiento espiral creciente.
* **Qué resultado obtuve:** Movimiento correcto, la partícula describe una espiral expandida.
* **Resultado:** Correcto, no fue necesario corregir.

### Prueba 3: Creación de múltiples tipos de partículas en una sola explosión

* **Qué intenté probar:** El comportamiento de `MultiPatternExplosion`.
* **Qué esperaba obtener:** Generación de partículas Rising, Horizontal y Spiral en una misma explosión.
* **Qué resultado obtuve:** Todos los tipos de partículas fueron generadas y se movieron según lo esperado.
* **Resultado:** Correcto.

### Prueba 4: Verificación de herencia y composición en depurador

* **Qué intenté probar:** Jerarquía y ocupación en memoria de `MultiPatternExplosion`.
* **Qué esperaba obtener:** Que cada subobjeto tuviera estructura independiente y estuviera correctamente instanciado.
* **Qué resultado obtuve:** Estructuras correctamente enlazadas en memoria.
* **Resultado:** Correcto.

### Prueba 5: Comportamiento del método `update` polimórfico

* **Qué intenté probar:** El polimorfismo en tiempo de ejecución mediante la llamada a `update` sobre `particles`.
* **Qué esperaba obtener:** Que el método `update()` se ejecutara según el tipo dinámico de partícula.
* **Qué resultado obtuve:** Cada partícula ejecutó su propio `update`.
* **Resultado:** Correcto.
