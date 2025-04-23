Al ejecutar el programa en modo depuración con un breakpoint en la línea `Punto p(10, 20);`, observé lo siguiente:

- En la ventana Locals, los valores de `x = 10` y `y = 20` se mostraron correctamente.
- Usando la herramienta Memory > Memory 1, escribí `&p` para ver la memoria del objeto.
- En la memoria aparecieron los bytes en orden: `0a 00 00 00 14 00 00 00`

Estos valores corresponden a:

- `0a` (hex) → `10` (decimal) → valor de `x`
- `14` (hex) → `20` (decimal) → valor de `y`

Los bytes están almacenados en orden little-endian, donde el byte menos significativo se guarda primero.

**¿Qué pasaría si fuera big-endian?**

En una arquitectura big-endian, los mismos valores estarían almacenados como:

`00 00 00 0a 00 00 00 14`

Es decir, el byte más significativo va primero.

**Parte 2 – Respuestas de entrega**

**¿Cuál es la diferencia entre un constructor y un destructor en C++?**

El constructor se ejecuta al crear un objeto y se usa para inicializar sus atributos.  
El destructor se ejecuta automáticamente cuando el objeto sale de su ámbito o se destruye, y sirve para liberar recursos o hacer limpieza.

**¿Cuál es la diferencia entre un objeto y una clase en C++?**

Una clase es el molde o plantilla para crear objetos, define atributos y comportamientos.  
Un objeto es una instancia real de una clase, con sus propios valores de atributos.

**¿Qué diferencia notas entre el objeto Punto en C++ y C#?**

En C++, `p` es un objeto real alocado en el stack. Su creación y destrucción es inmediata, y el destructor se llama tan pronto termina `main()`.  
En C#, `p` es una referencia a un objeto creado en el heap. Su destrucción no es inmediata, sino que depende del recolector de basura (GC), así que el destructor puede no ejecutarse de inmediato (o nunca si no es forzado).

**¿Qué es `p` en C++ y qué es `p` en C#?**

En C++, `p` es un objeto completo (no una referencia).  
En C#, `p` es una referencia a un objeto en el heap.

**¿En qué parte de memoria se almacena `p` en C++ y en C#?**

En C++, `p` está almacenado directamente en el stack.  
En C#, la referencia `p` está en el stack, pero el objeto real está en el heap.

- Variable `p` con dirección de memoria en "Locals".  
- Valores de `x = 10` y `y = 20`.  
- Ventana de "Memory 1" mostrando `0a 00 00 00 14 00 00 00`.

**¿Qué observaste con el depurador acerca de `p`?**

`p` está almacenado como una sola estructura de datos contigua en la memoria del stack.  
Cada uno de sus atributos (`x` e `y`) ocupa 4 bytes.  
En memoria se ve claramente que está en formato little-endian.  
El orden de creación y destrucción está bien definido y controlado por el programador (no hay recolector de basura).

**¿Qué es un objeto en C++?**

Un objeto en C++ es una instancia concreta de una clase que puede estar almacenada directamente en memoria (como en el stack) y que posee sus propios datos, organizados de forma contigua. En C++, el programador tiene control total sobre la creación, almacenamiento y destrucción del objeto.
