# Especificación de Reglas y Validaciones — Sistema Traductor

## Estado
Borrador

## Owner
T1 — Product/Tech Analyst

## Objetivo
Definir formalmente las **reglas de negocio** y las **validaciones** de la aplicación Traductor, asegurando la correcta operación del sistema de traducción asistida por IA. 

El documento cubre reglas de acceso, restricciones y validaciones que deben ejecutarse antes de permitir realizar ciertas acciones dentro del sistema.

---

## Convenciones

### Tipos de validaciones
1. **Reglas de Negocio (RB)**: Normas funcionales del sistema, describen lo que *debe* pasar en cada interacción.
2. **Validaciones (VAL)**: Verificaciones técnicas realizadas sobre datos, estados, o condiciones antes de ejecutar una acción.

### Severidad
- **Bloqueante**: La acción no puede continuar si no se cumple la regla/validación.
- **Advertencia**: Permite continuar, pero requiere notificación o corrección.

### Ejecución
- **UI**: Se valida en la interfaz del usuario.
- **Local**: Validación realizada en el dispositivo del usuario (sin depender de la nube).
- **Backend**: Validación en el servidor (si aplica).

---

## 1. Reglas de negocio (RB)

### 1.1 Gestión de sesión

| ID | Regla | Descripción | Severidad |
|---|---|---|---|
| RB-01 | **Autenticación obligatoria** | El usuario debe iniciar sesión para acceder al sistema. No se permite acceso sin autenticación. | Bloqueante |
| RB-02 | **Rol de usuario** | Cada acción está permitida/denegada según RBAC. Solo los usuarios autenticados pueden realizar traducciones o gestionar documentos. | Bloqueante |
| RB-03 | **Cierre de sesión** | El usuario puede cerrar sesión en cualquier momento, lo que eliminará su sesión local. | Bloqueante |

### 1.2 Gestión de documentos

| ID | Regla | Descripción | Severidad |
|---|---|---|---|
| RB-04 | **Importación de documentos** | Solo se pueden importar archivos con formatos compatibles (PDF, DOCX, TXT). | Bloqueante |
| RB-05 | **Documentos por proyecto** | Todos los documentos deben pertenecer a un proyecto. No pueden existir documentos huérfanos. | Bloqueante |
| RB-06 | **Versionado** | Cada documento debe tener un historial de versiones. No se pueden sobrescribir versiones previas sin crear una nueva. | Bloqueante |
| RB-07 | **Eliminación de documento** | Un documento solo puede eliminarse si se confirma la acción. | Bloqueante |

### 1.3 Traducción de documentos

| ID | Regla | Descripción | Severidad |
|---|---|---|---|
| RB-08 | **Selección de idiomas** | El usuario debe seleccionar un idioma de origen y un idioma de destino antes de iniciar la traducción. | Bloqueante |
| RB-09 | **Estado de traducción** | El estado del documento debe ser uno de los siguientes: "en cola", "ejecutándose", "terminado", "fallido". | Bloqueante |
| RB-10 | **Validación de traducción completada** | El sistema solo permite exportar un documento si la traducción está completada y aprobada. | Bloqueante |

### 1.4 Glosarios

| ID | Regla | Descripción | Severidad |
|---|---|---|---|
| RB-11 | **Glosarios por proyecto** | Los glosarios deben estar asociados a un proyecto y no pueden existir glosarios huérfanos. | Bloqueante |
| RB-12 | **Términos duplicados** | No se pueden agregar términos duplicados en el glosario, tanto para el idioma fuente como para el destino. | Bloqueante |
| RB-13 | **Uso de glosarios en traducción** | Los glosarios seleccionados deben aplicarse durante el proceso de traducción para mantener consistencia terminológica. | Bloqueante |

---

## 2. Validaciones (VAL)

### 2.1 Iniciar sesión

| ID | Validación | Dónde | Regla asociada | Si falla | Mensaje sugerido |
|---|---|---|---|---|---|
| VAL-01 | **Campos de inicio de sesión** | UI | RB-01 | Bloqueante | "Por favor, ingresa tus credenciales para continuar." |
| VAL-02 | **Sesión válida** | Local | RB-02 | Bloqueante | "Tu sesión ha expirado, por favor inicia sesión nuevamente." |

### 2.2 Importar documento

| ID | Validación | Dónde | Regla asociada | Si falla | Mensaje sugerido |
|---|---|---|---|---|---|
| VAL-10 | **Tipo de archivo soportado** | UI/Local | RB-04 | Bloqueante | "El archivo debe ser un PDF, DOCX o TXT." |
| VAL-11 | **Tamaño máximo de archivo** | Local | RB-04 | Bloqueante | "El archivo excede el tamaño máximo permitido." |
| VAL-12 | **Documento cargado** | Local | RB-05 | Bloqueante | "Debes asignar el documento a un proyecto antes de cargarlo." |

### 2.3 Crear documento / Versión

| ID | Validación | Dónde | Regla asociada | Si falla | Mensaje sugerido |
|---|---|---|---|---|---|
| VAL-20 | **Título de documento no vacío** | UI | RB-06 | Bloqueante | "El título del documento es obligatorio." |
| VAL-21 | **Nueva versión detectada** | Local | RB-07 | Bloqueante | "Se ha detectado que el documento ha cambiado, se creará una nueva versión." |

### 2.4 Iniciar traducción

| ID | Validación | Dónde | Regla asociada | Si falla | Mensaje sugerido |
|---|---|---|---|---|---|
| VAL-30 | **Documento cargado** | Local | RB-08 | Bloqueante | "Carga un documento antes de traducir." |
| VAL-31 | **Idioma seleccionado** | UI | RB-08 | Bloqueante | "Selecciona el idioma de origen y destino." |
| VAL-32 | **Modelo de IA seleccionado** | UI | RB-09 | Bloqueante | "Selecciona un modelo de IA para la traducción." |

### 2.5 Exportar documento

| ID | Validación | Dónde | Regla asociada | Si falla | Mensaje sugerido |
|---|---|---|---|---|---|
| VAL-40 | **Traducción completada** | Local | RB-10 | Bloqueante | "No se puede exportar hasta que la traducción esté terminada." |
| VAL-41 | **Ruta de exportación válida** | Local | RB-10 | Bloqueante | "La ruta de exportación no es válida. Verifica la carpeta de destino." |

---

## 3. Criterios de Aceptación

### 3.1 Criterios generales

- **CA-01:** Si un usuario sin sesión intenta importar archivo → el sistema lo redirige a iniciar sesión (VAL-01, VAL-02).
- **CA-02:** Si un archivo no es compatible, el sistema debe bloquear la importación y mostrar un mensaje de error (VAL-10).
- **CA-03:** Si el documento tiene cambios, debe crearse una nueva versión antes de permitir que se exporte (VAL-21).
- **CA-04:** Si el usuario no selecciona el idioma de destino, el botón de "Iniciar traducción" debe estar deshabilitado (VAL-31).

---

## 4. Notas de implementación

- Las **validaciones de UI** deben realizarse inmediatamente al recibir la entrada del usuario.
- Las **validaciones locales** se deben hacer en el backend para proteger datos sensibles.
- **Mensajes de error y advertencia** deben ser claros, amigables y orientados a la acción.

---

**Conclusión:**  
Estas reglas y validaciones aseguran que las operaciones dentro de Traductor sean correctas, seguras y consistentes, mejorando la experiencia del usuario y garantizando la privacidad de los datos.
