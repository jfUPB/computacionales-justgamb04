Para que un programa OpenGL funcione en Windows, necesitas varias piezas que trabajan juntas.

Primero está `opengl32.lib`, una biblioteca que viene incluida con Windows. Esta sirve para crear el contexto inicial de OpenGL y acceder a funciones básicas de la versión 1.1. Sin embargo, como OpenGL ha avanzado mucho desde entonces, esto no es suficiente por sí solo.

Aquí entra `GLAD`, que es una biblioteca encargada de cargar las funciones modernas de OpenGL. Estas funciones no están disponibles directamente en Windows, sino que están en los drivers de la tarjeta gráfica. GLAD consulta esos drivers para obtener las funciones y que puedas usarlas en tu código. Para que funcione, necesitas incluir los archivos de encabezado y también agregar el archivo `glad.c` al proyecto.

Para que el programa tenga una ventana donde dibujar y pueda recibir entradas del teclado o el mouse, se usa `GLFW`. Esta biblioteca se encarga de todo eso, además de crear el contexto de OpenGL. Para usarla, necesitas enlazar el archivo `glfw3.lib` al proyecto y asegurarte de que el archivo `glfw3.dll` esté en el mismo lugar que el ejecutable, ya que es lo que realmente se usa en tiempo de ejecución.

Una no obligatoria es `GLM`, es una biblioteca de matemáticas que facilita trabajar con vectores y matrices, algo muy común en gráficos 3D. Solo necesitas los archivos de encabezado, no tiene archivos `.lib` ni `.dll`.

En resumen, GLFW crea la ventana y el contexto, opengl32.lib permite iniciarlo, GLAD carga las funciones modernas desde los drivers, y GLM te ayuda con las operaciones matemáticas. Todo esto se conecta para que puedas dibujar gráficos modernos en una ventana en tu PC.
