# Subsistema de Aviónica — IREC 2026 (Categoría 10 000 ft COTS)

## Requerimientos Oficiales de Aviónica

Según el **IREC Rules & Requirements 2026 (v1.0)** y el **Design, Test and Evaluation Guide (DTEG 2025 + Updates 2026)**, todos los equipos deben cumplir los siguientes requisitos para el subsistema de aviónica:

### 1. Altímetro Oficial y Registro de Datos
- El cohete debe incluir al menos **un altímetro barométrico COTS** con capacidad de **registro interno de datos de vuelo**.
- Este dispositivo será la **fuente oficial** de información para el cálculo del apogeo.
- La telemetría **no sustituye** al registro interno del altímetro.
- El equipo deberá presentar, durante la **inspección posterior al vuelo**, los cables y software necesarios para descargar los datos oficiales del altímetro.

### 2. GPS de Rastreo
- Todos los cohetes deben contar con un **sistema de rastreo GPS COTS** para facilitar la recuperación.
- Si el cohete posee partes desplegables o módulos separados, **cada uno debe tener su propio GPS independiente**.
- Los sistemas deben operar dentro de las bandas **400 MHz o 900 MHz** asignadas por el comité DTEG.
- Cada GPS debe contar con su **propia fuente de energía y su propio switch de armado**, independientes de los demás canales de aviónica.

### 3. Computadoras de Vuelo y Redundancia
- El sistema de recuperación debe incluir **dos computadoras o altímetros COTS independientes**, cada uno con:
  - Su propio sensor barométrico.
  - Fuente de alimentación separada.
  - Switch de armado independiente.
  - Control sobre su propio sistema de liberación (CO₂ o pirotécnico).
- Al menos uno de ellos debe ser capaz de registrar la altitud y los eventos para verificación posterior.

### 4. Sistema de Energía
- **Se prohíben las baterías LiPo** dentro del cohete o de cualquier módulo interno.
- Solo se permiten fuentes **COTS seguras**, como baterías de litio primario (Energizer L522) o celdas Li-ion 18650 con circuito de protección.
- Cada sistema electrónico debe contar con **una fuente de energía dedicada** y **un switch de armado independiente**.

### 5. Cableado y Seguridad Eléctrica
- Todo cableado considerado “safety-critical” (recuperación, ignición, GPS, etc.) debe cumplir con:
  - Conectores asegurados estructuralmente.
  - Etiquetado o codificación por colores.
  - Alivio de tensión y sujeción mecánica.
  - Prohibición total de empalmes temporales o “wire nuts”.

### 6. Pruebas y Documentación
- Las **pruebas de tierra** de la aviónica deben realizarse antes del **tercer informe de progreso**, incluyendo video y registro.
- Las **pruebas de vuelo** pueden reemplazar las de tierra si los sistemas son idénticos a los utilizados en el lanzamiento.
- El **Technical Report** debe incluir:
  - Diagramas eléctricos.
  - Procedimientos de armado.
  - Evidencia de redundancia y seguridad.
  - Listado de componentes COTS y certificaciones de cumplimiento.

---

## Componentes de Aviónica (COTS)

A continuación se presenta la lista completa de componentes requeridos para cumplir los lineamientos IREC 2026, junto con su función y principio de operación.

### 2.1 Computadoras de Vuelo / Altímetros

| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Featherweight Blue Raven (Primario)** | Altímetro oficial y computadora principal. Controla los eventos de liberación y registra los datos de vuelo. | Mide la presión atmosférica mediante un sensor barométrico digital, calcula altitud y velocidad en tiempo real, y acciona las válvulas de CO₂ en el apogeo y a baja altitud. Registra los datos internamente para inspección posterior. |
| **Missile Works RRC3 (Respaldo)** | Computadora COTS secundaria para recuperación redundante. | Utiliza un sensor barométrico MEMS que detecta el punto de apogeo y la fase de descenso. Acciona su propio sistema de liberación por CO₂ con temporizaciones configuradas independientemente del sistema primario. |

