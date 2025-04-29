En esta unidad aprendí a manejar clases y objetos en C++, entendiendo sus componentes principales como atributos, métodos, constructores, destructores y la diferencia entre miembros estáticos y de instancia. También comprendí cómo funciona el paso de parámetros por valor y por referencia, así como la importancia de saber en qué parte de la memoria se almacena cada tipo de objeto: el stack o el heap.

Un ejemplo que me ayudó mucho fue cuando creé un objeto dentro de un bloque `{}` y vi cómo se destruía automáticamente al salir del bloque, mientras que un objeto creado con `new` solo se eliminaba cuando usaba `delete`.

También aprendí que las variables estáticas como `Contador::total` no pertenecen a cada instancia, sino que son compartidas por toda la clase, y se almacenan en un área distinta de memoria (segmento de datos estáticos).

**¿Cuáles fueron los conceptos más desafiantes de la unidad? ¿Por qué?**

Lo más difícil fue entender la memoria dinámica: saber qué es lo que realmente se guarda en el stack y qué en el heap. Al principio, pensaba que el puntero `p = new Objeto()` estaba completamente en el heap, pero luego entendí que el puntero como tal está en el stack, y el objeto al que apunta está en el heap.

También me costó un poco identificar cuándo se llamaba al destructor, especialmente en objetos creados dinámicamente.

**¿Qué estrategias utilicé para comprender esos conceptos desafiantes?**

Principalmente hice pruebas con Visual Studio en modo depuración. Usé breakpoints y la ventana de memoria para ver direcciones y valores en tiempo real. También consulté foros y escribí muchos comentarios en el código para explicarme a mí mismo cada línea. Otra estrategia fue dibujar esquemas de cómo se organiza la memoria (stack y heap).

**¿Qué estrategias me resultaron más efectivas?**

La más efectiva fue usar el depurador para seguir paso a paso lo que pasaba en memoria. Eso me ayudó a entender mucho mejor cómo se comportaban los objetos al entrar y salir de bloques, y qué pasaba con la memoria dinámica.

Voy a seguir usando el depurador en todos los ejercicios. Además, por cada tema nuevo que vea, haré un esquema a mano que muestre cómo se distribuye la memoria. También voy a practicar con más ejercicios cortos de punteros, referencias y manejo de memoria. Por último, si me bloqueo con un concepto, buscaré una monitoría o ayuda antes de dejarlo pasar, para no acumular dudas.
