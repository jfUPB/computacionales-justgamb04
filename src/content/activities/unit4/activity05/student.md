### ¿Qué aspectos de la implementación de la cola te resultaron más fáciles? ¿Por qué?

Lo que me resultó más fácil fue entender el concepto general de la cola y su funcionamiento como estructura FIFO. Desde un inicio tuve clara la idea de insertar elementos al final y eliminarlos desde el frente, gracias a analogías cotidianas como una fila de espera. Además, como ya había trabajado con listas enlazadas en otras actividades, crear la estructura del nodo y vincular elementos no me costó tanto. Tener esa base previa ayudó a que esta parte fluyera con naturalidad.

### ¿Qué parte te pareció más difícil o te tomó más tiempo? ¿Cómo la resolviste?

La parte más difícil fue manejar los casos especiales, como cuando la cola está vacía o cuando se elimina el último elemento. Me tomó tiempo entender que si no actualizaba correctamente los punteros `front` y `rear`, podía terminar con referencias inválidas. Al principio, al hacer `dequeue()`, no controlaba bien cuando la cola quedaba vacía y me salían errores al hacer operaciones después. Lo resolví leyendo cuidadosamente el flujo del código y haciendo pruebas con diferentes secuencias de inserciones y eliminaciones para ver cómo se comportaban los punteros.

### Si pudieras repetir esta actividad, ¿qué harías diferente para mejorar tu desempeño?

Si pudiera repetir esta actividad, empezaría por hacer un diagrama a mano antes de programar. Me di cuenta de que cuando no lo hice, me costaba imaginar cómo se conectaban los nodos y cómo afectaba cada operación a la estructura. También me organizaría mejor para no dejar el trabajo para el último momento, ya que eso me generó presión innecesaria. Además, probaría más casos límite desde el principio para detectar errores antes de avanzar mucho con la implementación.

### ¿Cómo se relaciona lo que aprendiste en esta unidad con otras áreas de la programación o de tu carrera?

Esta unidad se relaciona bastante con estructuras de datos, que son clave para resolver problemas de lógica, optimizar recursos y organizar la información de forma eficiente. Además, como estudio Ingeniería de Diseño de Entretenimiento Digital, este tipo de estructuras es útil para crear sistemas de juego, colas de eventos, procesamiento de tareas o animaciones. Entender cómo funcionan internamente también me prepara para usar estructuras complejas en motores gráficos o cuando se trabaje con redes o inteligencia artificial.

### ¿Qué aprendizajes de esta unidad te servirán en futuros proyectos?

Aprendí a pensar de forma más estructurada y a considerar casos especiales desde el diseño. También fortalecí mi habilidad para trabajar con punteros y memoria dinámica, lo cual es clave en C++ y en el manejo de estructuras personalizadas. Estos aprendizajes me servirán en proyectos donde necesite diseñar lógicas internas específicas, como sistemas de interacción entre personajes, gestión de eventos en tiempo real, o simulaciones. Saber implementar estas estructuras me da más control y comprensión cuando use herramientas más avanzadas.

