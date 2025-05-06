
#### **Dibujo**
![image](https://github.com/user-attachments/assets/a462f7d0-80a1-4460-b8d1-f9fa96a49f3d)


Supongamos que la lista tiene 5 nodos. Cada nodo tiene una posición en el plano y está conectado al siguiente:

```
[ (x0, y0) ] → [ (x1, y1) ] → [ (x2, y2) ] → [ (x3, y3) ] → [ (x4, y4) ] → nullptr
```

* Cada nodo representa una posición (un `glm::vec2`) en el espacio 2D.
* La flecha (`→`) representa el enlace al siguiente nodo de la lista.
* `nullptr` indica el final de la lista.

##### Inserción de un nodo

Por ejemplo, si se presiona la tecla `'a'`, se añade un nodo al final de la lista:

```
[ (x0, y0) ] → [ (x1, y1) ] → [ (x2, y2) ] → [ (x3, y3) ] → [ (x4, y4) ] → [ (xn, yn) ] → nullptr
```

##### Eliminación de un nodo

Si se presiona `'r'`, se elimina el nodo más reciente (último de la lista):

```
[ (x0, y0) ] → [ (x1, y1) ] → [ (x2, y2) ] → [ (x3, y3) ] → nullptr
```

##### Limpieza de la lista

Si se presiona `'c'`, se eliminan todos los nodos:

```
Lista vacía
```

#### **Respuestas a las preguntas del enunciado**

**¿Cómo se crea la lista enlazada?**

La lista se declara como atributo en la clase `ofApp` usando la clase estándar `std::list` de C++:

```cpp
std::list<glm::vec2> snake;
```

Esto crea una lista enlazada vacía que guardará nodos con posiciones `glm::vec2`.

**¿Cómo se añaden los primeros nodos a la lista?**

Se añaden en el método `setup()` usando un ciclo `for`:

```cpp
for (int i = 0; i < 20; i++) {
    snake.emplace_back(ofGetWidth() / 2, ofGetHeight() / 2);
}
```

Esto inserta 20 nodos con la misma posición central (centro de la pantalla).

**¿Cómo se añaden nodos adicionales a la lista?**

Cuando se presiona la tecla `'a'`, se ejecuta este fragmento en `keyPressed()`:

```cpp
else if (key == 'a') {
    snake.emplace_back(ofRandomWidth(), ofRandomHeight());
}
```

Este método añade un nuevo nodo al final de la lista, con posición aleatoria.

**¿Cómo se eliminan nodos de la lista?**

Con la tecla `'r'` se ejecuta:

```cpp
else if (key == 'r') {
    if (!snake.empty()) {
        snake.pop_back();
    }
}
```

Este código elimina el último nodo de la lista (el más nuevo).


**¿Cómo se limpia la lista?**

Presionando `'c'`, se ejecuta:

```cpp
if (key == 'c') {
    snake.clear();
}
```

Este método borra todos los nodos, dejando la lista vacía.

**¿Cómo se verifica si la lista está vacía?**

Con el método:

```cpp
if (!snake.empty())
```

Se evalúa si hay nodos presentes. Si devuelve `false`, la lista está vacía.
