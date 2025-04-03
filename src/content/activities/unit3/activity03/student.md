### **Código en C++**
![image](https://github.com/user-attachments/assets/cc8ca39e-15d0-471d-8a6e-b218de6d3615)
![image](https://github.com/user-attachments/assets/f9dd4334-b06e-4ead-a65f-d78922a0f377)
![image](https://github.com/user-attachments/assets/dfa240fd-1025-4707-91f6-06905e2c8cdd)
![image](https://github.com/user-attachments/assets/3d8d96c7-734f-4845-8338-98c6dede2cf5)

```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

// Variables globales
int global_inicializada = 42;
int global_no_inicializada;

// Constante global (memoria de solo lectura)
const char* const mensaje_ro = "Hola, memoria de solo lectura";

// Función con variable estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
}

// Función que asigna memoria en el Heap
int* crearArrayHeap(int tam) {
    int* arr = new int[tam];
    for (int i = 0; i < tam; i++) {
        arr[i] = i;
    }
    return arr;
}

// Función de ejemplo (ubicada en la región de código)
int suma(int a, int b) {
    int c = a + b; // "c" es una variable local (stack)
    return c;
}

int main() {
    // Variable local (stack)
    int a = 10; // <-- Coloca un breakpoint aquí
    int b = 20;
    int c = suma(a, b);

    cout << "Resultado de suma(a, b): " << c << endl;
    cout << "Dirección de variable local 'a': " << &a << endl;
    cout << "Dirección de variable local 'b': " << &b << endl;
    cout << "Dirección de la variable local 'c' (resultado): " << &c << endl;

    // Variables globales
    cout << "Dirección de 'global_inicializada': " << &global_inicializada << endl;
    cout << "Dirección de 'global_no_inicializada': " << &global_no_inicializada << endl;

    // Constante global (solo lectura)
    cout << "Dirección de 'mensaje_ro' (zona de solo lectura): " 
         << static_cast<const void*>(mensaje_ro) << endl;

    // Llamada a función que tiene variable estática
    funcionConStatic();

    // Uso del Heap: asignación dinámica
    int tamArray = 10;
    int* arrayHeap = crearArrayHeap(tamArray);
    cout << "Dirección del primer elemento del array asignado en Heap: " << arrayHeap << endl;
    
    for (int i = 0; i < tamArray; i++) {
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i]
            << " en " << (arrayHeap + i) << endl;
    }

    delete[] arrayHeap; // Liberamos la memoria dinámica

    return 0;
}
```

### **Resultados esperados en la ejecución**
Después de ejecutar el programa, se imprimen las direcciones de memoria de las variables en diferentes segmentos. Un ejemplo de salida podría verse así (las direcciones variarán):

```
Resultado de suma(a, b): 30
Dirección de variable local 'a': 0x7ffcd1234568
Dirección de variable local 'b': 0x7ffcd123456c
Dirección de la variable local 'c' (resultado): 0x7ffcd1234570

Dirección de 'global_inicializada': 0x601020
Dirección de 'global_no_inicializada': 0x601024

Dirección de 'mensaje_ro' (zona de solo lectura): 0x400780

Dirección de var_estatica (static): 0x601030

Dirección del primer elemento del array asignado en Heap: 0x558a6cdda4c0
arrayHeap[0] = 0 en 0x558a6cdda4c0
arrayHeap[1] = 1 en 0x558a6cdda4c4
arrayHeap[2] = 2 en 0x558a6cdda4c8
...
```

### **Mapa de Memoria del Programa**
Basado en la salida anterior, se puede organizar la memoria de la siguiente manera (las direcciones están en orden descendente):

```
+-------------------------------+
|   Segmento de Código (Text)   |  <- 0x400000 (Ejemplo)
|   - Función main()             |
|   - Función suma()             |
+-------------------------------+
|   Segmento de Solo Lectura    |  <- 0x400780 (mensaje_ro)
+-------------------------------+
| Variables Globales y Estáticas |  <- 0x601020 (globales)
|   - global_inicializada        |  0x601020
|   - global_no_inicializada     |  0x601024
|   - var_estatica (static)      |  0x601030
+-------------------------------+
|           Heap                 |  <- 0x558a6cdda4c0 (inicio)
|   - arrayHeap[0]               |  0x558a6cdda4c0
|   - arrayHeap[1]               |  0x558a6cdda4c4
|   - arrayHeap[2]               |  0x558a6cdda4c8
|   - ...                        |
+-------------------------------+
|           Stack                |  <- 0x7ffcd1234568 (inicio)
|   - Variable local 'a'         |  0x7ffcd1234568
|   - Variable local 'b'         |  0x7ffcd123456c
|   - Variable local 'c'         |  0x7ffcd1234570
+-------------------------------+
```


### **Conclusión**
- **Segmento de Código (Text):** Contiene las instrucciones del programa.
- **Segmento de Solo Lectura:** Contiene constantes como `mensaje_ro`.
- **Segmento de Datos (Variables Globales y Estáticas):** Almacena `global_inicializada`, `global_no_inicializada` y `var_estatica`.
- **Heap:** Se usa para la memoria dinámica (array `arrayHeap`).
- **Stack:** Contiene las variables locales (`a`, `b`, `c`) y direcciones de retorno de funciones.
