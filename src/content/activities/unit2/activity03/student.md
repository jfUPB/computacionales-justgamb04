### **Código en Ensamblador Hack (versión con `for`)**  
```assembly
// Suma 1+...+100 usando un ciclo for

@sum
M=0         // sum = 0
@i
M=1         // i = 1

(LOOP)
    @i
    D=M     // D = i
    @101
    D=D-A   // D = i - 101
    @END
    D;JGE   // si i es mayor o igual a 101, salimos del bucle

    @i
    D=M     // D = i
    @sum
    M=M+D   // sum = sum + i

    @i
    M=M+1   // i = i + 1

    @LOOP
    0;JMP   // vuelve al inicio del bucle

(END)
@END
0;JMP       // Para que el programa no siga corriendo sin sentido
```

---

### **Comparación entre `while` y `for` en ensamblador**  
La verdad, en ensamblador no hay diferencia real entre `for` y `while`. O sea, en lenguajes como C++ o Python, un `for` ya te pone la inicialización, condición y aumento en una sola línea, pero en ensamblador igual toca escribirlas a mano.  

Lo que cambia es más bien la forma en que uno lo organiza en código, porque al final los dos hacen exactamente lo mismo. Con este ejercicio entendí que, aunque en código de alto nivel un `for` se ve más limpio y ordenado, en ensamblador es prácticamente igual que un `while`, solo que toca escribir cada paso uno mismo.
