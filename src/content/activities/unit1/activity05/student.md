Esto es un programa simple en ensamblador Hack que suma dos números y almacena el resultado en la memoria.   

### Código en ensamblador Hack

``` asm
// Programa para sumar 5 + 3 y almacenar el resultado en la dirección de memoria 16
@5
D=A
@3
D=D+A
@16
M=D
```


### Tabla del Ciclo Fetch-Decode-Execute

| Ciclo | PC (Inicio) | Instrucción en Memoria | Decodificación | Ejecución (Cambios en Registros A, D y M) |
|-------|------------|----------------------|---------------|--------------------------------------|
| 1     | 0         | `@5`                 | A = 5         | A ← 5                               |
| 2     | 1         | `D=A`                 | D ← A        | D ← 5                               |
| 3     | 2         | `@3`                 | A = 3         | A ← 3                               |
| 4     | 3         | `D=D+A`               | D ← D + A    | D ← 5 + 3 = 8                       |
| 5     | 4         | `@16`                | A = 16        | A ← 16                              |
| 6     | 5         | `M=D`                 | M[A] ← D     | M[16] ← 8                           |

