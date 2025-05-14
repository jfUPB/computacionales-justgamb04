### **Análisis de errores y debugging**  

#### **Errores que cometí en la fase APPLY**  

1. **Error al manejar la memoria de la pantalla**  
   En el ejercicio donde tenía que dibujar un punto en la pantalla, traté de escribir `M=1` en `@SCREEN`, pero no apareció nada. No sabía que cada dirección en `SCREEN` representa 16 píxeles, y yo solo quería modificar uno.  

   **Cómo lo arreglé:**  
   Probé el código en el simulador paso a paso y vi que estaba cambiando todos los 16 bits en lugar de solo el primero. Busqué información y entendí que debía modificar solo el bit necesario.  

   **Qué aprendí:**  
   No basta con saber que `@SCREEN` es la memoria de la pantalla, también hay que entender cómo se organizan los datos en cada dirección.  

   **Cómo evitarlo en el futuro:**  
   Antes de escribir en memoria, revisaré bien cómo funciona la estructura de datos que estoy modificando.  

2. **Error en los saltos condicionales**  
   En la actividad donde debía comparar un número en memoria con 10, mi código siempre ponía el mismo resultado, sin importar el valor que tenía la memoria.  

   **Cómo lo arreglé:**  
   Al revisar paso a paso en el simulador, me di cuenta de que `D` no tenía el valor correcto antes de hacer la comparación. Lo corregí asegurándome de cargar bien `D` antes de restarle 10.  

   **Qué aprendí:**  
   Antes de hacer un salto, debo asegurarme de que los valores en los registros son los correctos, porque cualquier error puede hacer que el programa no funcione bien.  

   **Cómo evitarlo en el futuro:**  
   Voy a usar más el simulador para verificar los valores antes de hacer comparaciones.  

#### **Importancia del debugging**  

El debugging es clave para que un programa funcione bien. En Hack, un error pequeño puede hacer que todo falle, así que es importante revisar cada instrucción.  

#### **Técnicas de debugging que usé**  

- **Ejecutar paso a paso** para ver qué hace cada línea de código.  
- **Revisar los valores en los registros** para asegurarme de que las operaciones sean correctas.  
- **Probar partes del código por separado** en lugar de correr todo junto y esperar que funcione.  

Gracias a esto, pude encontrar y corregir mis errores sin perder demasiado tiempo.
