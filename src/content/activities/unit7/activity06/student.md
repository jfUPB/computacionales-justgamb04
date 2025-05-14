#### Cambios realizados en el código C++

Para lograr que el color del triángulo cambiara automáticamente con el tiempo, primero hice uso de la función `glfwGetTime()` que proporciona GLFW para obtener el tiempo transcurrido desde el inicio de la aplicación. Este valor lo paso al fragment shader como un `uniform`.

En el código C++, justo antes de dibujar el triángulo, obtuve el tiempo actual y lo envié al shader así:

```cpp
double timeValue = glfwGetTime(); // Obtener el tiempo actual
int timeLocation = glGetUniformLocation(shaderProg, "time"); // Ubicar el uniform
glUniform1f(timeLocation, (float)timeValue); // Enviar el valor al shader
```

Este bloque lo puse dentro del loop principal del renderizado, asegurándome de que se actualice en cada frame.

#### Fragment Shader Modificado

```glsl
#version 460 core
out vec4 FragColor;
uniform float time;

void main() {
    float red = (sin(time) + 1.0) / 2.0;
    float green = (cos(time) + 1.0) / 2.0;
    float blue = (sin(time * 0.5) + 1.0) / 2.0;
    FragColor = vec4(red, green, blue, 1.0);
}
```

#### Uso de la función de tiempo

Para lograr el cambio cíclico en el color, usé funciones **trigonométricas** como `sin()` y `cos()`, que son perfectas para este tipo de efectos suaves y repetitivos.
Cada una de las componentes de color (R, G, B) la generé usando una de estas funciones, y escalé el resultado para que esté entre 0.0 y 1.0 (el rango aceptado por `vec4` para colores).

Por ejemplo:

* `sin(time)` oscila entre -1 y 1 → lo paso a \[0, 1] con: `(sin(time) + 1.0) / 2.0`
* Lo mismo hice para `cos(time)` y para un `sin()` más lento en el canal azul.

Esto crea un efecto visual de color pulsante que se ve muy fluido y llamativo.

#### Reflexión

El tiempo como uniform es una herramienta muy poderosa para animar cosas sin necesidad de interacción directa del usuario. Usando tiempo también se podrían lograr efectos como:

* Movimiento automático del triángulo (cambiando su posición con `sin(time)`).
* Oscilaciones en tamaño (escalado suave).
* Rotaciones periódicas (aunque no las hemos visto formalmente, podría combinar `cos` y `sin` para girar).

Una idea interesante sería hacer que el triángulo “respire”, aumentando y disminuyendo su tamaño como si latiera al ritmo del tiempo.

#### Conclusión

Esta actividad me ayudó a entender cómo se puede hacer que un shader trabaje con tiempo para crear animaciones autónomas. Me gustó mucho experimentar con las funciones trigonométricas y ver cómo pequeños cambios en el código generan efectos visuales muy expresivos.

