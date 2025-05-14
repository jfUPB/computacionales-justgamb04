### ¿Qué es una cola y cómo funciona el principio FIFO?

Una cola es una estructura de datos lineal que sigue el principio FIFO, que significa "First In, First Out" o "el primero en entrar es el primero en salir". Esto quiere decir que los elementos se insertan por un extremo (llamado final o `rear`) y se eliminan por el otro extremo (llamado frente o `front`).

Una forma simple de imaginarlo es pensar en una fila de personas esperando para ser atendidas. La primera persona en llegar será la primera en salir de la fila cuando sea su turno. De la misma forma, en una cola de programación, el primer elemento en entrar es el primero que se procesa o elimina.

### ¿Cómo se implementa `enqueue()` y `dequeue()` en una cola?

Para implementar una cola manualmente en C++, se puede usar una estructura de nodos enlazados. Cada nodo contiene un dato y un puntero al siguiente nodo.

**Definición del nodo:**

```cpp
struct Node {
    int dato;
    Node* next;
};
```

**Definición de la clase de la cola:**

```cpp
class Cola {
public:
    Node* front; // Apunta al primer elemento
    Node* rear;  // Apunta al último elemento

    Cola() {
        front = nullptr;
        rear = nullptr;
    }
};
```

**Método `enqueue()` (insertar al final):**

```cpp
void Cola::enqueue(int valor) {
    Node* nuevo = new Node();
    nuevo->dato = valor;
    nuevo->next = nullptr;

    if (rear == nullptr) {
        // La cola está vacía
        front = rear = nuevo;
    } else {
        // Hay elementos en la cola
        rear->next = nuevo;
        rear = nuevo;
    }
}
```

**Método `dequeue()` (eliminar del frente):**

```cpp
void Cola::dequeue() {
    if (front == nullptr) return; // Cola vacía

    Node* temp = front;
    front = front->next;

    if (front == nullptr) {
        // La cola quedó vacía
        rear = nullptr;
    }

    delete temp;
}
```

### Un error común en la implementación y cómo evitarlo

Un error muy común al implementar una cola es **no actualizar el puntero `rear` cuando se elimina el último nodo de la cola**. Si se hace `dequeue()` y el nodo eliminado era el único, entonces la cola queda vacía. En ese caso, si no se actualiza `rear` a `nullptr`, se corre el riesgo de que `rear` apunte a memoria liberada, lo que puede provocar fallos o errores difíciles de detectar más adelante.

La solución es asegurarse de que después de hacer `front = front->next`, si `front` queda siendo `nullptr`, también se debe hacer `rear = nullptr`.

### Conclusión

Una cola es una estructura útil para situaciones donde el orden de llegada es importante. Implementarla desde cero ayuda a entender el manejo de punteros y memoria dinámica en C++. Recordar el principio FIFO y manejar correctamente los casos en que la cola se vacía es fundamental para evitar errores en la implementación.

