#### Tabla 
---

### **Explicación paso a paso (Fetch-Decode-Execute)**  

| Ciclo | PC (Inicio) | Instrucción | Decodificación | Ejecución (Cambios en A, D, M) |
|-------|------------|-------------|---------------|--------------------------------|
| 1     | 0         | `@5`        | A = 5         | A ← 5                          |
| 2     | 1         | `D=A`       | D = A         | D ← 5                          |
| 3     | 2         | `@10`       | A = 10        | A ← 10                         |
| 4     | 3         | `D=D+A`     | D = D + A     | D ← 5 + 10 = 15                |
| 5     | 4         | `@3`        | A = 3         | A ← 3                          |
| 6     | 5         | `D=D-A`     | D = D - A     | D ← 15 - 3 = 12                |
| 7     | 6         | `@10`       | A = 10        | A ← 10                         |
| 8     | 7         | `M=D`       | M[A] = D      | M[10] ← 12                     |

---

#### Evidencia

![image](https://github.com/user-attachments/assets/da74f6e4-c14b-43fc-a46a-96210ce09cce)
