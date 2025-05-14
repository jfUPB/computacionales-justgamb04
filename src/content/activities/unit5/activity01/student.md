**Análisis y Experimentos**

### Descripción General del Código

El código implementa un sistema de partículas en el que las partículas nacen en la parte inferior de la pantalla y se desplazan hacia arriba. Cuando alcanzan una cierta altura o superan su tiempo de vida, explotan generando diferentes patrones de explosión. Estas explosiones se representan con partículas de distintos tamaños y colores, dependiendo del tipo de explosión: circular, aleatoria o en forma de estrella.

Las partículas se gestionan mediante clases base y derivadas, permitiendo una amplia flexibilidad en los efectos visuales generados. El sistema permite la interacción con el usuario a través del mouse y el teclado, generando una experiencia dinámica y visualmente atractiva.

### Interacción con la Aplicación

#### Uso del Mouse:

* Al hacer clic en cualquier parte de la pantalla, se crea una nueva partícula en la parte inferior central que asciende hacia el objetivo en la parte superior.
* Las partículas se mueven en la pantalla hasta que explotan según su vida útil o al alcanzar un umbral de altura determinado.

#### Uso del Teclado:

* **Tecla Espacio (Space)**: Crea 1000 partículas de manera automática, lo que genera una gran cantidad de explosiones simultáneas.
* **Tecla 's'**: Guarda una captura de pantalla del estado actual de la aplicación, permitiendo al usuario capturar la escena visual en cualquier momento.

### Comportamiento de las Partículas

* **RisingParticle**: Las partículas nacen en la parte inferior de la pantalla y ascienden hacia un punto de destino en la parte superior. Al alcanzar cierto nivel de altura o cuando su tiempo de vida expira, explotan.
* **ExplosionParticle**: Cuando una partícula de tipo RisingParticle explota, se generan nuevas partículas de explosión. Las explosiones pueden tomar tres formas:

  * **CircularExplosion**: Explosión en un patrón circular.
  * **RandomExplosion**: Explosión con partículas dispersas aleatoriamente.
  * **StarExplosion**: Explosión con partículas distribuidas en forma de estrella.

### Resultados Visuales

Al ejecutar la aplicación y realizar interacciones con el mouse o el teclado, se pueden observar diversos efectos visuales:

* Una partícula inicial subiendo hacia el objetivo.
* Una partícula que explota generando nuevas partículas.
* Múltiples partículas creando una explosión simultánea cuando se presiona la tecla espacio.
* Múltiples partículas que explotan en diferentes patrones.


### Reflexión y Experimentación

Este proyecto permite experimentar con efectos visuales de partículas de una manera directa. A través de la interacción con el mouse y el teclado, se pueden generar diversas combinaciones de explosiones, ajustando la cantidad de partículas y la intensidad de las explosiones. Esto ofrece una comprensión profunda sobre el comportamiento de las partículas y cómo interactúan en un sistema físico simulado.

Las diferentes clases y sus métodos permiten un control detallado sobre cada tipo de partícula y explosión, lo que abre la puerta a modificaciones y ampliaciones del sistema. Es posible ajustar la velocidad, la dirección, la vida útil y el tamaño de las partículas para obtener distintos efectos visuales.

### Conclusiones

La aplicación permite un análisis visual y práctico de cómo funcionan las partículas y sus interacciones dentro de un entorno gráfico. El sistema es flexible y facilita el aprendizaje de los conceptos relacionados con la manipulación de partículas en openFrameworks, lo que puede ser útil para proyectos que involucren simulaciones gráficas o efectos visuales complejos.
