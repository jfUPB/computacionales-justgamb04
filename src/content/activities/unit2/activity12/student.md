## **1. Condicionales**
### **Código en C++**
```cpp
int x = 5;
int y;

if (x > 3) {
    y = 10;
} else {
    y = 0;
}
```

### **Código en Ensamblador Hack**
```asm
@x
D=M      // D = x
@3
D=D-A    // D = x - 3
@ELSE
D;JLE    // Si x <= 3, salta a ELSE

@10
D=A
@y
M=D      // y = 10
@END
0;JMP    // Salta al final

(ELSE)
@0
D=A
@y
M=D      // y = 0

(END)
```

## **2. Ciclo While**
### **Código en C++**
```cpp
int x = 5;
while (x > 0) {
    x = x - 1;
}
```

### **Código en Ensamblador Hack**
```asm
(LOOP)
@x
D=M
@END
D;JLE    // Si x <= 0, salir del loop

@x
M=M-1    // x = x - 1
@LOOP
0;JMP    // Repetir

(END)
```

## **3. Ciclo For**
### **Código en C++**
```cpp
for (int i = 0; i < 5; i++) {
    // Hacer algo (ej: incrementar una variable)
}
```

### **Código en Ensamblador Hack**
```asm
@0
D=A
@i
M=D     // i = 0

(LOOP)
@i
D=M
@5
D=D-A
@END
D;JGE   // Si i >= 5, salir del loop

@i
M=M+1   // i++
@LOOP
0;JMP   // Repetir

(END)
```

## **4. Escritura de Variables por Medio de Punteros**
### **Código en C++**
```cpp
int a = 10;
int *p = &a;
*p = 20;  // Modifica a
```

### **Código en Ensamblador Hack**
```asm
@10
D=A
@a
M=D     // a = 10

@a
D=A
@p
M=D     // p almacena la dirección de a

@20
D=A
@p
A=M    // Accede a la dirección guardada en p
M=D    // *p = 20
```

## **5. Lectura de Variables por Medio de Punteros**
### **Código en C++**
```cpp
int a = 10;
int *p = &a;
int b = *p;  // Lee el valor de a
```

### **Código en Ensamblador Hack**
```asm
@10
D=A
@a
M=D    // a = 10

@a
D=A
@p
M=D    // p almacena la dirección de a

@p
A=M
D=M   // D = *p (valor de a)
@b
M=D   // b = *p
```

## **6. Manipulación de un Arreglo por Medio de Punteros**
### **Código en C++**
```cpp
int arr[] = {1,2,3,4,5};
int *p = arr;
*(p + 2) = 10;  // Modifica arr[2]
```

### **Código en Ensamblador Hack**
```asm
@1
D=A
@16
M=D    // arr[0] = 1

@2
D=A
@17
M=D    // arr[1] = 2

@3
D=A
@18
M=D    // arr[2] = 3

@4
D=A
@19
M=D    // arr[3] = 4

@5
D=A
@20
M=D    // arr[4] = 5

@16
D=A
@p
M=D    // p apunta al inicio del arreglo

@p
D=M
@2
D=D+A  // Dirección de arr[2]
A=D
M=10   // *(p + 2) = 10
```

## **7. Llamado a Funciones con Parámetros**
### **Código en C++**
```cpp
void setX(int valor) {
    x = valor;
}

setX(5);
```

### **Código en Ensamblador Hack**
```asm
@5
D=A
@valor
M=D     // Guardar 5 en 'valor'

@setX
0;JMP   // Llamar función

(RETURN)
@END
0;JMP   // Fin del programa

(setX)
@valor
D=M
@x
M=D     // x = valor
@RETURN
0;JMP   // Regresar
```

## **8. Llamado a Funciones con Retorno de Parámetros**
### **Código en C++**
```cpp
int suma(int a, int b) {
    return a + b;
}

int resultado = suma(2, 3);
```

### **Código en Ensamblador Hack**
```asm
@2
D=A
@a
M=D     // a = 2

@3
D=A
@b
M=D     // b = 3

@suma
0;JMP   // Llamar función

(RETURN)
@resultado
M=D     // Guardar el retorno en resultado
@END
0;JMP   // Fin del programa

(suma)
@a
D=M
@b
D=D+M   // D = a + b
@RETURN
0;JMP   // Regresar con el resultado en D
```
