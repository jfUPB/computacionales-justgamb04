#### El viaje de un vértice

Imaginemos que tengo un vértice en el array `vertices[]` de C++ con una posición `(0.0f, 0.5f, 0.0f)`. Este dato comienza su viaje en la **CPU**, donde vive en la memoria RAM del sistema. Luego, lo envío a la **GPU** usando un **Vertex Buffer Object (VBO)**, que es básicamente un bloque de memoria en la GPU donde se almacenan los datos de los vértices.

Después, creo un **Vertex Array Object (VAO)** que guarda la configuración de cómo se deben interpretar los datos del VBO (por ejemplo, cuántos floats por vértice, si son posiciones o colores, etc.).

Cuando se llama a `glDrawArrays`, el vértice pasa al **Vertex Shader**, que es el primer shader que se ejecuta en la GPU. Aquí puedo transformar la posición del vértice, como aplicarle una matriz de transformación si quiero moverlo o escalarlo. Luego de pasar por todos los vértices, el sistema hace la **Rasterización**, que convierte estos vértices en fragmentos (candidatos a píxeles).

Cada uno de esos fragmentos entra al **Fragment Shader**, donde decido el color final de cada píxel en la pantalla. Finalmente, el resultado se guarda en el **Framebuffer**, que es lo que se muestra visualmente en mi ventana.

#### La orquesta gráfica

En este sistema, siento que **el código C++** (y más específicamente el loop principal del programa) es quien **dirige la orquesta**. Se encarga de inicializar todo, de hacer los llamados clave y de pasar la información entre los componentes.

Los **músicos especializados** serían:

* **GLFW**: se encarga de abrir la ventana y capturar inputs (como teclado y mouse).
* **GLAD**: carga las funciones de OpenGL, sin él no podríamos usar las llamadas de OpenGL moderno.
* **VBO/VAO**: manejan la organización y transferencia de datos de vértices.
* **Shaders GLSL**: hacen el trabajo visual específico, como transformar vértices o decidir colores.

Todos estos componentes se comunican principalmente a través de llamadas desde el C++, pasando datos a la GPU con funciones como `glUniform`, `glVertexAttribPointer`, etc.

#### Shaders

Los **shaders** son clave en OpenGL moderno porque nos dan **control total** sobre cómo se procesan los gráficos. Antes, en el pipeline fijo, solo podíamos usar lo que OpenGL ofrecía por defecto. Ahora, podemos escribir nuestro propio código para determinar desde la posición exacta de un vértice hasta su color final con lógicas dinámicas.

El **Vertex Shader** se encarga de transformar los vértices (posición, por lo general) y decidir su ubicación en la pantalla.
El **Fragment Shader**, en cambio, se encarga de determinar el color de cada fragmento que formará parte de un píxel en la pantalla.

#### De la CPU a la GPU

Necesitamos mecanismos como **VBOs** y **uniforms** porque la GPU trabaja de forma paralela y masiva, y no puede simplemente “pedirle” datos a la CPU cuando los necesita. Tenemos que **preparar y enviar todo de antemano**.

* Los **atributos** (como posiciones, colores, normales) son datos por vértice, enviados una vez por cada vértice a través del VBO.
* Los **uniforms** son datos que son iguales para todos los fragmentos o vértices durante un draw call (como el tiempo o una matriz de transformación). Se actualizan con `glUniform` desde el código C++.

#### El concepto clave

Para mí, el concepto más importante de esta unidad es **el uso de shaders**. Entender que todo lo que vemos en pantalla pasa por código personalizado que nosotros escribimos fue una revelación. Saber que podemos controlar cómo se comportan vértices y píxeles a ese nivel me hizo entender el poder real que tenemos como programadores gráficos.


#### Mayor desafío

Lo más difícil fue al principio entender cómo se conecta todo. Me costó entender qué hace exactamente cada objeto (VBO, VAO, shader, etc.) y por qué el orden en que se hacen las llamadas importa tanto.

Lo que me ayudó fue hacer diagramas visuales, revisar ejemplos paso a paso y, sobre todo, **modificar el código y ver qué pasaba**. A veces un simple error, como no bindear bien un VAO, hacía que no se viera nada y eso me frustraba. Pero poco a poco fui entendiendo la lógica detrás.

#### Conclusión

Esta unidad fue una muy buena introducción al pipeline gráfico moderno. Me quedo con una mejor comprensión de cómo la CPU y la GPU se comunican, y del rol fundamental de los shaders. Aunque aún me falta mucho por explorar, ahora tengo una base clara para seguir aprendiendo.
