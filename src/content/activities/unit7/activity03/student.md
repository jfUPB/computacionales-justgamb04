##  Primera Digestión: Análisis general y experimento con el viewport

### Lo que aprendí hasta ahora

Durante el análisis de la función `main()` del programa triangle.cpp, aprendí que:

* OpenGL necesita un contexto para trabajar, y este es creado y asociado a una ventana usando GLFW.
* GLFW es la biblioteca que se encarga de manejar eventos (teclado, mouse, tamaño de ventana) y de crear ventanas multiplataforma con contexto OpenGL.
* El framebuffer es la zona de memoria donde OpenGL “pinta” los pixeles antes de que se muestren en la pantalla.
* El viewport define qué parte del framebuffer se utiliza para mostrar en pantalla.
* GLAD carga las funciones de OpenGL que el sistema operativo no provee directamente.
* La GPU es quien realmente dibuja, pero OpenGL es el intermediario entre el programador y la GPU.

### Experimento con el viewport

Modifiqué esta línea:

```cpp
glViewport(0, 0, bufferWidth, bufferHeight);
```

Por esta:

```cpp
glViewport(0, bufferHeight / 2, bufferWidth / 2, bufferHeight / 2);
```

#### Observaciones:

* El triángulo se dibujó solo en la mitad inferior izquierda de la ventana.
* Cambiar el viewport es como decirle a OpenGL: “dibuja aquí, y no en toda la hoja”.
* Si divido el tamaño por 4, el triángulo aparece aún más pequeño y en una esquina.
* Si multiplico por 2, parte del triángulo queda fuera del área visible.

Esto demuestra cómo el viewport controla la porción del framebuffer donde OpenGL renderiza.

## Game loop explicado

Este bloque es el corazón del programa: el ciclo que se repite constantemente para dibujar en la ventana. Desglose:

* `glfwPollEvents();` ⇒ Revisa si se presionó alguna tecla o se cambió el tamaño.
* `processInput(mainWindow);` ⇒ En este caso, solo permite cerrar con ESC.
* `glClearColor(...)` y `glClear(...)` ⇒ Limpian la pantalla con un color de fondo (aquí, verde oscuro).
* `glUseProgram(shaderProg);` ⇒ Usa los shaders que compilé antes.
* `glBindVertexArray(VAO);` y `glDrawArrays(...)` ⇒ Dibuja el triángulo usando los datos cargados en la GPU.
* `glfwSwapBuffers(...)` ⇒ Cambia el buffer invisible con el visible (doble buffering) para evitar parpadeos.

## Respondiendo preguntas clave

### ¿Qué es el contexto OpenGL?

Es el entorno interno que contiene toda la información y recursos que OpenGL usa para renderizar. Es como el “taller” donde trabaja el artista (la GPU), y sin él no se puede hacer nada gráfico. GLFW se encarga de crearlo y asociarlo a la ventana.

### ¿Cuál es el rol de GLFW?

Crear la ventana y el contexto, gestionar eventos (teclado, mouse), abstraer las diferencias entre sistemas operativos. La ventaja: escribo el código una sola vez y funciona igual en Windows, Mac o Linux.

### ¿Por qué OpenGL necesita un contexto?

Porque sus funciones no son globales: necesitan saber sobre qué “espacio de trabajo” van a operar (shaders, buffers, texturas, etc.). Sin contexto, no hay dibujo.

### ¿Qué es el framebuffer?

Es la memoria donde se dibuja cada cuadro antes de mostrarse. Me recuerda a los pixeles de las imágenes o pantallas en las primeras unidades: cada cuadro es una imagen.

### ¿Qué relación hay entre el viewport y el framebuffer?

El viewport define qué porción del framebuffer se usa para mostrar en pantalla. Si el framebuffer es una hoja, el viewport es la ventana por la cual se ve esa hoja.

### ¿Qué rol juegan los drivers de GPU y la GPU?

Los drivers traducen las instrucciones de OpenGL en comandos que la GPU entiende. La GPU ejecuta esos comandos y dibuja millones de pixeles por segundo. OpenGL es el lenguaje intermedio.

### ¿Por qué activar el VSync?

Para sincronizar la velocidad de dibujo con la tasa de refresco del monitor y evitar “tearing” (cortes visuales). Si no lo activo y el contenido es dinámico, la imagen puede verse desfasada.

### ¿Qué es OpenGL Legacy?

La versión antigua de OpenGL donde se usaban funciones como `glBegin()` y `glEnd()`. No usaba shaders. El OpenGL moderno (Core Profile) usa shaders y da más control, pero requiere más trabajo inicial.

### ¿Qué es un shader program y por qué es importante?

Un conjunto de shaders (vertex + fragment) que define cómo se transforman los vértices y cómo se colorean los pixeles. Es esencial en OpenGL moderno porque sin él, no hay renderizado.

### ¿Qué hace `setupTriangle()`?

Crea el VAO y el VBO, y carga en la GPU los vértices del triángulo. El VAO guarda la configuración de atributos y el VBO guarda los datos (posiciones). Es la “carga inicial” del triángulo.

### ¿Hay que volver a usar `glUseProgram()` y `glBindVertexArray()` en cada loop?

Sí, si queremos asegurarnos de que están activos antes de dibujar. Aunque no cambien, es buena práctica activarlos cada vez por claridad. También permite cambiar de objeto o shader en otros frames si es necesario.

### ¿Por qué `glfwSwapBuffers()` es importante?

Porque muestra en pantalla lo que OpenGL acaba de dibujar. Si no lo llamo, la imagen no se actualiza. Me pasó: cuando comenté esta línea, la ventana se abría pero quedaba en negro.

Conclusión

Esta actividad me ayudó a entender la estructura mínima de un programa OpenGL moderno. Aprendí que todo se basa en configurar correctamente el contexto, los shaders, los buffers y en mantener un ciclo de dibujo constante. También descubrí lo poderoso (y detallado) que puede ser el control gráfico con OpenGL Core Profile.
