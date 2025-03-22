### **Código Ensamblador Hack**  
```asm
// Simulación de int a = 10;
@16     // Dirección arbitraria para 'a'
D=10    // D = 10
M=D     // Memoria[16] = 10

// Simulación de int b = 5;
@17     // Dirección arbitraria para 'b'
D=5     // D = 5
M=D     // Memoria[17] = 5

// Simulación de int* p;
@18     // Dirección arbitraria para 'p'
D=16    // D = dirección de 'a'
M=D     // Memoria[18] = 16 (p apunta a a)

// Simulación de b = *p;
@18     // Cargar dirección de p
D=M     // D = contenido de p (que es 16, la dirección de 'a')
A=D     // A = 16 (la dirección de 'a')
D=M     // D = contenido de 'a' (que es 10)
@17     // Cargar dirección de 'b'
M=D     // Memoria[17] = 10 (b ahora es 10)
```


### **Tabla de Estados de Memoria**
| **Ciclo** | **Dirección (Memoria RAM)** | **Valor (Contenido)** | **Explicación** |
|-----------|----------------------------|----------------------|----------------|
| **Inicio** | `16 (a)` | `0` | `a` sin inicializar |
| | `17 (b)` | `0` | `b` sin inicializar |
| | `18 (p)` | `0` | `p` sin inicializar |
| **Paso 1** | `16 (a)` | `10` | Se asigna `10` a `a` |
| **Paso 2** | `17 (b)` | `5` | Se asigna `5` a `b` |
| **Paso 3** | `18 (p)` | `16` | `p` almacena la dirección de `a` |
| **Paso 4** | `17 (b)` | `10` | `b` cambia a `10` usando `p` |

---

### **Explicación**
1. Se asigna `10` a `a` (`Memoria[16]`).
2. Se asigna `5` a `b` (`Memoria[17]`).
3. `p` almacena la dirección de `a` (`Memoria[18] = 16`).
4. Se usa `p` para leer `a` y asignar su valor (`10`) a `b`.
