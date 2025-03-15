#### Codigo

``` asm
// Inicializar el contador en 1
@1
D=A
@i
M=D

// Inicializar la suma en 0
@sum
M=0

// Inicio del ciclo
(LOOP)
    // Cargar la suma actual en D
    @sum
    D=M

    // Sumar el valor de i
    @i
    D=D+M

    // Guardar la nueva suma
    @sum
    M=D

    // Incrementar i en 1
    @i
    M=M+1

    // Verificar si i > 5 (salir del bucle)
    @i
    D=M
    @6
    D=D-A  // Si i - 6 < 0, sigue en el bucle

    @LOOP
    D;JLT  // Si i < 6, repetir el ciclo

// Guardar el resultado en la dirección de memoria 12
@sum
D=M
@12
M=D

// Bucle infinito para detener el programa
(END)
@END
0;JMP
```


### TABLA (No me deja tomar captura)

| Ciclo | PC  | Instrucción  | Decodificación | Ejecución (Cambios en A, D, M) |
|-------|----|-------------|---------------|--------------------------------|
| 1     | 0  | `@1`        | A = 1         | A ← 1                          |
| 2     | 1  | `D=A`       | D = A         | D ← 1                          |
| 3     | 2  | `@i`        | A = i         | A ← Dirección de `i`           |
| 4     | 3  | `M=D`       | M[A] = D      | M[i] ← 1                       |
| 5     | 4  | `@sum`      | A = sum       | A ← Dirección de `sum`         |
| 6     | 5  | `M=0`       | M[A] = 0      | M[sum] ← 0                     |
| 7     | 6  | `(LOOP)`    | -             | -                               |
| 8     | 7  | `@sum`      | A = sum       | A ← Dirección de `sum`         |
| 9     | 8  | `D=M`       | D = M[A]      | D ← M[sum]                     |
| 10    | 9  | `@i`        | A = i         | A ← Dirección de `i`           |
| 11    | 10 | `D=D+M`     | D = D + M[A]  | D ← M[sum] + M[i]              |
| 12    | 11 | `@sum`      | A = sum       | A ← Dirección de `sum`         |
| 13    | 12 | `M=D`       | M[A] = D      | M[sum] ← Nueva suma            |
| 14    | 13 | `@i`        | A = i         | A ← Dirección de `i`           |
| 15    | 14 | `M=M+1`     | M[A] = M[A]+1 | M[i] ← M[i] + 1                |
| 16    | 15 | `@i`        | A = i         | A ← Dirección de `i`           |
| 17    | 16 | `D=M`       | D = M[A]      | D ← M[i]                       |
| 18    | 17 | `@6`        | A = 6         | A ← 6                          |
| 19    | 18 | `D=D-A`     | D = D - A     | D ← M[i] - 6                   |
| 20    | 19 | `@LOOP`     | A = LOOP      | A ← Dirección de LOOP          |
| 21    | 20 | `D;JLT`     | Si D < 0, salta | PC ← LOOP si i < 6             |
| ...   | .. | (Se repite el ciclo hasta que `i = 6`) | - | - |
| 22    | XX | `@sum`      | A = sum       | A ← Dirección de `sum`         |
| 23    | XX | `D=M`       | D = M[A]      | D ← M[sum] (que ahora es 15)   |
| 24    | XX | `@12`       | A = 12        | A ← 12                         |
| 25    | XX | `M=D`       | M[A] = D      | M[12] ← 15                     |
| 26    | XX | `(END)`     | -             | -                               |
| 27    | XX | `@END`      | A = END       | A ← END                        |
| 28    | XX | `0;JMP`     | Salta a END   | PC ← END (bucle infinito)      |

---

