
## Código 
```cpp
#include <iostream>

using namespace std;

// Función que intenta intercambiar valores pasando por valor (no funcionará correctamente)
void swapPorValor(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

// Función que intercambia valores usando paso por referencia
void swapPorReferencia(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

// Función que intercambia valores usando punteros
void swapPorPuntero(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 5, y = 10;

    // Valores originales
    cout << "Valores originales: x = " << x << ", y = " << y << endl;

    // Prueba de swapPorValor
    swapPorValor(x, y);
    cout << "Después de swapPorValor: x = " << x << ", y = " << y << " (No cambia)\n";

    // Restauramos valores originales
    x = 5;
    y = 10;

    // Prueba de swapPorReferencia
    swapPorReferencia(x, y);
    cout << "Después de swapPorReferencia: x = " << x << ", y = " << y << " (Valores intercambiados correctamente)\n";

    // Restauramos valores originales
    x = 5;
    y = 10;

    // Prueba de swapPorPuntero
    swapPorPuntero(&x, &y);
    cout << "Después de swapPorPuntero: x = " << x << ", y = " << y << " (Valores intercambiados correctamente)\n";

    return 0;
}
```

## **Respuestas a las Preguntas**
### ¿Por qué la versión de `swapPorValor` no logra intercambiar los valores de `x` e `y` en `main()`?
Porque cuando pasamos los parámetros por valor, se crea una copia de las variables originales.  

- Dentro de `swapPorValor`, los valores se intercambian correctamente, pero al terminar la función, estas copias se destruyen y no afectan a las variables originales en `main()`.  
- Ejemplo:  
  - Se crea una copia de `x = 5` y `y = 10`.
  - Se intercambian en la copia (`x = 10, y = 5` dentro de la función).
  - Al salir de la función, las variables originales siguen siendo `x = 5, y = 10`.

### ¿Cómo (`swapPorReferencia` y `swapPorPuntero`) modifican las variables originales?
**swapPorReferencia:**  
- Usa referencias (`&a` y `&b`), lo que significa que `a` y `b` no son copias, sino alias de las variables originales.  
- Cualquier cambio en `a` y `b` dentro de la función también modifica las variables en `main()`.  
- Ejemplo:  
  - `x = 5, y = 10` antes de la función.  
  - Se intercambian dentro de la función (`x = 10, y = 5`).  
  - Al salir de la función, los valores se mantienen intercambiados en `main()`.  

**swapPorPuntero:**  
- Usa punteros (`int *a, int *b`), lo que significa que recibe la dirección de memoria de `x` e `y`.  
- Para modificar los valores originales, se usa el operador de indirección (`*`).  
- Ejemplo:  
  - `x = 5, y = 10` antes de la función.  
  - Se usa `*a` y `*b` para intercambiar los valores en la misma memoria.  
  - Al salir de la función, los valores de `x` e `y` se han intercambiado en `main()`.  

### Ventajas y consideraciones
| Método | Ventajas | Consideraciones |
|--------|---------|----------------|
| **Paso por Valor** | Protege las variables originales (seguridad) | No puede modificar los valores originales |
| **Paso por Referencia** | Código más limpio, más fácil de leer | No es obvio en `main()` que se está modificando la variable |
| **Paso por Puntero** | Permite trabajar con punteros dinámicos y `nullptr` | Requiere manejo de punteros, lo que puede ser más propenso a errores |

**Conclusión:**  
- Si solo quieres modificar los valores originales, usa referencias (`&`).  
- Si necesitas manejar direcciones de memoria o valores dinámicos, usa punteros (`*`).  
- Si solo necesitas leer los valores sin modificarlos, usa paso por valor.  
