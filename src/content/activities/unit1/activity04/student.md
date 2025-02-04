#### ¿Cuál es la función de cada tipo de instrucción en el lenguaje ensamblador Hack?**

En el lenguaje ensamblador Hack, existen dos tipos principales de instrucciones: las **A-instructions** y las **C-instructions**.

- **A-instructions (Address instructions)**: Son instrucciones que se utilizan para cargar un valor en el registro **A**. Este valor puede ser una dirección de memoria o un valor inmediato (constante). La función de las A-instructions es establecer el valor de la dirección de memoria que se utilizará en otras operaciones o directamente asignar un valor a una dirección de memoria. 

- **C-instructions (Computation instructions)**: Son instrucciones que realizan operaciones de cómputo, como operaciones aritméticas y lógicas, y controlan cómo se deben almacenar los resultados de estas operaciones, indicando si el valor debe guardarse en la memoria o en un registro. También especifican condicionales de salto, permitiendo el flujo de control dentro del programa.

#### ¿Cómo se representa cada tipo de instrucción en binario?**

- **A-instructions**: Las A-instructions se representan en binario con un formato de 16 bits. El primer bit es siempre **0** (indica que es una A-instrucción), seguido de 15 bits que representan el valor de la dirección de memoria o el valor inmediato (en formato binario).
  
##### Ejemplo de formato de A-instruction:
  ```
  0 000000000000000 (15 bits para la dirección o valor)
  ```

- **C-instructions**: Las C-instructions tienen un formato de 16 bits. El primer bit es **1** (indica que es una C-instrucción), seguido de 3 bits que indican el campo **destino** (donde se almacenará el resultado de la operación), luego 7 bits para el campo **comp** (la operación de cálculo o comparación que se va a realizar), y finalmente 3 bits para el campo **jump** (la operación de salto, si corresponde).

##### Ejemplo de formato de C-instruction:
  ```
  111 a cccccc ddd jjj
  |   |      |    |   |
  |   |      |    |   +--- jump (condicional de salto)
  |   |      |    +------- dest (destino)
  |   |      +------------ comp (cálculo)
  |   +-------------------- bit fijo que indica que es una C-instrucción
  +------------------------ bit fijo
  ```

**3. Ejemplos de A-instructions y C-instructions**

### Ejemplos de A-instructions:
- **A-instruction: `@10`**
  - **Binario**: `0000000000001010`
  - **Explicación**: Esta instrucción establece el valor del registro A en la dirección de memoria 10. Si este valor es utilizado en una C-instrucción posterior, se refiere a la memoria en esa dirección.
  
- **A-instruction: `@R0`**
  - **Binario**: `0000000000000000`
  - **Explicación**: El valor de la dirección de memoria para el registro **R0** es 0, por lo que esta instrucción carga el registro A con el valor de la dirección de **R0** (que es 0).

- **A-instruction: `@100`**
  - **Binario**: `0000000001100100`
  - **Explicación**: Esta instrucción carga el registro A con el valor de la dirección de memoria 100, que puede utilizarse luego en una operación de cómputo.

### Ejemplos de C-instructions:
- **C-instruction: `D=A`**
  - **Binario**: `1110001100001000`
  - **Explicación**: Esta instrucción indica que el valor del registro A debe ser copiado en el registro **D**. El valor en **A** es copiado al **D** sin ninguna operación aritmética.

- **C-instruction: `M=D`**
  - **Binario**: `1110001100000001`
  - **Explicación**: Aquí, el valor del registro **D** se almacena en la dirección de memoria que está en el registro **A** (el valor almacenado en **A** se usa como dirección). El valor de **D** se guarda en esa dirección de memoria.

- **C-instruction: `D=D+A`**
  - **Binario**: `1110000010010000`
  - **Explicación**: Esta instrucción realiza una operación de adición entre los valores almacenados en los registros **D** y **A**, y guarda el resultado en el registro **D**. 

**Conclusión:**

- Las **A-instructions** se encargan de establecer valores de direcciones de memoria o valores constantes en el registro **A**. Se representan en un formato de 16 bits, donde los 15 bits restantes codifican la dirección o el valor.
  
- Las **C-instructions** realizan operaciones de cómputo y control, especificando dónde almacenar los resultados y cómo gestionar los saltos. Se representan también en un formato de 16 bits, con campos para el cálculo (comp), el destino (dest), y el salto (jump).
