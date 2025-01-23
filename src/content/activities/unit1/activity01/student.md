#### mi programa

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@6
0;JMP
```

<!--
Esto es un comentario que nunca saldrá a la luz
-->
**Explicación**: simplemente cambié los numeros 1 y 2 por 60 y 9 y la dirección de salto que modificaba el PC la cambié de 6 a 0. Con esto se cumplen los requisitos. Y al simular mi programa, el programa funcionó. así sería:

``` asm
@60 
D=A 
@9 
D=D+A 
@6 
M=D 
@0 
0;JMP
```
