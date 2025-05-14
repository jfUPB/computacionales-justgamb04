### Observación general del comportamiento

Al ejecutar la aplicación, en pantalla se visualizan múltiples partículas que se mueven en diferentes direcciones. Algunas son pequeñas y blancas, otras más grandes y de colores como verde o azul, lo cual sugiere que hay distintos tipos de partículas. Estas partículas parecen tener comportamientos distintos desde el inicio.

### Interacción con la aplicación

Se puede interactuar con la aplicación usando el teclado:

* `a`: Las partículas comienzan a **atraerse hacia el cursor del mouse**.
* `r`: Las partículas **huyen del cursor del mouse**.
* `s`: Las partículas se **detienen completamente**.
* `n`: Las partículas **retoman su comportamiento normal**, moviéndose aleatoriamente.

Este cambio de comportamiento es instantáneo al presionar cada tecla.

### Diferentes tipos de partículas

Sí, hay al menos tres tipos distintos de partículas:

* **"star"**: Pequeñas y blancas, se comportan de manera estándar.
* **"shooting\_star"**: Verdes y rápidas, con velocidad inicial aumentada.
* **"planet"**: Azules y más grandes, con movimiento más sutil.

Estos tipos son definidos al crearse en el `ParticleFactory`.

### Hipótesis de funcionamiento interno

Cada vez que se presiona una tecla, se genera un evento (por ejemplo, `"attract"`) que es **notificado a todas las partículas**. Al recibir este evento, cada partícula **cambia su estado interno** (State) que modifica la lógica de su `update()`:

* `AttractState`: calcula un vector hacia el mouse y ajusta la velocidad.
* `RepelState`: hace lo contrario.
* `StopState`: pone la velocidad en cero.
* `NormalState`: vuelve al movimiento aleatorio.

Esto implementa claramente el **patrón State**, y la notificación masiva utiliza el **patrón Observer**.

### Complemento visual

#### Diagrama de clases simplificado

```
            +----------------+
            |   Subject      |
            +----------------+
            | +addObserver() |
            | +notify()      |
            +----------------+
                    |
        +-----------+-------------+
        |                         |
+---------------+         +----------------+
|   ofApp       |         |   Observer     |
+---------------+         +----------------+
| +keyPressed() |<--------| +onNotify()    |
| +setup()      |         +----------------+
| +update()     |
| +draw()       |
+---------------+
        |
        | observes
        v
+---------------+
|  Particle      |
+----------------+
| position       |
| velocity       |
| size, color    |
| +update()      |
| +draw()        |
| +setState()    |
+----------------+
        |
        | uses
        v
+---------------+
|     State     |<-------------+
+---------------+              |
| +update()     |              |
| +onEnter()    |              |
+---------------+              |
        ^                      |
   +----+----+     +-----------+-----------+-----------+
   |         |     |           |           |           |
+-----------+ +--------------+ +---------+ +---------+ |
| NormalState| |AttractState| |RepelState| |StopState| |
+-----------+ +--------------+ +---------+ +---------+ |
                                                |
                                         +---------------+
                                         | ParticleFactory|
                                         +---------------+
                                         | +createParticle|
                                         +---------------+
```

#### Diagrama de flujo del evento (input → cambio en partículas)

```
Usuario presiona tecla (a/r/s/n)
            |
            v
     ofApp recibe input
            |
            v
   ofApp.notify("evento")  ← Evento: "attract", "repel", etc.
            |
            v
 Partículas reciben evento (onNotify)
            |
            v
  Cada partícula cambia su estado actual
            |
            v
 En update(), cada partícula llama a su nuevo estado:
    - AttractState: se acerca al mouse
    - RepelState: se aleja del mouse
    - StopState: se detiene
    - NormalState: se mueve aleatoriamente
```

### Conclusión

Esta actividad permite comprender de forma clara cómo los patrones Observer, Factory y State pueden combinarse para diseñar sistemas complejos y flexibles. Al observar el comportamiento de las partículas y su reacción ante distintos eventos, se evidencia cómo estos patrones estructuran la lógica de forma modular y mantenible.
