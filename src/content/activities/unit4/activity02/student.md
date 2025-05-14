### 1. Lista enlazada con 3 y 4 nodos

**Con 3 nodos:**

```
[Node1] → [Node2] → [Node3] → nullptr
```

* **Node1**: posición (x1, y1), `next` apunta a Node2.
* **Node2**: posición (x2, y2), `next` apunta a Node3.
* **Node3**: posición (x3, y3), `next` es `nullptr`.

**Con 4 nodos:**

```
[Node1] → [Node2] → [Node3] → [Node4] → nullptr
```

* Se agrega **Node4** al final, y el `next` de Node3 ahora apunta a Node4.

### 2. Objeto de la clase `LinkedList` con 3 nodos

```
head → [Node1] → [Node2] → [Node3] → nullptr
tail -----------------------------↑
size = 3
```

* **head** apunta a Node1.
* **tail** apunta a Node3.
* **size** es 3.

### 3. ¿Qué pasa si falta `head`, `tail` o `size`?

* **Sin `head`**: No podrías recorrer la lista desde el inicio, ya que no tendrías un punto de entrada.
* **Sin `tail`**: Agregar nodos al final requeriría recorrer toda la lista para encontrar el último nodo, lo que reduce la eficiencia.
* **Sin `size`**: No podrías conocer rápidamente cuántos nodos hay en la lista; tendrías que recorrerla completamente para contarlos.

### 4. Importancia del destructor `~LinkedList()`

El destructor llama al método `clear()`, que libera la memoria de todos los nodos. Esto es crucial porque en C++, la gestión de memoria es manual. Si no liberas la memoria, puedes causar fugas que deterioren el rendimiento o provoquen fallos en el programa.

### 5. Diferencia entre C# y C++ en la gestión de memoria

En C#, existe un recolector de basura que automáticamente libera la memoria de los objetos no utilizados. En cambio, en C++, debes liberar manualmente la memoria utilizando `delete`. No hacerlo puede resultar en fugas de memoria y otros problemas relacionados con la gestión de recursos.

### 6. Comportamiento de `push_back` con diferentes tamaños de lista

**Cuando `size = 0`:**

```
head → [Node1] → nullptr
tail ---------↑
size = 1
```

**Cuando `size = 1`:**

```
head → [Node1] → [Node2] → nullptr
tail -------------------↑
size = 2
```

**Cuando `size = 2`:**

```
head → [Node1] → [Node2] → [Node3] → nullptr
tail ---------------------------↑
size = 3
```

Cada llamada a `push_back` agrega un nuevo nodo al final y actualiza `tail` y `size` en consecuencia.

### 7. Comportamiento de `pop_back` con diferentes tamaños de lista

**Cuando `size = 1`:**

```
Antes:
head → [Node1] → nullptr
tail ---------↑
size = 1

Después de pop_back:
head = nullptr
tail = nullptr
size = 0
```

**Cuando `size = 2`:**

```
Antes:
head → [Node1] → [Node2] → nullptr
tail -------------------↑
size = 2

Después de pop_back:
head → [Node1] → nullptr
tail ---------↑
size = 1
```

`pop_back` elimina el último nodo y actualiza `tail` y `size` adecuadamente.

### 8. Comportamiento de `clear()`

Durante la ejecución de `clear()`, se recorre la lista desde `head`, eliminando cada nodo y avanzando al siguiente hasta que todos han sido eliminados.

```
Proceso:
current = head
while current != nullptr:
    nextNode = current->next
    delete current
    current = nextNode

Después:
head = nullptr
tail = nullptr
size = 0
```

Esto asegura que toda la memoria asignada a los nodos sea liberada.

### 9. Funciones `setup()`, `update()`, `draw()` y `keyPressed()`

* **`setup()`**: Inicializa la serpiente con 20 nodos en el centro de la pantalla y establece el tono de fondo en 0.

* **`update()`**: Mueve cada nodo de la serpiente hacia la posición del mouse utilizando interpolación lineal (`glm::mix`). También actualiza el tono de fondo.

* **`draw()`**: Dibuja un fondo con un gradiente de color y representa la serpiente como una línea de nodos con colores y tamaños variables.

* **`keyPressed()`**: Maneja las teclas presionadas:

  * `'c'`: Limpia la lista de nodos.
  * `'a'`: Agrega un nuevo nodo en una posición aleatoria.
  * `'r'`: Elimina el último nodo.
  * `'s'`: Guarda una captura de pantalla.

### 10. Análisis del código de interpolación en `update()`

```cpp
Node* current = snake.head;
while (current != nullptr) {
    current->position = glm::mix(glm::vec3(current->position, 0.0f), glm::vec3(target, 0.0f), interpolationFactor);
    target = current->position;
    current = current->next;
}
```

Este fragmento de código realiza una interpolación lineal entre la posición actual de cada nodo y la posición objetivo (inicialmente la del mouse). El factor de interpolación determina cuánto se mueve cada nodo hacia el objetivo. Al actualizar `target` con la nueva posición del nodo, se crea un efecto de seguimiento donde cada nodo sigue al anterior.