**Ambos sistemas son independientes en energía, armado y control.**

---

### 2.2 Sistema de Rastreo GPS (Dual e Independiente)

| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Featherweight GPS Tracker (Primario)** | Rastrea la posición del cohete en tiempo real y envía coordenadas al receptor en tierra. | Recibe señales GNSS (GPS/Galileo) y transmite la posición a 900 MHz hacia el receptor Featherweight App o estación terrena. |
| **Eggtimer Quasar GPS (Respaldo)** | Rastreo redundante en frecuencia distinta para asegurar recuperación. | Módulo GPS independiente que transmite coordenadas a 433 MHz a un receptor LCD portátil o estación base. |

🔋 Cada GPS tiene **su propia batería y switch**.

---

### 2.3 Sistema de Energía

| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Baterías de litio primario (Energizer L522 9V)** | Alimentan cada subsistema de forma independiente (Blue Raven, RRC3, GPS-A, GPS-B). | Celdas de litio primario (Li-FeS₂) seguras, de alta densidad energética, con tensión estable y sin riesgo de inflamación. |
| **Switches de armado (x4)** | Permiten activar o desactivar cada canal de energía de manera independiente. | Interrumpen la línea positiva de cada batería. Pueden ser de tipo magnético o mecánico (screw switch). |
| **Fusibles o Breakers (opcional)** | Protegen cada canal ante sobrecorriente. | Abren el circuito si se supera la corriente máxima, evitando cortocircuitos o sobrecalentamientos. |

---

### 2.4 Sistema de Liberación por CO₂


| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Válvulas de liberación por CO₂ (x2)** | Liberan gas comprimido para separar etapas o desplegar paracaídas. | Controladas eléctricamente por los altímetros, las válvulas abren al recibir una señal, liberando CO₂ de un cartucho presurizado para generar la fuerza de separación. |
| **Cartuchos de CO₂ (12 g o 16 g)** | Fuente de gas presurizado. | Al activarse la válvula, el gas expande rápidamente dentro del compartimiento, generando presión que empuja el paracaídas o desacopla las secciones. |
| **Conductos / Manifold de presión** | Canaliza el gas hacia el compartimento de despliegue. | Tubos o cámaras selladas que distribuyen uniformemente el CO₂. |
| **Sensores de presión (opcional)** | Monitorean la liberación y la presión del sistema. | Detectan cambios de presión interna y los registran para validación de funcionamiento. |


---

### 2.5 Estructura y Montaje

| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Sled de aviónica (54 mm o 75 mm)** | Soporte central de los módulos de aviónica. | Placa COTS (Additive Aerospace o impresa en 3D) con orificios para sujetar altímetros, baterías y válvulas de CO₂. |
| **Varillas roscadas + tuercas y arandelas** | Estructura de unión del bay. | Dos varillas #1/4-20 atraviesan el sled y se fijan a los bulkheads, formando una estructura sólida. |
| **Bulkheads / Tapas del bay** | Sellan el compartimiento y soportan las conexiones. | Placas de aluminio o fibra con pasacables y válvulas montadas. |
| **Arnés de cableado** | Conecta todos los sistemas de forma segura. | Cables AWG20–22 para potencia, AWG24 para señal, con conectores JST y termorretráctil. |

---

### 2.6 Telemetría y Estación Terrena

| Componente | Función | Cómo funciona |
|-------------|----------|----------------|
| **Receptor Featherweight Ground Station** | Recibe telemetría BLE y GPS del Blue Raven y Featherweight GPS. | Conexión Bluetooth o dongle USB con visualización en tiempo real. |
| **Receptor Eggtimer Quasar** | Recibe señal del GPS secundario. | Pantalla LCD que muestra coordenadas actualizadas en campo. |
| **Laptop o Tablet de Estación Terrena** | Registra y monitorea datos de vuelo. | Ejecuta software de visualización y almacenamiento de datos del lanzamiento. |

---

## Funcionamiento General del Sistema

