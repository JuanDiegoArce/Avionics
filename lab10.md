# Clase 20 de octubre del 2025
## Depuración, gdb, valgrind

# Depuración, GDB y Valgrind — Resumen Completo

## Depuración
La **depuración** es el proceso de identificar y eliminar errores o fallos en un programa de software.  
Es una etapa esencial del ciclo de desarrollo que garantiza que el código funcione correctamente y cumpla con los requisitos.

### Importancia
1. **Garantía de calidad:** asegura que el software funcione sin fallos.  
2. **Mantenimiento del código:** facilita su actualización y legibilidad.  
3. **Eficiencia del desarrollo:** detectar errores temprano ahorra tiempo y costos.  
4. **Experiencia del usuario:** reduce errores que afecten su uso.

---

## Tipos de errores
1. **Errores de sintaxis:**  
   - Violaciones en las reglas del lenguaje (ej. punto y coma faltante).  
   - Detectados por el compilador antes de ejecutar.

2. **Errores de tiempo de ejecución:**  
   - Ocurren mientras el programa se ejecuta (ej. división por cero).  
   - Pueden causar que el programa se detenga inesperadamente.

3. **Errores lógicos:**  
   - El programa se ejecuta pero produce resultados incorrectos.  
   - Son los más difíciles de detectar.

---

## Conceptos clave
- **Breakpoints (puntos de interrupción):** Pausan el programa en una línea específica.  
- **Stepping:**  
  - `Step over`: avanza sin entrar en funciones.  
  - `Step into`: entra en la función llamada.  
  - `Step out`: sale de la función actual.  
- **Inspección de variables:** muestra o modifica valores en tiempo real.  
- **Call Stack (pila de llamadas):** muestra la secuencia de funciones ejecutadas hasta el punto actual.

---

## GDB (GNU Debugger)
**GDB** es una herramienta para depurar programas en **C, C++** y otros lenguajes.  
Permite ver lo que ocurre dentro del programa mientras se ejecuta o al fallar.

### Características
- Controlar la ejecución (pausar, continuar, paso a paso).  
- Inspeccionar y modificar variables.  
- Navegar por la pila de llamadas.  
- Establecer breakpoints.  
- Seguir el flujo del programa.

### Comandos principales
| Comando | Descripción |
|----------|--------------|
| `run` | Inicia la ejecución del programa |
| `break` | Crea un punto de interrupción |
| `next` | Ejecuta la siguiente línea sin entrar en funciones |
| `step` | Ejecuta la siguiente línea y entra en funciones |
| `continue` | Reanuda la ejecución hasta el siguiente breakpoint |
| `print` | Muestra el valor de una variable |
| `backtrace` | Muestra la pila de llamadas actual |

## Análisis de memoria — Valgrind

**Valgrind** es un conjunto de herramientas para analizar programas y encontrar errores de memoria y concurrencia.

### Funcionalidades
- **Pérdidas de memoria:** detecta memoria no liberada.  
- **Errores de memoria:** detecta accesos fuera de límites o no inicializados.  
- **Análisis de concurrencia:** identifica problemas en programas multihilo.

### Herramienta principal: Memcheck
- Supervisa todas las operaciones de memoria.  
- Detecta errores de lectura/escritura fuera de rango.  
- Informa sobre memoria no inicializada o liberada más de una vez.

### Ejemplo

## Análisis de hilos — Helgrind

**Helgrind** (parte de Valgrind) detecta errores de concurrencia, como **condiciones de carrera** y **bloqueos**.

---

## Sanitizers (Detectores del compilador)

Los **Sanitizers** son herramientas que ayudan a detectar errores en tiempo de ejecución al compilar el código con opciones especiales.

---

### Tipos más comunes
- `address` → **ASan** (errores de memoria).  
- `thread` → **TSan** (condiciones de carrera).

---

## AddressSanitizer (ASan)

Detecta **errores de memoria** como:
- Accesos fuera de límites (*heap-buffer-overflow*, *stack-buffer-overflow*).  
- Uso de memoria liberada (*use-after-free*).  
- Doble liberación o memoria no inicializada.

---

## ThreadSanitizer (TSan)

Detecta **errores de concurrencia** y **data races** en programas multihilo.
