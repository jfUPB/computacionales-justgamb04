## **Código en C++**

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

    // Método para imprimir valores
    void imprimir() {
        cout << "Punto " << name << "(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    // Objeto original
    Punto original("original", 70, 80);
    original.imprimir();

    // Puntero al objeto original
    Punto* p = &original;

    // Copia del objeto
    Punto copia = original;
    copia.name = "copia";
    copia.x = 100;
    copia.y = 200;
    copia.imprimir();
    original.imprimir();

    // Cambios a través del puntero
    p->name = "p";
    p->x = 300;
    p->y = 400;
    p->imprimir();
    original.imprimir();

    return 0;
}
```

---

## **Código en C#**

```csharp
using System;

public class Punto
{
    public int x;
    public int y;
    public string name;

    public Punto(string _name, int _x, int _y)
    {
        name = _name;
        x = _x;
        y = _y;
        Console.WriteLine($"Constructor: Punto {name}({x}, {y}) creado.");
    }

    public void Imprimir()
    {
        Console.WriteLine($"Punto {name}({x}, {y})");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Punto original = new Punto("original", 70, 80);
        original.Imprimir();

        Punto copia = original;
        copia.name = "copia";
        copia.x = 100;
        copia.y = 200;
        copia.Imprimir();
        original.Imprimir();
    }
}
```

## **Explicación y Comparación**

### **¿Qué ocurre al copiar un objeto en C++?**

- Al ejecutar `Punto copia = original;`, se realiza una **copia profunda** del objeto, utilizando el constructor de copia por defecto.
- Se crea un nuevo objeto en una **dirección de memoria diferente**.
- Modificar `copia` **no afecta** a `original`, lo que significa que son **copias independientes**.
- En este caso también se demuestra que un puntero como `p` sí afecta al objeto original, ya que apunta directamente a su dirección de memoria.

### **¿Qué ocurre al copiar un objeto en C#?**

- En C#, las clases son **tipos de referencia**, por lo tanto `Punto copia = original;` simplemente copia la **referencia** al mismo objeto.
- Tanto `copia` como `original` apuntan al **mismo objeto en memoria**.
- Cualquier cambio en `copia` se verá reflejado en `original`.

## **¿Qué es copia en C++ y en C#?**

| Lenguaje | ¿Qué se copia?                        | ¿Son independientes?              |
|----------|---------------------------------------|-----------------------------------|
| **C++**  | Se copia el contenido del objeto      | **Sí**, son objetos distintos     |
| **C#**   | Se copia la referencia al objeto      | **No**, apuntan al mismo objeto   |

## **Conclusión**

- En **C++**, las copias de objetos se comportan como **copias reales** de los datos. Puedes tener dos objetos iguales pero separados.
- En **C#**, copiar un objeto de clase significa **copiar una referencia**, por lo que ambos nombres apuntan al mismo espacio en memoria.
- Si se quisiera en C# tener una copia independiente, se debe implementar manualmente una copia profunda (`DeepCopy`) o clonar el objeto.
