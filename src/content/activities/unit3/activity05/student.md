### Análisis 

## **Experimento 3: Modificar el Segmento de Datos (Variables Globales)**  
**Código:**  
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

// Variables globales
int global_inicializada = 42;
int global_no_inicializada;

int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 3
    ***********************************************************/

    cout << "global_inicializada: " << global_inicializada << endl;
    cout << "global_no_inicializada: " << global_no_inicializada << endl;

    global_inicializada = 69;
    global_no_inicializada = 666;

    cout << "global_inicializada: " << global_inicializada << endl;
    cout << "global_no_inicializada: " << global_no_inicializada << endl;

    /********************************************************/

    return 0;
}
```

### **¿Qué ocurre?**  
El programa compila y ejecuta sin errores, y podemos modificar sin problema las variables globales. La salida esperada será:  

```
global_inicializada: 42
global_no_inicializada: 0  // Dependerá del compilador, pero en Visual Studio suele inicializarse en 0.
global_inicializada: 69
global_no_inicializada: 666
```

### **¿Por qué ocurre esto?**  
1. **Las variables globales están en la sección de datos de la memoria.**  
   - `global_inicializada = 42;` está en la **sección de datos (Data Segment)** porque se inicializa con un valor explícito.  
   - `global_no_inicializada;` está en la **sección BSS (Block Started by Symbol)** y es inicializada automáticamente en **0** por el sistema en tiempo de ejecución.  

2. **Las variables globales son accesibles desde cualquier parte del programa** y pueden modificarse libremente, ya que no están protegidas como las constantes o el código ejecutable.  

## **Experimento 4: Modificar la Variable Local Estática de una Función por Fuera de Ella**  
**Código (con error):**  
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

// Función de ejemplo que muestra la dirección de su variable local estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
}

int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 4
    ***********************************************************/

    var_estatica = 42;

    cout << "var_estatica: " << var_estatica << endl;

    /********************************************************/
    return 0;
}
```


### **¿Qué ocurre?**  
El código no compilará:  

### **¿Por qué ocurre esto?**  
1. **`var_estatica` es una variable local estática dentro de la función `funcionConStatic()`, por lo que solo existe dentro de esa función.**  
   - No es accesible desde `main()`, ya que **su alcance (scope) es local a la función en la que está declarada**.  
   - Las variables estáticas dentro de una función **se almacenan en la sección de datos (Data Segment)**, pero no pueden usarse fuera de su función.  

2. **Si queremos modificar `var_estatica`, debemos hacerlo dentro de `funcionConStatic()`.**  
   - Una forma correcta sería modificar `funcionConStatic()` para permitir cambiar su valor:

   ```cpp
   void funcionConStatic(int nuevo_valor) {
       static int var_estatica = 100;
       var_estatica = nuevo_valor;
       cout << "var_estatica: " << var_estatica << endl;
   }
   ```

   Luego, en `main()`, podemos llamarla así:

   ```cpp
   funcionConStatic(42);
   ```

### **¿Qué pasa con las variables cada que entras y sales de la función?**  
1. **Las variables locales normales (no estáticas) se crean y destruyen en cada llamada a la función.**  
   - Se almacenan en el **stack**.  
   - Se pierden una vez que la función termina.  

2. **Las variables estáticas dentro de una función NO se destruyen al salir de la función.**  
   - Se almacenan en la **sección de datos (Data Segment)**, no en el stack.  
   - Conservan su valor entre llamadas a la función.  
   - Solo se inicializan una vez, la primera vez que la función se ejecuta.  

### **Conclusión**  
- **Experimento 3:** Las variables globales pueden modificarse sin problema porque están en la **sección de datos** y son accesibles desde cualquier parte del código.  
- **Experimento 4:** No podemos acceder a una variable estática de una función fuera de ella, porque **su alcance es local a la función**, aunque su tiempo de vida sea todo el programa.
