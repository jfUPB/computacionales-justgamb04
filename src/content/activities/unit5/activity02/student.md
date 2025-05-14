## 1. Explorando el Objeto `ofApp` en Memoria

### Hipótesis

Antes de ejecutar el código, espero encontrar en memoria una estructura que represente la instancia de `ofApp`, con sus métodos públicos disponibles, y un vector `particles` conteniendo punteros a objetos `Particle` (o derivados).

### Observaciones y Conclusiones

* El depurador muestra que `particles` es un vector de punteros.
* Solo existe en memoria mientras la app se ejecuta.
* Podemos inspeccionar la estructura del objeto, pero no acceder directamente a los valores privados.

## 2. Explorando `CircularExplosion` en Memoria

### Jerarquía de Clases

```cpp
Particle
└── ExplosionParticle
    └── CircularExplosion
```

### Observaciones

* El objeto contiene campos heredados desde `ExplosionParticle` y `Particle`.
* En memoria, aparecen organizados de forma jerárquica.

### Conclusión

La jerarquía de clases se refleja claramente en la memoria. Cada segmento del objeto pertenece a una clase base en la cadena de herencia.

## 3. Explorando la `_vtable` (Virtual Table)

### ¿Qué es la `_vtable`?

Una tabla interna que contiene punteros a los métodos virtuales del objeto. Permite seleccionar dinámicamente el método correcto durante la ejecución (polimorfismo).

### Comparación y Conclusión

* Ambas tablas tienen direcciones distintas para algunos métodos: muestra que han sido sobreescritos.
* El polimorfismo es posible gracias a esta tabla que elige dinámicamente qué función ejecutar según el tipo real del objeto.

## 4. Reflexión: ¿Para qué sirve la `_vtable`?

Permite el **polimorfismo en tiempo de ejecución**, al decidir qué versión de un método virtual debe ejecutarse según el tipo real del objeto, no el tipo del puntero.

## 5. Encapsulamiento

### Experimento: Acceso a Modificadores

#### Código:

```cpp
AccessControl ac;
ac.publicVar = 10; // Válido
ac.protectedVar = 20; // Error
ac.privateVar = 30; // Error
```

### Resultado

Errores de compilación al acceder a `protectedVar` y `privateVar`.

### Conclusión

El encapsulamiento en C++ restringe el acceso desde fuera de la clase, pero esto solo se garantiza en tiempo de compilación.

### Experimento: Rompiendo el Encapsulamiento

#### Código con `reinterpret_cast`

```cpp
int* ptrInt = reinterpret_cast<int*>(&obj);
```

### Resultado

Acceso directo a miembros privados de un objeto en memoria.

### Conclusión

Aunque el compilador impide acceder a miembros privados, en tiempo de ejecución es posible romper el encapsulamiento con punteros y manipulación directa de memoria. Esto evidencia que la seguridad del encapsulamiento es solo superficial en C++.

### ¿Qué es el encapsulamiento?

Es el principio de ocultar los detalles internos de una clase (atributos y métodos), exponiendo solo lo necesario mediante interfaces públicas. Es fundamental para proteger la integridad del objeto y reducir el acoplamiento.

## 6. Herencia en C++

### Conclusión

La memoria refleja la jerarquía de clases. El objeto contiene todos los campos heredados y los propios de su clase.

### ¿Cómo se implementa la herencia en C++?

Mediante el uso de la sintaxis `: public ClaseBase`, donde la clase derivada hereda los miembros públicos y protegidos. En tiempo de ejecución, todos los datos de las clases base están presentes en el objeto derivado.

### Herencia Múltiple

C++ permite herencia de múltiples clases base.

#### Ejemplo:

```cpp
class A { public: int a; };
class B { public: int b; };
class C : public A, public B { public: int c; };
```
#### Conclusión

La memoria del objeto contiene áreas separadas para cada clase base, lo cual puede generar ambigüedades si no se maneja con cuidado.

## 7. Polimorfismo

### Observación del Método `update()` en Tiempo de Ejecución

```cpp
particles[i]->update(dt);
```

### Resultado

Cada objeto invoca su versión específica del método `update()`.

### Conclusión

Gracias al uso de métodos virtuales, el compilador utiliza la `_vtable` para ejecutar el método adecuado según el tipo real del objeto, no el tipo del puntero.

### Pregunta Final: ¿Qué relación existe entre los métodos virtuales y el polimorfismo?

Los métodos virtuales permiten redefinir comportamientos en clases derivadas. El polimorfismo depende de esta funcionalidad para ejecutar métodos apropiados en tiempo de ejecución, según el tipo real del objeto.

## Conclusiones

* La memoria refleja fielmente la jerarquía de clases.
* El encapsulamiento es fuerte en compilación, débil en ejecución.
* La herencia permite reutilización y extensión del código.
* La `_vtable` es clave para lograr el polimorfismo.
* El depurador es una herramienta poderosa para ver el comportamiento real de los objetos en ejecución.

