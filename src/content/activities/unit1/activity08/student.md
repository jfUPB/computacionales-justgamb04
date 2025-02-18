#### Codigo del programa

```assembly
// Cargar el valor almacenado en la dirección de memoria 5 en D
@5
D=M

// Comparar D con 10
@10
D=D-A  // D = M[5] - 10

// Si D < 0 (M[5] < 10), saltar a INFERIOR
@INFERIOR
D;JLT

// Si no, guardar 0 en la dirección 7
@7
M=0
@FIN
0;JMP

// Si M[5] < 10, guardar 1 en la dirección 7
(INFERIOR)
@7
M=1

// Fin del programa
(FIN)
@FIN
0;JMP
```

---




![image](https://github.com/user-attachments/assets/c3abe7cf-3164-4549-b625-94cf25b4e469)

![image](https://github.com/user-attachments/assets/c4e47a3e-91d5-477a-9a66-e502a07e5720)

![image](https://github.com/user-attachments/assets/0b52b137-6d06-4733-995c-49682ca3492d)

