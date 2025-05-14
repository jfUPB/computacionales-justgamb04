#### 1. Nivel de comodidad 

   Realmente no estoy del todo cómodo. Entiendo los conceptos básicos, como el ciclo Fetch-Decode-Execute y cómo funciona la memoria, pero todavía me cuesta escribir código sin errores y optimizarlo.  

   Por ejemplo, en la actividad donde debía mover una línea con el teclado, tuve problemas para hacer que la línea respondiera correctamente a las teclas de flecha. Sabía que la dirección de memoria 24576 (`@KBD`) almacenaba el código ASCII de la tecla presionada, pero no tenía claro cómo comparar ese valor y hacer que el programa ejecutara el movimiento sin errores. Al final, logré hacerlo con prueba y error, pero fue más difícil de lo que esperaba.  

#### 2. Desafios de la unidad 

   - **Memoria y direcciones**:
     Me tomó un tiempo entender cómo funciona la memoria en Hack. Al principio, intenté modificar `@SCREEN` directamente sin considerar que cada dirección almacena 16 bits, lo que hizo que el dibujo no saliera como quería.  

   - **Saltos condicionales y bucles**:
     En la actividad de sumar del 1 al 5, tenía problemas porque mi bucle no terminaba correctamente. A veces entraba en un bucle infinito, y otras veces el resultado no se guardaba bien en memoria. No estaba usando bien las instrucciones de comparación (`D;JGT`, `D;JEQ`, etc.), lo que hacía que el código no ejecutara la lógica correctamente.  

   - **Uso de etiquetas**:
     Me confundía con el uso de etiquetas como `@LOOP` porque no siempre las declaraba en la parte correcta del código. Por ejemplo, en un ejercicio intenté hacer un salto a `@END`, pero la etiqueta no estaba definida, lo que me daba errores en el simulador.  

#### 3. Estrategias utilizadas para comprender mejor  

   ##### - Probar el código paso a paso en el simulador: 
   Esto me ayudó mucho a ver qué valores se cargaban en los registros y en la memoria en cada ciclo. Cuando algo fallaba, podía ver en qué parte del proceso estaba el error.  

   ##### - Comparar con ejemplos de código: 
   Revisé los códigos de ejemplo del material de estudio y traté de modificarlos para entender cómo funcionaban. Esto fue especialmente útil para aprender a usar `@SCREEN` y `@KBD` correctamente.  

   ##### - Dividir los problemas en partes más pequeñas: 
   En la actividad de la línea en la pantalla, primero logré dibujar un solo punto, luego lo expandí a una línea de 16 píxeles, y después agregué el movimiento con el teclado. Hacerlo paso a paso me permitió entender cada parte antes de juntar todo.

   ##### - Uso de inteligencia artificial:
   En las actividades utilizaba inteligencia artifical para explicarme ciertos problemas que tuve a lo largo de la unidad 
      

En general, aunque al principio el lenguaje ensamblador Hack me pareció difícil, con práctica fui entendiendo mejor cómo funcionan las instrucciones y cómo manipular la memoria. Aún me falta mejorar en optimización y en hacer código más eficiente, pero ya me siento más cómodo con los conceptos básicos.
