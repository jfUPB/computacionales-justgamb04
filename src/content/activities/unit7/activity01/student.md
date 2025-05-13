Después de descomprimir el archivo, abrí la solución en Visual Studio y exploré la estructura general del proyecto. El archivo principal de código se encuentra en `main.cpp`, dentro de la carpeta `src`.

Compilé y ejecuté el proyecto correctamente. Al hacerlo, se abre una ventana donde se visualiza un triángulo centrado, con colores interpolados (degradado). Esto confirma que el entorno está funcionando adecuadamente. A continuación, incluyo la captura de pantalla del programa funcionando en mi máquina:

![image](https://github.com/user-attachments/assets/62389572-f1cc-4ea5-85da-c23a96a0ce15)

Al revisar el archivo `main.cpp`, observé fragmentos de código que crean y compilan shaders, generan buffers y configuran atributos de vértices. Aunque aún no entiendo todo lo que ocurre, identifiqué varias cosas que me causan curiosidad y que me gustaría investigar más adelante:

1. ¿Qué significa exactamente `glGenVertexArrays`, `glGenBuffers` y por qué hay que usarlos para dibujar un triángulo tan simple?
2. ¿Cómo se construye y enlaza un shader en OpenGL? ¿Por qué hay que escribir código separado para el vértice (`vertex shader`) y el fragmento (`fragment shader`)?
3. ¿Cuál es la función de `glfw` y `glad` dentro del programa? ¿Podría escribir un programa similar sin ellos?

Estas preguntas serán el punto de partida para la siguiente fase, donde profundizaré en los conceptos y técnicas que sustentan este ejemplo.

