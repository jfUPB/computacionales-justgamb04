## **Código Modificado**

```cpp
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    // Constructor
    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    // Destructor
    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    // Método para imprimir valores y dirección de memoria
    void imprimir() {
        cout << "Punto(" << x << ", " << y << ") en la dirección " << this << endl;
    }
};

int main() {
    // Objeto en el stack
    Punto pStack(30, 40);
    cout << "Dirección de pStack: " << &pStack << endl;
    pStack.imprimir();

    // Objeto en el heap
    Punto* pHeap = new Punto(50, 60);
    cout << "Valor de pHeap (dirección del objeto en el heap): " << pHeap << endl;
    cout << "Dirección del puntero pHeap (en el stack): " << &pHeap << endl;
    pHeap->imprimir();

    // Liberar la memoria del heap
    delete pHeap;

    return 0;
}
```

## **Explicación**

### Diferencia entre objetos en el **stack** y en el **heap**:

- **Stack**: la memoria es administrada automáticamente. El objeto `pStack` se crea al entrar al `main()` y se destruye automáticamente al salir del mismo.
- **Heap**: la memoria es administrada manualmente. El objeto `pHeap` se crea con `new` y debe eliminarse con `delete`.

### Comparación de direcciones:

- `&pStack`: muestra la dirección del objeto en el stack.
- `pHeap`: contiene la dirección del objeto creado dinámicamente en el heap.
- `&pHeap`: es la dirección del puntero (variable) que está en el stack y apunta a un objeto en el heap.

Ejemplo de salida (referencial):
```
Dirección de pStack: 0x61ff08
Punto(30, 40) en la dirección 0x61ff08
Valor de pHeap (dirección del objeto en el heap): 0x9b6140
Dirección del puntero pHeap (en el stack): 0x61fef8
Punto(50, 60) en la dirección 0x9b6140
```

### ¿pStack es un objeto o una referencia?

Es un objeto real creado en el stack. No es una referencia ni un puntero.

### ¿pHeap es un objeto o una referencia?

Es un puntero (referencia) que apunta a un objeto de tipo `Punto` que vive en el heap. Es decir, `pHeap` no es el objeto como tal, sino una variable que contiene la dirección del objeto creado dinámicamente.

### Observación en **Memory1** (simulada):

- Al inspeccionar `&pHeap` en la ventana de memoria (`Memory1`), se muestra el contenido del puntero, es decir, la dirección en el heap donde se encuentra el objeto.
- En la pestaña de **Locals**, `pHeap` muestra esa misma dirección como su valor.
- Esto confirma que `pHeap` apunta efectivamente a un objeto alocado en el heap, y que la dirección que almacena se guarda en una variable ubicada en el stack.

### ¿Qué significa esto?

Significa que, aunque el puntero `pHeap` está en el stack (como cualquier variable local), el objeto al que apunta fue creado dinámicamente y reside en el heap, permitiendo su existencia más allá del ámbito local si se desea.
