1. **¿Qué hace esto `int *pvar;`?**  
   Declara un puntero llamado pvar que puede almacenar la dirección de una variable de tipo int. En este punto, pvar no apunta a nada en particular.  

2. **¿Qué hace esto `*pvar = var;`?**  
   Almacena el valor de var en la dirección de memoria a la que apunta pvar. Esto solo funciona si pvar ya apunta a una dirección válida. Si pvar no ha sido inicializado, esto puede causar un error.  

3. **¿Qué hace esto `var2 = *pvar;`?**  
   Asigna a var2 el contenido de la dirección de memoria almacenada en pvar. Es decir, var2 tendrá el mismo valor que la variable a la que apunta pvar.  

4. **¿Qué hace esto `pvar = &var3;`?**  
   Hace que pvar apunte a la dirección de var3, es decir, ahora pvar almacena la dirección en memoria de var3 y puede usarse para modificar su contenido indirectamente.  
