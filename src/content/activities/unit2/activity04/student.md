
### **Código Ensamblador Hack**
```asm
// Simulación de int a = 10;
@16     // Dirección arbitraria para 'a'
D=10    // D = 10
M=D     // Memoria[16] = 10

// Simulación de int* p;
@17     // Dirección arbitraria para 'p'
D=16    // D = dirección de 'a'
M=D     // Memoria[17] = 16 (p apunta a a)

// Simulación de *p = 20;
@17     // Cargar dirección de p
D=M     // D = contenido de p (que es 16, la dirección de 'a')
@18     // Usamos un registro temporal para almacenar la dirección de 'a'
M=D     // Guardamos la dirección de 'a' en Memoria[18] (temporal)

// Modificación del valor de 'a' a través de 'p'
@18     // Recuperamos la dirección de 'a'
A=M     // A = Memoria[18] (que es 16, la dirección de 'a')
D=20    // D = 20
M=D     // Memoria[16] = 20
```

---

### **Tabla de Estados de Memoria**
| **Ciclo** | **Dirección (Memoria RAM)** | **Valor (Contenido)** | **Explicación** |
|-----------|----------------------------|----------------------|----------------|
| **Inicio** | `16 (a)` | `0` | `a` sin inicializar |
| | `17 (p)` | `0` | `p` sin inicializar |
| **Paso 1** | `16 (a)` | `10` | Se asigna `10` a `a` |
| **Paso 2** | `17 (p)` | `16` | `p` almacena la dirección de `a` |
| **Paso 3** | `18` | `16` | Dirección de `a` almacenada temporalmente |
| **Paso 4** | `16 (a)` | `20` | Se modifica `a` usando `p` |

---

### **Explicación**
1. Se guarda `10` en `a` (`Memoria[16]`).
2. Se guarda la dirección de `a` (`16`) en `p` (`Memoria[17]`).
3. Se almacena temporalmente la dirección de `a` en `Memoria[18]`.
4. Se usa `p` para modificar `a`, asignándole `20`.
