## **Experimento 5: Variable local estática vs no estática**

### **Código:**
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

// Función con variable local estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "var_estatica: " << var_estatica << endl;
    var_estatica++;
}

// Función con variable local no estática
void funcionSinStatic() {
    int var_no_estatica = 100;
    cout << "var_no_estatica: " << var_no_estatica << endl;
    var_no_estatica++;
}

int main() {
    for (int i = 0; i < 5; i++) {
        cout << "Iteración " << i << endl;
        funcionSinStatic();
        funcionConStatic();
    }

    return 0;
}
```

### **¿Qué ocurre?**
La salida será algo como:

```
Iteración 0
var_no_estatica: 100
var_estatica: 100
Iteración 1
var_no_estatica: 100
var_estatica: 101
Iteración 2
var_no_estatica: 100
var_estatica: 102
Iteración 3
var_no_estatica: 100
var_estatica: 103
Iteración 4
var_no_estatica: 100
var_estatica: 104
```

### **¿Por qué ocurre esto?**
- La **variable no estática (`var_no_estatica`)** se **crea y destruye cada vez** que se entra y sale de la función `funcionSinStatic()`. Siempre inicia en 100.
- La **variable estática (`var_estatica`)** **se conserva entre llamadas**, porque solo se inicializa una vez y mantiene su valor. Es persistente, aunque su alcance es local.

### **¿Ves alguna diferencia entre las variables locales estáticas y no estáticas?**
Sí:
- Las **no estáticas** viven solo mientras la función se está ejecutando. Están en el **stack**.
- Las **estáticas** permanecen vivas hasta que el programa termina. Están en la **sección de datos**.

### **¿Qué pasa con las variables cada que entras y sales de la función?**
- Las variables **no estáticas** se destruyen al salir.
- Las **estáticas** conservan su estado entre llamadas, pero no pueden ser accedidas desde fuera de la función.


## **Experimento 6: Modificar el segmento de Heap**

### **Código:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int tam = 5;
    int* arrayHeap = new int[tam];

    for (int i = 0; i < tam; i++) {
        arrayHeap[i] = (i + 1) * 10;
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i]
            << " en dirección " << (arrayHeap + i) << endl;
    }

    // Liberar la memoria
    delete[] arrayHeap;

    /**********************************************************
        EXPERIMENTO 6
    ***********************************************************/
    cout << arrayHeap[0] << endl;
    /**********************************************************/

    return 0;
}
```

### **¿Qué ocurre?**
- El programa **compila**, pero puede arrojar un **comportamiento indefinido** al ejecutar `cout << arrayHeap[0] << endl;` después de liberar la memoria con `delete[]`.

**Resultados:**
- Se imprime un valor basura.
- Se genera una excepción de acceso inválido.
- No imprime nada.
- En depuración, puede aparecer un error del tipo **"access violation"**.

### **¿Por qué?**
Porque se está **accediendo a memoria que ya fue liberada**, lo cual es ilegal. Aunque el puntero `arrayHeap` sigue existiendo, ya no apunta a memoria válida del Heap.

#### Diferencias
- **Heap:**
  - Controlado manualmente por el programador (con `new` y `delete`).
  - La memoria **permanece viva** hasta que se libere explícitamente.
  - Mayor flexibilidad, pero más propenso a errores.
- **Stack:**
  - Controlado automáticamente por el compilador.
  - Variables se crean y destruyen al entrar/salir del bloque o función.
  - Más seguro y rápido, pero con límite de espacio.

#### Consecuencias 
- Se produce una **fuga de memoria (memory leak)**.
- Si se repite muchas veces en un programa grande, puede causar:
  - Uso excesivo de memoria.
  - Disminución del rendimiento.
  - Cierre inesperado del programa.

#### ¿Por qué es importante usar `delete[]` al liberar memoria asignada para un arreglo?
- Porque `new[]` y `delete[]` van **en pareja**. Usar solo `delete` en vez de `delete[]` podría:
  - No liberar toda la memoria del arreglo.
  - Invocar incorrectamente destructores (en caso de objetos).
  - Provocar errores de ejecución.

## **Conclusión**
- **Las variables estáticas** son útiles cuando queremos conservar información entre llamadas a una función sin que sea global.
- **El Heap es poderoso pero peligroso** si no se gestiona con cuidado.
- Siempre que uses `new[]`, **usa `delete[]` para evitar fugas** de memoria y errores inesperados.
