### **Código base:**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Punto {
public:
    string name;
    int x;
    int y;

    // Constructor
    Punto(string _name, int _x, int _y) : name(_name), x(_x), y(_y) {
        cout << "Constructor: Punto " << name << "(" << x << ", " << y << ") creado." << endl;
    }

    // Destructor
    ~Punto() {
        cout << "Destructor: Punto " << name << "(" << x << ", " << y << ") destruido." << endl;
    }

    void imprimir() {
        cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
    }
};

void cambiarNombre(Punto p, string nuevoNombre) {
    p.name = nuevoNombre;
}

int main() {
    Punto original("original", 70, 80);
    original.imprimir();

    cambiarNombre(original, "cambiado");
    original.imprimir();

    return 0;
}
```

### **1. ¿Qué ocurre después de llamar a la función `cambiarNombre`?**

Después de llamar a la función `cambiarNombre(original, "cambiado")`, **no cambia el nombre del objeto `original`**. Esto se debe a que se está pasando el objeto **por valor**, por lo tanto:

- Se crea una **copia temporal** del objeto `original` llamada `p`.
- El nombre de `p` se cambia, pero esta copia se destruye al finalizar la función.
- Por eso aparece el mensaje:  
  **Destructor: Punto cambiado(70, 80) destruido.**
- `original` sigue siendo el mismo, sin cambios.

### **2. ¿Por qué `original` sigue existiendo luego de llamar `cambiarNombre`?**

Porque se está pasando el objeto por **valor**. La función trabaja con una **copia del objeto original**, no con el objeto mismo. Cuando termina la función, esa copia se destruye y `original` permanece intacto.

### **3. ¿Dónde se encuentra `original` y dónde `p`? ¿Son el mismo objeto?**

- `original` se encuentra en la **pila (stack)** del `main()`.
- `p` también se encuentra en la pila, **pero dentro del stack frame de `cambiarNombre`**, en una dirección distinta.
- **No son el mismo objeto**, son dos instancias separadas con el mismo contenido.

### **4. Versión modificada: Paso por referencia**

```cpp
void cambiarNombre(Punto& p, string nuevoNombre) {
    p.name = nuevoNombre;
}
```

**¿Qué ocurre ahora?**

- El nombre del objeto `original` **sí se cambia a "cambiado"**.
- Al pasar por **referencia**, la función trabaja directamente sobre el objeto original, no sobre una copia.
- No se crea ni destruye ningún objeto nuevo.
- El destructor **no se llama** al terminar la función.

### **5. Versión modificada: Paso por puntero**

```cpp
void cambiarNombre(Punto* p, string nuevoNombre) {
    p->name = nuevoNombre;
}

int main() {
    Punto original("original", 70, 80);
    original.imprimir();

    cambiarNombre(&original, "cambiado");
    original.imprimir();

    return 0;
}
```

**¿Qué ocurre ahora?**

- El nombre del objeto `original` **también se cambia a "cambiado"**.
- Se pasa un **puntero** a la función, que permite acceder directamente al objeto original.
- Al igual que con la referencia, **no se crea una copia**, y el objeto original es modificado.

## **Diferencias entre pasar por valor, por referencia y por puntero**

| Modo de paso       | ¿Se modifica el original? | ¿Se crea una copia? | Sintaxis en llamada | Seguridad y claridad        |
|--------------------|----------------------------|----------------------|----------------------|-----------------------------|
| **Por valor**       | No                         | Sí                   | `cambiarNombre(original, "c")` | Simple pero ineficiente si el objeto es grande |
| **Por referencia**  | Sí                         | No                   | `cambiarNombre(original, "c")` | Requiere cuidado, pero es claro y seguro |
| **Por puntero**     | Sí                         | No                   | `cambiarNombre(&original, "c")` | Más verboso y expuesto a errores nulos |


## **Conclusiones**

- Si se quiere modificar un objeto dentro de una función, **hay que pasarlo por referencia o por puntero**.
- Pasar por **valor** genera una copia, y cualquier modificación se pierde al salir de la función.
- Usar **referencias** es más limpio y seguro cuando se quiere modificar directamente el objeto.
- Los **punteros** también permiten modificar el objeto original, pero requieren más cuidado con la gestión de memoria y punteros nulos.
