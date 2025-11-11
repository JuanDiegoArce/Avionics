## 4. Identificación de problemas y oportunidades

Durante el análisis del sistema **EIEInfo** se identificaron los siguientes aspectos críticos relacionados con la estructura del código, la arquitectura y la experiencia del usuario.  
Cada observación se asocia con los archivos específicos en donde se detectó el problema.

---

### **Código duplicado**
**Archivos:**  
- `src/server/administrativos/models.py`  
- `src/server/estudiantes/models.py`  
- `src/server/trabajo_final_de_graduacion/models.py`

**Descripción:**  
Se encontraron estructuras de clases y validaciones similares replicadas entre módulos, especialmente en las definiciones de modelos de usuarios, funcionarios y estudiantes.  
También, ciertas funciones de envío de correo y manejo de fechas se repiten en múltiples módulos sin una librería central común, lo que genera **duplicidad de lógica** y mayor probabilidad de errores cuando se realizan cambios en el código.

---

### **Falta de modularidad**
**Archivos:**  
- `src/server/profesores/views.py`  
- `src/server/trabajo_final_de_graduacion/views.py`  
- `src/server/webpage/views.py`

**Descripción:**  
Los controladores combinan lógica de negocio, consultas y renderizado de plantillas dentro del mismo archivo.  
El sistema no presenta una separación clara entre capas (controladores, servicios y datos). También se evidencian importaciones cruzadas entre apps como `profesores`, `administrativos` y `trabajo_final_de_graduacion`, provocando un **acoplamiento alto**, esto puede dificultar el mantenimiento del sistema.

---

### **Problemas de UI/UX**
**Archivos:**  
- `src/server/webpage/templates/webpage/index.html`  
- `src/server/estudiantes/templates/estudiantes/*.html`  
- `src/server/eventos/templates/eventos/*.html`

**Descripción:**  
La interfaz del usuario varía visualmente entre módulos, los formularios carecen de mensajes de confirmación o advertencia coherentes. También algunos formularios son extensos y no incluyen validaciones visuales o avisos de error claros.  

---

### **Falta de validación o seguridad**
**Archivos:**  
- `src/server/estudiantes/forms.py`  
- `src/server/administrativos/forms.py`  
- `src/server/trabajo_final_de_graduacion/views.py`

**Descripción:**  
Existen formularios que no implementan validaciones robustas del lado del servidor.  
También se encontraron vistas que no verifican los roles del usuario antes de permitir ciertas operaciones (por ejemplo, modificar registros de estudiantes o TFG).  
Esto compromete la **seguridad del flujo de datos y el control de acceso** dentro del sistema.

---

### **Carencia de documentación**
**Archivos:**  
- `src/server/README.md` (vacío o con contenido mínimo)  
- `src/server/administrativos/views.py`  
- `src/server/trabajo_final_de_graduacion/models.py`

**Descripción:**  
El proyecto carece de documentación técnica y de instalación actualizada.  
Muchos módulos no incluyen comentarios descriptivos en las funciones ni docstrings que expliquen su propósito.  
Esto dificulta la comprensión del sistema por parte de nuevos desarrolladores.

---

### **Lógica mezclada entre capas**
**Archivos:**  
- `src/server/webpage/views.py`  
- `src/server/trabajo_final_de_graduacion/models.py`  
- `src/server/eventos/views.py`

**Descripción:**  
Se observaron funciones que ejecutan lógica de negocio directamente dentro de las vistas, y modelos (`models.py`) que contienen operaciones que deberían anular en servicios o controladores.  
Por ejemplo, generación de PDFs o envío de correos desde los modelos.  
Esto **viola la separación de responsabilidades** del patrón MTV de Django, incrementando la complejidad y dificultando las pruebas unitarias.

---

## 4.2 Oportunidades de mejora propuestas

### A. Oportunidades técnicas

| Nº | Propuesta técnica | Descripción y justificación |
|----|-------------------|-----------------------------|
| **T1** | **Refactorización modular del sistema** | Separar la lógica común (usuarios, roles, ciclo académico) en una app core reutilizable. Esto reduce el acoplamiento y facilita la escalabilidad. |
| **T2** | **Implementar capa de servicios o controladores lógicos** | Extraer funciones de negocio complejas de `views.py` a módulos tipo `services.py`, siguiendo principios SOLID. |
| **T3** | **Centralizar validaciones y permisos** | Crear middlewares o *decorators* que manejen roles, autenticación y permisos de acceso de forma homogénea en todas las vistas. |
| **T4** | **Mejorar estructura de carpetas y convenciones de código** | Adoptar nomenclaturas uniformes, carpetas para *forms*, *serializers* y *tests* en cada módulo, facilitando contribuciones futuras. |
| **T5** | **Implementar sistema de logging y manejo de errores** | Integrar un registro centralizado (por ejemplo, con Python logging o Sentry) que permita auditar fallos y monitorear el funcionamiento. |

---

### B. Oportunidades funcionales

| Nº | Propuesta funcional | Descripción y justificación |
|----|---------------------|-----------------------------|
| **F1** | **Mejorar la experiencia de usuario (UI/UX)** | Rediseñar formularios y navegación; agregar confirmaciones visuales y mensajes de error claros. |
| **F2** | **Dashboard unificado para administrativos y coordinación** | Crear un panel que centralice métricas y accesos a TFG, eventos, anuncios y prácticas, reduciendo pasos de navegación. |
| **F3** | **Agregar historial y trazabilidad de cambios** | Incorporar un sistema de *audit log* que registre quién modifica cada registro y cuándo, fortaleciendo la transparencia institucional. |
| **F4** | **Optimizar búsquedas y filtros** | Implementar buscadores dinámicos y filtros avanzados en módulos de anuncios, eventos, profesores y TFG. |

---

Estas mejoras son prioritarias para asegurar la **sostenibilidad técnica** y la **mantenibilidad** del sistema EIEInfo a largo plazo.
