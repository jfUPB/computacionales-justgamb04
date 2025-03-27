
### Código en Ensamblador
```asm
// Definir direcciones de memoria
@KBD
D=M             // Leer tecla presionada

@80             // Código ASCII de 'P' (mayúscula)
D=D-A           // Comparar con 'P'
@PINTAR         // Si es 'P', saltar a pintar
D;JEQ          

@66             // Código ASCII de 'B' (mayúscula)
D=D+A           // Comparar con 'B'
@BORRAR         // Si es 'B', saltar a borrar
D;JEQ

@INICIO         // Si no es ni 'P' ni 'B', reiniciar
0;JMP           

// ------------------------------
// Función para pintar la pantalla
// ------------------------------
(PINTAR)
@SCREEN         // Dirección base de la pantalla
D=A
@i
M=D             // Inicializar contador en i = SCREEN

(PINTAR_LOOP)
@i
D=M
@KBD
D=D-A
@RETORNO_PANTALLA
D;JGE           // Si llegamos al final de la pantalla, volver

@i
A=M
M=-1            // Pintar píxeles (poner todos en 1)

@i
M=M+1          // i++
@PINTAR_LOOP
0;JMP           // Repetir hasta llenar la pantalla

// ------------------------------
// Función para borrar la pantalla
// ------------------------------
(BORRAR)
@SCREEN         // Dirección base de la pantalla
D=A
@i
M=D             // Inicializar contador en i = SCREEN

(BORRAR_LOOP)
@i
D=M
@KBD
D=D-A
@RETORNO_PANTALLA
D;JGE           // Si llegamos al final de la pantalla, volver

@i
A=M
M=0             // Apagar píxeles (poner todos en 0)

@i
M=M+1          // i++
@BORRAR_LOOP
0;JMP           // Repetir hasta vaciar la pantalla

// ------------------------------
// Retorno desde la función pantalla
// ------------------------------
(RETORNO_PANTALLA)
@INICIO
0;JMP           // Volver al inicio

// ------------------------------
// Punto de inicio del programa
// ------------------------------
(INICIO)
@KBD
D=M             // Leer tecla presionada

@80             // Código ASCII de 'P' 
D=D-A           
@PINTAR
D;JEQ           // Si es 'P', saltar a PINTAR

@66             // Código ASCII de 'B'
D=D+A           
@BORRAR
D;JEQ           // Si es 'B', saltar a BORRAR

@INICIO
0;JMP           // Volver a empezar si no es una tecla válida
```
### **Explicación del código**
1. **Se lee la tecla presionada en `KBD`** y se compara con los valores ASCII de 'P' (`80`) y 'B' (`66`).
2. **Si se presiona 'P'**, se llama a la función `PINTAR`, que recorre toda la memoria de la pantalla (`SCREEN[8192]`) llenándola con `-1` (todos los bits en 1).
3. **Si se presiona 'B'**, se llama a la función `BORRAR`, que hace lo mismo pero llenando la pantalla con `0` (apagando los píxeles).
4. **Si no se presiona ni 'P' ni 'B'**, el programa vuelve al inicio y sigue esperando una entrada.
5. **Las funciones terminan en `RETORNO_PANTALLA`**, que devuelve el control al inicio para seguir esperando nuevas teclas.

