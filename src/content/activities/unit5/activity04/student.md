## 1. ¿En la actividad anterior dónde estás aplicando el concepto de **encapsulamiento**? ¿Por qué? Muestra en qué parte del código.

El encapsulamiento se aplica al definir atributos como `position`, `velocity`, `angle`, y `radius` como `private` o `protected` dentro de las clases `Particle`, `SpiralParticle`, `HorizontalParticle`, etc. Esto impide que otras partes del programa accedan directamente a estos datos y obliga a interactuar con ellos mediante los métodos públicos (`update`, `draw`), controlando así cómo se accede o modifica la información interna de cada objeto.

Ejemplo:

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

    void update(float dt) override { ... }
    void draw() override { ... }
};
```

Aquí se encapsulan `angle` y `radius` dentro de `SpiralParticle`.

## 2. ¿En la actividad anterior dónde estás aplicando el concepto de **herencia**? ¿Por qué? Muestra en qué parte del código.

La herencia se aplica cuando clases como `RisingParticle`, `HorizontalParticle`, y `SpiralParticle` heredan de la clase base `Particle`. Esto permite que compartan métodos y estructura básica (como `position`, `update`, `draw`) y sobreescriban los métodos según su comportamiento específico.

Ejemplo:

```cpp
class HorizontalParticle : public Particle {
public:
    HorizontalParticle(ofVec2f position) { ... }
    void update(float dt) override { ... }
    void draw() override { ... }
};
```

Aquí, `HorizontalParticle` hereda de `Particle`, reutilizando la estructura y modificando su comportamiento.

## 3. ¿En la actividad anterior dónde estás aplicando el concepto de **polimorfismo**? ¿Por qué? Muestra en qué parte del código.

El polimorfismo se implementa al declarar métodos virtuales (`update` y `draw`) en la clase base `Particle` y sobreescribirlos en las clases hijas. Luego se utiliza al guardar distintos tipos de partículas en un mismo vector de punteros a `Particle`, permitiendo que cada una ejecute su propia versión de los métodos.

Implementación del polimorfismo:

```cpp
class Particle {
public:
    virtual void update(float dt) = 0;
    virtual void draw() = 0;
    virtual ~Particle() {}
};
```

Uso del polimorfismo (en `ofApp::update()` y `ofApp::draw()`):

```cpp
for (auto& p : particles) {
    p->update(ofGetLastFrameTime());
    p->draw();
}
```

En este fragmento se están llamando métodos polimórficos sobre punteros a `Particle`.

## 4. Luego de esta experiencia de aprendizaje, define con tus propias palabras:

### ¿Qué es un objeto?

Un objeto es una instancia concreta de una clase. Es una entidad que tiene estado (atributos) y comportamiento (métodos), y representa un elemento del mundo real o lógico dentro del programa.

### ¿Qué es una clase?

Una clase es un molde o plantilla que define qué atributos y métodos tendrá un objeto. Es una abstracción que permite construir múltiples objetos con las mismas características y comportamientos.

## 5. ¿Cómo se ve en memoria un objeto de una clase que hereda de otra clase?

Un objeto de una clase derivada contiene en memoria primero los atributos heredados de la clase base y luego los atributos propios de la clase hija. Además, si la clase tiene métodos virtuales, contiene una tabla de punteros virtuales (vtable) para garantizar el comportamiento polimórfico. En resumen, en memoria se reserva un bloque continuo donde se combinan las estructuras de ambas clases (base e hija).

Por ejemplo, un `SpiralParticle` tendrá en memoria:

* Los atributos heredados de `Particle` como `position`.
* Sus propios atributos como `angle` y `radius`.
* Un puntero a la vtable si hay métodos virtuales.
