**Captura de pantalla del ejemplo funcionando:**
![image](https://github.com/user-attachments/assets/62389572-f1cc-4ea5-85da-c23a96a0ce15)

**Observaciones iniciales:**
El proyecto se abre correctamente en Visual Studio, y tras compilarlo, se muestra una ventana con un triángulo en el centro. Al revisar el código, se identifican varias funciones desconocidas relacionadas con OpenGL moderno y conceptos nuevos como VAO, VBO y shaders. Aunque aún no comprendo del todo el funcionamiento de cada parte, ya empiezo a identificar cómo se organiza la estructura básica de un programa gráfico.

**Preguntas que me surgen al observar el código:**

1. ¿Qué significa exactamente `glGenVertexArrays`, `glGenBuffers` y por qué hay que usarlos para dibujar un triángulo tan simple?
2. ¿Cómo se construye y enlaza un shader en OpenGL? ¿Por qué hay que escribir código separado para el vértice (`vertex shader`) y el fragmento (`fragment shader`)?
3. ¿Cuál es la función de `glfw` y `glad` dentro del programa? ¿Podría escribir un programa similar sin ellos?

### Respuestas a las preguntas planteadas:

**1. ¿Qué significa exactamente `glGenVertexArrays`, `glGenBuffers` y por qué hay que usarlos para dibujar un triángulo tan simple?**
Estas funciones de OpenGL permiten trabajar con la memoria de la GPU.

* `glGenVertexArrays` crea un VAO (Vertex Array Object) que guarda configuraciones sobre cómo se usan los vértices.
* `glGenBuffers` crea un VBO (Vertex Buffer Object) que almacena directamente los datos de los vértices.
  Esto puede parecer complejo para un triángulo, pero es necesario en OpenGL moderno para aprovechar el procesamiento en paralelo y preparar el código para proyectos más grandes.

**2. ¿Cómo se construye y enlaza un shader en OpenGL? ¿Por qué hay que escribir código separado para el vértice y el fragmento?**
Los shaders son programas escritos en GLSL que se ejecutan en la GPU.

* El **vertex shader** transforma cada vértice individual (posición, color, etc.).
* El **fragment shader** decide el color de cada píxel que se va a dibujar.
  Ambos se escriben, compilan y luego se enlazan en un programa usando funciones como `glAttachShader` y `glLinkProgram`. Se separan porque cada uno cumple un rol distinto en la renderización.

**3. ¿Cuál es la función de `glfw` y `glad` dentro del programa? ¿Podría escribir un programa similar sin ellos?**

* **GLFW** se encarga de crear la ventana y gestionar eventos como el teclado y mouse.
* **GLAD** permite acceder a las funciones modernas de OpenGL, ya que estas no están disponibles directamente en todos los sistemas.
  Se podría hacer sin estas librerías, pero requeriría trabajar directamente con APIs como Win32 o X11, lo cual es muy complejo. Usar GLFW y GLAD facilita el trabajo y hace el programa más portable.

