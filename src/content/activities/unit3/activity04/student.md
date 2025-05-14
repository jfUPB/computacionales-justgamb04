### Análisis 
## **Experimento 1: Modificar el Segmento de Texto**  
**Código:**  
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 1
    ***********************************************************/

    void* ptr = reinterpret_cast<void*>(&main);
    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
    *reinterpret_cast<int*>(ptr) = 0;

    /********************************************************/

    return 0;
}
```

### **¿Qué ocurre?**  
El programa intentará modificar la memoria donde se encuentra el código ejecutable (el segmento de código o **text segment**). Sin embargo, esto provocará un error de segmentación (**segmentation fault**) o una excepción de acceso a memoria en la mayoría de los sistemas operativos modernos.  

### **¿Por qué ocurre esto?**  
1. **El segmento de código es de solo lectura:** La mayoría de los sistemas protegen esta área de memoria para evitar modificaciones accidentales o ataques maliciosos.  
2. **Intentamos escribir en una zona protegida:** `&main` devuelve la dirección de la función `main()`, que se encuentra en la sección de código. Intentar modificarla causa una violación de acceso.  
3. **Las protecciones de seguridad lo impiden:** Los sistemas operativos modernos implementan protecciones como **W^X (Write XOR Execute)**, que evita que una sección de memoria sea simultáneamente ejecutable y escribible.  

## **Experimento 2: Modificar el Segmento de Datos (Constante Global)**  
**Código:**  
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

// Constante global
const char* const mensaje_ro = "Hola, memoria de solo lectura";

int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 2
    ***********************************************************/

    char* ptr = (char*)&mensaje_ro;
    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
    *ptr = 0;

    /********************************************************/

    return 0;
}
```
### **¿Qué ocurre?**  
1. **Segmentación fault:** Si `mensaje_ro` está almacenado en el segmento de solo lectura (**RODATA**), intentaremos modificar memoria protegida, lo que causará un **segmentation fault** o una excepción de acceso a memoria.  
2. **Comportamiento inesperado:** Si el compilador decide colocar `mensaje_ro` en la sección de datos en vez de RODATA, podríamos modificar el puntero, pero **no la cadena de texto en sí**, ya que está en memoria de solo lectura.  

### **¿Por qué ocurre esto?**  
- `mensaje_ro` es un **puntero constante a una cadena de texto constante**.  
- Aunque intentamos modificar el puntero con `(char*)&mensaje_ro`, la cadena `"Hola, memoria de solo lectura"` puede estar en **RODATA**, lo que impide la escritura.  
- El compilador puede optimizar el código y colocar `mensaje_ro` en el **segmento de datos**, pero modificar el contenido sigue siendo ilegal.  

### **Conclusión**  
Ambos experimentos demuestran las restricciones de acceso a los segmentos de memoria en un programa C++ moderno. El sistema protege tanto el código ejecutable como las constantes de solo lectura para evitar errores y ataques de seguridad.
