## Desarrollo

```assembly
// Inicializar la dirección base del arreglo en memoria
@16
D=A
@arr
M=D  // arr = 16

// Inicializar sum en 0
@sum
M=0

// Inicializar j en 0
@j
M=0

(LOOP)
    // Comprobar si j < 10
    @j
    D=M
    @10
    D=D-A
    @END
    D;JGE  // Si j >= 10, salir del bucle

    // Obtener arr[j]
    @arr
    D=M
    @j
    A=D+M  // Dirección de arr[j]
    D=M    // Guardar arr[j] en D

    // Sumar arr[j] a sum
    @sum
    M=M+D

    // Incrementar j
    @j
    M=M+1

    // Volver al inicio del bucle
    @LOOP
    0;JMP

(END)
    @END
    0;JMP  // Bucle infinito para detener el programa
```

---

### **Tabla del Código Ensamblador**  

| **Instrucción** | **Comentario** |
|---------------|---------------|
| `@16`  | Cargar la dirección base del arreglo. |
| `D=A`  | Guardar la dirección en D. |
| `@arr` | Ir a la variable arr. |
| `M=D`  | Guardar la dirección base en arr. |
| `@sum` | Ir a la variable sum. |
| `M=0`  | Inicializar sum en 0. |
| `@j`   | Ir a la variable j. |
| `M=0`  | Inicializar j en 0. |
| `(LOOP)` | Inicio del bucle. |
| `@j`   | Cargar j. |
| `D=M`  | Guardar su valor en D. |
| `@10`  | Cargar el límite del bucle. |
| `D=D-A` | Restar j - 10. |
| `@END` | Ir a END si j >= 10. |
| `D;JGE` | Comparar y saltar si es necesario. |
| `@arr` | Cargar la dirección base del arreglo. |
| `D=M`  | Guardar la dirección en D. |
| `@j`   | Cargar j. |
| `A=D+M` | Acceder a la dirección arr[j]. |
| `D=M`  | Cargar el valor de arr[j] en D. |
| `@sum` | Ir a sum. |
| `M=M+D` | Acumular sum = sum + arr[j]. |
| `@j`   | Cargar j. |
| `M=M+1` | Incrementar j++. |
| `@LOOP` | Volver al inicio del bucle. |
| `0;JMP` | Saltar a LOOP. |
| `(END)` | Punto de parada. |
| `@END` | Bucle infinito para detener ejecución. |
| `0;JMP` | Mantener el programa en END. |

---

### **Explicación**  

El código inicializa el arreglo en la memoria desde la dirección 16, con `arr = 16`. Luego, establece las variables `sum = 0` y `j = 0`.  

El bucle (`LOOP`) recorre el arreglo, accediendo a cada posición con `arr[j]` y sumando su valor a `sum`.  

Para verificar la condición `j < 10`, el programa usa `D=D-A` y salta a `(END)` si `j >= 10`. Si no, sigue sumando y aumentando `j`, repitiendo el proceso hasta llegar a 10.  

Cuando se alcanza el final, el programa entra en un bucle infinito para detenerse.
