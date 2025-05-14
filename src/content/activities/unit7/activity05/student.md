#### Modificación del Código

Para lograr el comportamiento interactivo, se realizaron modificaciones tanto en los shaders como en el código C++. En los shaders, se introdujeron dos nuevos **uniforms**:

1. **`offset`**: Este uniform es utilizado en el vertex shader para modificar la posición del triángulo en la pantalla.
2. **`ourColor`**: Este uniform es utilizado en el fragment shader para cambiar el color del triángulo.

Cómo se implementaron los shaders:

**Vertex Shader:**

```glsl
#version 460 core
layout(location = 0) in vec3 aPos;
uniform vec2 offset;

void main() {
    vec3 newPos = aPos;
    newPos.x += offset.x;
    newPos.y += offset.y;
    gl_Position = vec4(newPos, 1.0);
}
```

**Fragment Shader:**

```glsl
#version 460 core
out vec4 FragColor;
uniform vec4 ourColor;

void main() {
    FragColor = ourColor;
}
```

En el código C++, se obtuvieron las posiciones del mouse y se normalizaron para ajustarse al sistema de coordenadas de OpenGL. La normalización de las coordenadas del mouse permite mapearlas de 0 a 1 (en píxeles) a un rango de -1 a 1, que es el espacio de coordenadas que OpenGL utiliza para dibujar.

**Código C++ para pasar los uniforms:**

```cpp
glUseProgram(shaderProg);
int offsetLocation = glGetUniformLocation(shaderProg, "offset");
int colorLocation = glGetUniformLocation(shaderProg, "ourColor");

// Obtener la posición del mouse
double xpos, ypos;
glfwGetCursorPos(mainWindow, &xpos, &ypos);

// Normalizar las coordenadas del mouse
float x = (float)xpos / (float)SCR_WIDTH;
x = x < 0 ? 0 : (x > 1 ? 1 : x);

float y = (float)ypos / (float)SCR_HEIGHT;
y = y < 0 ? 0 : (y > 1 ? 1 : y);

// Enviar el color y la posición del triángulo
glUniform4f(colorLocation, x, y, 0.0f, 1.0f);

// Enviar el offset del triángulo (normalizado a NDC)
glUniform2f(offsetLocation, x * 2 - 1, 1 - y * 2);

glBindVertexArray(VAO);
glDrawArrays(GL_TRIANGLES, 0, 3);

// Intercambiar buffers
glfwSwapBuffers(mainWindow);
```

#### Normalización de las Coordenadas del Mouse

En este paso, las coordenadas del mouse se obtenían en píxeles, pero OpenGL utiliza un sistema de coordenadas diferente, donde el centro de la pantalla es `(0, 0)` y los valores van de `-1` a `1`.

Para adaptar las coordenadas del mouse al sistema de coordenadas de OpenGL, se realizó una **normalización** de las coordenadas de la siguiente manera:

1. La coordenada `x` se transformó del rango `[0, 1]` a `[-1, 1]` con la fórmula:
   `x_normalizado = x * 2 - 1`

2. La coordenada `y` se transformó de manera similar, pero también se invirtió el eje Y (ya que OpenGL tiene el origen en la esquina inferior izquierda, mientras que las coordenadas del mouse están en la esquina superior izquierda):
   `y_normalizado = 1 - y * 2`

Este proceso asegura que las coordenadas del mouse sean adecuadas para ser usadas en OpenGL, donde los valores de las coordenadas están en el rango de `-1` a `1`.

#### Normalización a Coordenadas de Dispositivo Normalizadas (NDC)

OpenGL utiliza el espacio de coordenadas de **dispositivo normalizado** (NDC), en el que las coordenadas de los vértices van de `-1` a `1` en ambos ejes `x` y `y`. La normalización permite convertir las coordenadas del mouse, que están en píxeles, al sistema de coordenadas NDC. Este proceso implica convertir las coordenadas del mouse al rango `[-1, 1]` para que OpenGL pueda procesarlas correctamente.

El proceso de **normalización a NDC** asegura que las coordenadas del mouse se ajusten al espacio de OpenGL, permitiendo que el triángulo se mueva y cambie de color en función de la posición del mouse en la ventana.

#### Conclusión

En esta actividad, aprendí a trabajar con **uniforms** en OpenGL para hacer un triángulo interactivo, cambiando su posición y color en función de la ubicación del mouse. La normalización de las coordenadas fue clave para hacer que las posiciones del mouse se ajustaran al sistema de coordenadas de OpenGL, permitiendo una interacción fluida y precisa con el triángulo.
