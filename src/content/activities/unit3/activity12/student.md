### **Parte 1: Objeto en el stack vs objeto en el heap**

#### **Código base:**

```cpp
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    {
        cout << "Inicio del bloque" << endl;
        Punto pBloque(100, 200);
        pBloque.imprimir();
    }
    cout << "Fuera del bloque" << endl;

    Punto* pDinamico = new Punto(300, 400);
    pDinamico->imprimir();
    delete pDinamico;

    return 0;
}
```
### **Explicación del ciclo de vida:**

#### Objeto en el stack (`pBloque`)
- **Se crea dentro de un bloque `{}`**, por tanto se destruye **automáticamente al finalizar ese bloque.**
- El destructor se llama **al salir del bloque.**
- Su memoria está ubicada en la **pila (stack)**.

#### Objeto en el heap (`pDinamico`)
- Se crea usando `new`, y **no se destruye automáticamente.**
- El objeto permanece **hasta que se invoque explícitamente `delete`.**
- La memoria del puntero `pDinamico` está en el **stack**, pero el objeto al que apunta está en el **heap (montículo)**.

## **Parte 2: Código con error de compilación**

```cpp
int main() {
    {
        cout << "Inicio del bloque 2" << endl;
        Punto* pBloque2 = new Punto(500, 600);
        pBloque2->imprimir();
    }
    pBloque2->imprimir();  //  Error: pBloque2 no existe aquí
    delete pBloque2;
    return 0;
}
```

### **¿Compila?**  
**No.** El compilador da error: **`pBloque2` no está declarado en este ámbito.**  
Esto ocurre porque `pBloque2` fue **declarado dentro del bloque**, y por lo tanto **no existe fuera de él**.

## **Parte 3: Declarar `pBloque2` fuera e inicializar dentro**

```cpp
int main() {
    Punto* pBloque2 = nullptr;
    {
        cout << "Inicio del bloque 2" << endl;
        pBloque2 = new Punto(500, 600);
        pBloque2->imprimir();
    }
    pBloque2->imprimir();
    delete pBloque2;
    return 0;
}
```

### ¿Compila?  
**Sí.** En este caso `pBloque2` fue **declarado fuera del bloque**, por lo tanto **su alcance abarca todo `main`**, y se puede usar después del bloque.

## **Parte 4: Preguntas de análisis**

### **¿Por qué el objeto `pBloque` se destruye al salir del bloque y `pBloque2` no?**

- `pBloque` fue creado **como una instancia directa (no puntero)** dentro del bloque. Al salir del bloque, se llama **automáticamente su destructor.**
- `pBloque2` es un **puntero**. El objeto al que apunta fue creado con `new`, así que **su destrucción depende del uso de `delete`**, no del fin del bloque.

### **¿`pBloque2` es un objeto o una referencia a un objeto?**

- `pBloque2` **no es un objeto**, es un **puntero (referencia) a un objeto**.  
- El objeto en sí se encuentra en el **heap** y `pBloque2` guarda su dirección.

### **¿Dónde se almacena `pBloque2` y dónde el objeto al que apunta?**

| Elemento         | Segmento de memoria | Descripción                                                   |
|------------------|---------------------|---------------------------------------------------------------|
| `pBloque2`       | **Stack (pila)**    | Variable local dentro de `main`, guarda una dirección.       |
| `*pBloque2`      | **Heap (montículo)**| El objeto `Punto(500, 600)` está en memoria dinámica.        |

## **Conclusiones**

- Los objetos creados en el **stack** tienen **vida limitada al bloque** donde se declaran.
- Los objetos creados en el **heap** viven hasta que se liberen con `delete`, aunque la variable que los apunta haya salido de alcance.
- Declarar un puntero permite manejar objetos dinámicos que sobreviven a los bloques locales.
- Se debe tener cuidado de **liberar la memoria con `delete`** para evitar fugas de memoria.
