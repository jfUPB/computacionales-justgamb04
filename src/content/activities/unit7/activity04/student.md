Para la **diferencia entre una CPU y una GPU**, la CPU (Unidad Central de Procesamiento) es un procesador general diseñado para manejar una variedad de tareas de cómputo, mientras que la GPU (Unidad de Procesamiento Gráfico) está especializada en realizar operaciones matemáticas altamente paralelizadas, como las necesarias para el procesamiento de gráficos y la manipulación de imágenes. La CPU maneja las instrucciones del sistema operativo y las aplicaciones, ejecutando secuencias de tareas en serie. En contraste, la GPU está optimizada para manejar muchas tareas en paralelo, lo que la hace más eficiente para procesar gráficos, aunque también se usa en otras áreas como la inteligencia artificial y el aprendizaje automático.

**Gráficas en un computador**: En los computadores, las gráficas son gestionadas por una tarjeta gráfica, que está equipada con una GPU. Los datos gráficos, como los vértices de un modelo 3D, son procesados por la GPU a través del pipeline gráfico. El pipeline toma estos datos y los transforma en una imagen que se muestra en el monitor. Para esto, OpenGL o DirectX son las API que permiten comunicarse con la GPU, procesando los datos de los vértices, shaders, y realizando tareas como rasterización, iluminación, y texturización.

**El pipeline de OpenGL** está compuesto por tres pasos clave:

1. **Procesamiento de vértices**: En este paso, los vértices de los objetos son transformados, y se les asignan atributos como la posición, el color, y las coordenadas de textura. El *vertex shader* es responsable de transformar los vértices.

2. **Rasterización**: En esta etapa, los vértices transformados se convierten en fragmentos que corresponden a posibles píxeles en la pantalla. Aquí es donde se determinan las posiciones finales de los puntos de los objetos.

3. **Procesamiento de fragmentos**: Los fragmentos son luego procesados, generalmente por el *fragment shader*, que puede realizar tareas como asignar un color final a cada fragmento, o aplicar efectos de iluminación o texturas.

El **pipeline programable** en OpenGL es una característica importante porque permite a los programadores escribir y controlar los shaders, tanto de vértices como de fragmentos, mientras que el pipeline fijo predefinía ciertos pasos de la ejecución. Esto otorga más flexibilidad y control a la hora de programar gráficos complejos.

**Rasterización**: Es el proceso de convertir objetos 3D en una imagen 2D, o de convertir primitivas gráficas (como triángulos) en píxeles o fragmentos en la pantalla. Esto implica interpolar los atributos de los vértices (como color y textura) a lo largo de las superficies que representan los objetos.

**Fragmentos y píxeles**: Un fragmento es una unidad de procesamiento que contiene información sobre un píxel potencial, pero aún no ha sido decidido si será visible en la pantalla (esto se determina en la etapa de la prueba de profundidad). No es lo mismo que un píxel, ya que un fragmento puede representar varios píxeles, dependiendo del contexto y del cálculo de visibilidad (depth test).

**Z-buffer y Depth test**: El Z-buffer es una técnica utilizada para gestionar la visibilidad de los objetos en una escena 3D, manteniendo la información de profundidad (distancia de la cámara) para cada píxel. El *depth test* compara la profundidad de un fragmento con el valor almacenado en el Z-buffer para decidir si el fragmento debe ser visible.

**Aliasing y Anti-aliasing**: El aliasing ocurre cuando las imágenes contienen artefactos visuales como bordes dentados debido a la resolución limitada de la pantalla. El anti-aliasing es una técnica que suaviza esos bordes para hacer la imagen más suave y realista.

**Iluminación y fragment shader**: Los fragment shaders suelen ser responsables de la iluminación, ya que determinan cómo se iluminan los fragmentos con base en las fuentes de luz y las propiedades del material. Es posible tener un fragment shader sin iluminación, pero generalmente se usa para efectos de color o textura. Si se usan múltiples fuentes de iluminación, cada fuente debe ser procesada en el fragment shader, lo que incrementa la carga de trabajo en la GPU.

### Relación con el código del ejemplo del triángulo:

En el ejemplo del triángulo simple, los vértices son enviados a la GPU y se almacenan en un VBO. Estos vértices son luego procesados por el vertex shader, que los transforma según las coordenadas definidas, y luego se dibujan en pantalla con un fragment shader que define el color del triángulo. Los shaders son programas que se ejecutan en la GPU para procesar vértices y fragmentos, y su propósito es manipular estos datos para crear la imagen final que vemos.

El código de la función `setupTriangle()` se encarga de configurar los buffers de vértices (VBO) y los objetos necesarios para almacenar la información de los vértices, mientras que `buildShaderProgram()` compila y vincula los shaders. Los shaders en OpenGL moderno son cruciales para realizar el procesamiento gráfico en la GPU de forma eficiente.

