## **Conceptos de la unidad**
### 1. **Punteros**
   - Un **puntero** es una variable que almacena la **dirección de memoria** de otra variable.
   - **Ejemplo en C++:**
     ```cpp
     int a = 10;
     int* p = &a; // p almacena la dirección de a
     *p = 20;     // Modifica el valor de a a 20
     ```
   - **Ejemplo en Ensamblador Hack:**
     ```asm
     @a
     D=M    // Cargar el valor de 'a'
     @p
     M=D    // Guardar en 'p' la dirección de 'a'
     ```

### 2. **Lectura y Escritura con Punteros**
   - Los punteros permiten **leer y modificar** datos almacenados en una dirección de memoria.
   - **Ejemplo en C++:**
     ```cpp
     int a = 10, b = 5;
     int *p = &a;
     b = *p; // b ahora vale 10
     ```
   - **Ejemplo en Ensamblador Hack:**
     ```asm
     @a
     D=M   // Cargar el valor de 'a'
     @p
     M=D   // Guardar dirección en 'p'

     @p
     A=M   // Acceder a la dirección almacenada en 'p'
     D=M   // Obtener el valor
     @b
     M=D   // Asignar a 'b'
     ```

### 3. **Arreglos en Ensamblador**
   - Un **arreglo** es una secuencia de datos en memoria.
   - **Ejemplo en C++:**
     ```cpp
     int arr[] = {1,2,3,4,5};
     int sum = 0;
     for (int i = 0; i < 5; i++) {
         sum += arr[i];
     }
     ```
   - **Ejemplo en Ensamblador Hack:**
     ```asm
     @16
     D=A
     @i
     M=D  // i = dirección base del arreglo

     (SUM_LOOP)
     @i
     D=M
     @21  // Dirección límite del arreglo (5 elementos)
     D=D-A
     @END_SUM
     D;JGE

     @i
     A=M
     D=M
     @sum
     M=M+D  // sum += arr[i]

     @i
     M=M+1  // i++
     @SUM_LOOP
     0;JMP

     (END_SUM)
     ```

### 4. **Lenguaje de Máquina y Ensamblador**
   - El **lenguaje de máquina** usa instrucciones binarias, mientras que el **ensamblador** es un nivel más alto y fácil de leer.
   - **Ejemplo de código en lenguaje de máquina (Hack):**
     ```
     0100000000000000
     1110110000010000
     ```
   - **Su equivalente en Ensamblador:**
     ```asm
     @0
     D=A
     ```
### 5. **Condiciones y Saltos en Ensamblador**
   - Se pueden usar comparaciones y saltos condicionales (`JEQ`, `JGT`, `JLT`) para tomar decisiones.
   - **Ejemplo en C++:**
     ```cpp
     if (x == 5) {
         y = 10;
     }
     ```
   - **Ejemplo en Ensamblador Hack:**
     ```asm
     @x
     D=M
     @5
     D=D-A
     @SET_Y
     D;JEQ   // Si x == 5, saltar a SET_Y

     (SET_Y)
     @10
     D=A
     @y
     M=D     // y = 10
     ```

### 6. **Funciones en Ensamblador**
   - En **C++**, una función recibe parámetros y ejecuta código.
   - **Ejemplo en C++:**
     ```cpp
     void pantalla(int valor) {
         if (valor == 'p') {
             // Pinta la pantalla
         } else if (valor == 'b') {
             // Borra la pantalla
         }
     }
     ```
   - **Ejemplo en Ensamblador Hack:**
     ```asm
     (pantalla)
     @KBD
     D=M
     @80
     D=D-A
     @PINTAR
     D;JEQ
     @66
     D=D+A
     @BORRAR
     D;JEQ
     @RETORNO
     0;JMP
     ```
