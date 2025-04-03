
### **Tabla del Ciclo Fetch-Decode-Execute**
| **Paso** | **PC** | **Instrucción** | **Decodificación** | **Ejecución (Cambios en A, D, M)** |
|---------|------|----------------|----------------|--------------------------------|
| 1       | 0    | `@16384`       | A = 16384     | A ← 16384                      |
| 2       | 1    | `D=A`          | D = A         | D ← 16384                      |
| 3       | 2    | `@0`           | A = 0         | A ← 0                          |
| 4       | 3    | `M=D`          | M[A] = D      | M[0] ← 16384 (Guardar en RAM[0]) |
| 5       | 4    | `@16384`       | A = 16384     | A ← 16384                      |
| 6       | 5    | `M=-1`         | M[A] = -1     | M[16384] ← 1111111111111111 (Dibuja la línea) |
| 7       | 6    | `@5`           | A = 5         | A ← 5                          |
| 8       | 7    | `0;JMP`        | Salto incondicional | PC ← 5 (Bucle infinito) |


![image](https://github.com/user-attachments/assets/7309efda-59c0-4b2c-a099-f70048d84150)  

![image](https://github.com/user-attachments/assets/1e8d9436-584d-4821-8e5c-e668732e6a56)
