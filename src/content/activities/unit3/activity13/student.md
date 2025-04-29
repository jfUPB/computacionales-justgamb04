## **Código fuente**

```cpp
#include <iostream>
using namespace std;

class CuentaBancaria {
private:
    int saldo;
    int* historial;  // Almacena los últimos movimientos
    static int totalCuentas;
public:
    string titular;

    // Constructor
    CuentaBancaria(string nombre, int saldoInicial) : titular(nombre), saldo(saldoInicial) {
        historial = new int[5] {0, 0, 0, 0, 0}; // Inicializa historial
        totalCuentas++;
        cout << "Cuenta creada para " << titular << " con saldo $" << saldo << endl;
    }

    // Destructor
    ~CuentaBancaria() {
        delete[] historial;
        cout << "Cuenta de " << titular << " destruida." << endl;
    }

    // Método que deposita dinero (por valor, no modifica el argumento)
    void depositar(int cantidad) {
        saldo += cantidad;
        historial[0] = cantidad;
        cout << "Depósito de $" << cantidad << " realizado. Nuevo saldo: $" << saldo << endl;
    }

    // Método que transfiere dinero (por referencia: afecta a otra cuenta)
    void transferir(CuentaBancaria& destino, int cantidad) {
        if (saldo >= cantidad) {
            saldo -= cantidad;
            destino.saldo += cantidad;
            cout << "Transferencia de $" << cantidad << " a " << destino.titular << " realizada." << endl;
        } else {
            cout << "Fondos insuficientes para transferir." << endl;
        }
    }

    void mostrarSaldo() {
        cout << "Saldo actual de " << titular << ": $" << saldo << endl;
    }

    static int getTotalCuentas() {
        return totalCuentas;
    }
};

// Inicialización del miembro estático
int CuentaBancaria::totalCuentas = 0;

// Función que recibe objeto por valor
void mostrarResumen(CuentaBancaria cuenta) {
    cout << "[Resumen por copia] Titular: " << cuenta.titular << endl;
}

int main() {
    cout << "--- INICIO DEL PROGRAMA ---" << endl;

    // Objeto en el stack
    CuentaBancaria cuenta1("Alice", 1000);

    // Objeto dinámico (en el heap)
    CuentaBancaria* cuenta2 = new CuentaBancaria("Bob", 500);

    cuenta1.depositar(200);
    cuenta2->transferir(cuenta1, 100);

    mostrarResumen(cuenta1); // Paso por valor
    cuenta1.mostrarSaldo();
    cuenta2->mostrarSaldo();

    cout << "Total de cuentas: " << CuentaBancaria::getTotalCuentas() << endl;

    delete cuenta2;

    cout << "--- FIN DEL PROGRAMA ---" << endl;
    return 0;
}
```
## **Aplicación de conceptos**

| Concepto                         | ¿Cómo se aplicó? |
|----------------------------------|------------------|
| **Clases y objetos**             | Clase `CuentaBancaria`, objetos `cuenta1`, `cuenta2`. |
| **Constructores y destructores** | Se definen para inicializar el saldo y limpiar la memoria del historial. |
| **Métodos y atributos**          | `depositar()`, `transferir()`, `mostrarSaldo()` y atributo `saldo`, `titular`, etc. |
| **Paso por valor**              | `mostrarResumen(CuentaBancaria cuenta)` recibe una copia. |
| **Paso por referencia**         | `transferir(CuentaBancaria& destino)` modifica otro objeto. |
| **Punteros y referencias**      | `cuenta2` es un puntero. Se accede con `->`. |
| **Objetos en el stack y heap**  | `cuenta1` está en el stack, `cuenta2` en el heap (`new`). |
| **Variable estática**           | `totalCuentas` se incrementa cada vez que se crea una cuenta. |
| **Depuración**                  | Puedes colocar breakpoints en `main()` y seguir las llamadas a métodos y constructores para ver cómo cambian los valores y direcciones. |

## **Análisis detallado de memoria**

| Variable u objeto         | Segmento de memoria | Explicación                                                                 |
|---------------------------|---------------------|------------------------------------------------------------------------------|
| `cuenta1`                 | **Stack**           | Variable local del `main()`, almacenada automáticamente.                    |
| `cuenta2` (el puntero)    | **Stack**           | El puntero está en el stack.                                                |
| `*cuenta2` (el objeto)    | **Heap**            | El objeto creado con `new` está en el heap.                                 |
| `CuentaBancaria::totalCuentas` | **Segmento de datos estáticos** | Variable estática compartida entre todas las instancias.                    |
| `historial` dentro de objetos | **Heap**            | Arreglo dinámico dentro de cada cuenta, creado con `new int[5]`.           |
| Argumento `cuenta` en `mostrarResumen()` | **Stack (copia)** | Copia del objeto original, almacenado temporalmente en el stack.           |
