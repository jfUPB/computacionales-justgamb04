### **Tabla detallada para la ejecución**

| **Paso** | **PC (Contador de Programa)** | **Instrucción** | **Decodificación** | **Ejecución (Cambios en A, D, M)** |
|---------|------|----------------|----------------|--------------------------------|
| 1       | 0    | `@16384`       | A = 16384     | A ← 16384                      |
| 2       | 1    | `D=A`          | D = A         | D ← 16384                      |
| 3       | 2    | `@0`           | A = 0         | A ← 0                          |
| 4       | 3    | `M=D`          | M[A] = D      | M[0] ← 16384 (Guardar en RAM[0]) |
| 5       | 4    | `@16384`       | A = 16384     | A ← 16384                      |
| 6       | 5    | `A=M`          | A = M[A]      | A ← 16384 (Cargar dirección guardada en RAM) |
| 7       | 6    | `M=1`          | M[A] = 1      | M[16384] ← 1 (Encender primer bit de pantalla) |
| 8       | 7    | `@5`           | A = 5         | A ← 5                          |
| 9       | 8    | `0;JMP`        | Salto incondicional | PC ← 5 (Bucle infinito) |



![image](https://github.com/user-attachments/assets/a711fd46-81b2-4562-87b9-f2e56261e14d)  
![image](https://github.com/user-attachments/assets/c6b398a5-3e74-4df1-a36d-42f5a9df172a)
