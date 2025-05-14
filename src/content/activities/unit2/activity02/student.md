#### DESARROLLO

Al ejecutar el programa en el simulador, las variables `i` y `sum` se almacenan en direcciones de memoria específicas, que el sistema asigna automáticamente. Por lo general, en el simulador de Hack, las variables se guardan en las primeras posiciones de la RAM, como en la dirección `16` para `i` y `17` para `sum`.  

La diferencia entre la dirección de una variable y su contenido es que la dirección es el lugar en la memoria donde se almacena un valor, mientras que el contenido es el valor en sí. Por ejemplo, si `i` está en la dirección `16` y su contenido es `5`, significa que en la posición `16` de la RAM hay guardado un `5`.  

La condición `i <= 100` se implementa con las instrucciones:  
1. Se carga `i` en el registro `D`.  
2. Se resta `100` (`D = i - 100`).  
3. Se usa `D;JGT` para saltar a `END` si `i` es mayor que `100`, terminando el bucle.  

Así, el programa se repite mientras `i` sea menor o igual a `100`, sumando los valores uno por uno hasta llegar a `5050`, que es el resultado de la suma de los números del 1 al 100.
