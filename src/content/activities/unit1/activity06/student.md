#### ¿Qué es el direccionamiento directo? ¿Cómo se usa en el lenguaje ensamblador Hack?  
   El direccionamiento directo es un modo de acceso a memoria en el que se especifica directamente la dirección donde se encuentra el dato que se quiere leer o modificar. En el lenguaje ensamblador Hack, se utiliza la instrucción `@dirección` para cargar una dirección en el registro `A`, y luego `M` se usa para referirse al valor almacenado en esa dirección.
   
   ```assembly
   @5      // Cargar la dirección 5 en A
   D=M     // Cargar en D el valor almacenado en la dirección 5
   ```

#### ¿Qué significa `M=D` en lenguaje ensamblador Hack? ¿Y `D=M`? 
   - `M=D` significa que el valor almacenado en el registro `D` se copia en la dirección de memoria actualmente apuntada por `A`.  
   - `D=M` significa que el valor almacenado en la dirección de memoria actualmente apuntada por `A` se carga en el registro `D`.  
   ```assembly
   @10     // Cargar la dirección 10 en A
   D=M     // Guardar en D el valor almacenado en la dirección 10
   @20     // Cargar la dirección 20 en A
   M=D     // Guardar en la dirección 20 el valor de D (copiado de la dirección 10)
   ```

#### Explicación del concepto de "puntero" en el contexto de la memoria  
   En el contexto de la memoria, un **puntero** es una variable que almacena la dirección de otra ubicación en memoria. En ensamblador Hack, un puntero se puede usar para acceder a valores de memoria de manera indirecta.  

   ##### Ejemplo
   Supongamos que queremos almacenar un número en una dirección referenciada por un puntero almacenado en la dirección 2.  

   ```assembly
   @2      // Cargar la dirección del puntero en A
   D=M     // Cargar en D la dirección a la que apunta el puntero
   @D      // Cargar esa dirección en A
   M=7     // Almacenar el número 7 en la dirección apuntada por el puntero
   ```

   En este caso:  
   - La dirección 2 almacena otra dirección, digamos la 10.  
   - `D=M` carga la dirección almacenada en la posición 2 (que es 10).  
   - `@D` carga esa dirección en `A`, y `M=7` almacena el número 7 en la dirección 10.  

### Código en ensamblador Hack que ilustra el concepto de puntero
Este código almacena el valor `25` en la dirección de memoria apuntada por la dirección `3` (es decir, si en `RAM[3]` está el valor `12`, entonces `RAM[12]` recibirá `25`).

```assembly
@3      // Cargar la dirección del puntero en A
D=M     // Cargar en D la dirección a la que apunta el puntero
@D      // Cargar en A la dirección contenida en D
M=25    // Guardar el valor 25 en la dirección apuntada por el puntero
```
