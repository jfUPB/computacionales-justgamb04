### Código en C++

```cpp
#include <iostream>

int sum(int a, int b) {
    return a + b;
}

int main() {
    int a = 5;
    int b = 7;
    std::cout << "La suma de " << a << " y " << b << " es " << sum(a, b) << "\n";
    return 0;
}
```

Este código define la función `sum`, que recibe dos enteros y devuelve su suma. Luego, en `main`, se inicializan dos variables `a` y `b`, y se imprime el resultado de la suma en la consola.


### Ejecución Paso a Paso
Las imágenes adjuntas muestran la ejecución del programa en modo de depuración.  

1. **Primera imagen:**
   
   ![image](https://github.com/user-attachments/assets/b7ee1d1d-0d8d-421a-8d7f-fdcb03cf57fe)

   - Se ha colocado un **breakpoint** en la línea `int a = 5;` para detener la ejecución en ese punto.

2. **Segunda imagen:**
   
   ![image](https://github.com/user-attachments/assets/31b5748c-c2d8-42a4-a255-205b193ec13e)
 
   - Se ejecutó paso a paso usando `F10`, lo que permite ver el estado de las variables en la ventana **Autos**.  
   - `a` ya ha sido asignado con el valor `5`, mientras que `b` aún no tiene su valor asignado (`0`).

### Explicación de las Opciones de Depuración en Visual Studio
Al ejecutar paso a paso el código en **Visual Studio**, se tienen varias herramientas de depuración:

| Opción         | Explicación |
|---------------|------------|
| **Continue (F5)** | Reanuda la ejecución del programa hasta el siguiente punto de interrupción o hasta que finalice. |
| **Step Over (F10)** | Ejecuta la siguiente línea de código, pero si hay una función en esa línea, la ejecuta sin entrar en ella. |
| **Step Into (F11)** | Ejecuta la siguiente línea de código y, si hay una función, entra dentro de ella para ver su ejecución paso a paso. |
| **Step Out (Shift + F11)** | Si se está dentro de una función, la ejecuta completamente y regresa a la línea donde fue llamada. |
| **Restart (Ctrl + Shift + F5)** | Reinicia la ejecución del programa desde el inicio. |
| **Stop Debugging (Shift + F5)** | Detiene la ejecución del programa. |

#### **Ejemplo de Uso en el Código**
1. **Step Over (F10):** Si estamos en `main()` y usamos `F10`, el código se ejecuta línea por línea sin entrar a la función `sum()`.  
2. **Step Into (F11):** Si estamos en `std::cout << sum(a, b);` y presionamos `F11`, entramos a la función `sum(int a, int b)`, permitiendo ver cómo se ejecuta.  
3. **Step Out (Shift + F11):** Si estamos dentro de `sum()`, al presionar `Shift + F11`, salimos de la función y regresamos a `main()`.  

### Conclusión
- Aprendimos cómo configurar un proyecto en **Visual Studio** en **C++**.  
- Implementamos un **Hola Mundo** que suma dos números.  
- Usamos la depuración para analizar cómo se ejecuta el código paso a paso.  
- Identificamos el uso de las herramientas de depuración en **Visual Studio**.  