1. **Antes del vuelo**, cada canal (Blue Raven, RRC3, GPS A/B) se alimenta y arma por separado.  
2. Ambos altímetros inician el registro de presión y aceleración desde el despegue.  
3. En el **apogeo**, los sistemas activan sus respectivas **válvulas de CO₂**, liberando gas para separar la sección superior e iniciar el despliegue del drogue.  
4. Durante el descenso, al alcanzar la altitud programada (300–500 m), se acciona la **segunda válvula de CO₂**, desplegando el paracaídas principal.  
5. Los GPS transmiten coordenadas continuamente a los receptores de tierra.  
6. Todo el registro barométrico queda almacenado en el altímetro principal para verificación posterior ante jueces.

---

## Lista Completa de Componentes

| Categoría | Componentes Requeridos |
|------------|------------------------|
| **Computadoras de Vuelo / Altímetros** | 1× Featherweight Blue Raven (principal) • 1× Missile Works RRC3 (respaldo) |
| **Rastreo GPS** | 1× Featherweight GPS (primario) • 1× Eggtimer Quasar (respaldo) |
| **Energía y Armado** | 4× Baterías de litio primario 9 V • 4× Switches independientes • (4× Fusibles opcionales) |
| **Liberación por CO₂** | 2× Válvulas solenoides de CO₂ • 2× Cartuchos CO₂ (12–16 g) • Conductos / manifold • Sensores de presión (opcional) |
| **Estructura y Montaje** | 1× Sled 54 mm • 2× Varillas + tuercas/arandelas • 2× Bulkheads • Arnés de cableado |
| **Telemetría y Estación Terrena** | Receptor Featherweight • Receptor Eggtimer • Laptop o Tablet |
| **Accesorios / Seguridad** | Etiquetas, checklist de armado, puertos de presión, espuma filtrante, test de continuidad |

---

**Cumplimiento IREC 2026:**
- 100 % COTS.  
- Doble sistema de recuperación independiente.  
- Sin baterías LiPo.   
- GPS redundante.  
- Registro interno verificable.  
- Cableado seguro y codificado.

---
## Tabla de Masa de Aviónica (Estimado Total — Sistema COTS con CO₂)

| Ítem | Modelo / Descripción | Masa (g) |
|------|----------------------|---------:|
| **Computadora principal (altímetro)** | Featherweight Blue Raven | **6.8** |
| **Computadora de respaldo (altímetro)** | Missile Works RRC3 | **13.6** |
| **GPS primario** | Featherweight GPS (placa + antena) | **15.0** |
| **GPS de respaldo** | Eggtimer Quasar | **28.0** |
| **Baterías (x4)** | 9 V litio primario (una por canal) | **135.6** |
| **Switches de armado (x4)** | Magnéticos o mecánicos | **6.8** |
| **Válvulas de CO₂ (x2)** | Solenoides de liberación | **60.0** |
| **Cartuchos de CO₂ (x2)** | 12–16 g cada uno | **32.0** |
| **Conductos y manifold de presión** | Tuberías y conectores | **25.0** |
| **Sled de aviónica (54 mm)** | Additive Aerospace o impreso en 3D | **39.5** |
| **Varillas + tuercas/arandelas** | Estructura del bay | **25.0** |
| **Cableado y termorretráctil** | Arnés completo (AWG20–24) | **20.0** |
| **Sensores de presión (opcional)** | Monitoreo CO₂ | **8.0** |
| **Espuma filtrante + puertos de presión** | Compensación barométrica | **4.0** |
| **Total estimado** |  | **≈ 419.3 g** |

---

### Notas importantes
- Este peso corresponde a la **bahía de aviónica completa**, lista para integrar en el cohete.  
- El margen de error es ±10 %, dependiendo del tipo de válvulas de CO₂ y material estructural usado (aluminio, ABS o fibra).  
- Cumple con los límites típicos de masa para una sección de aviónica de **54 mm–75 mm**, dentro del rango seguro para un cohete de 10 000 ft.
