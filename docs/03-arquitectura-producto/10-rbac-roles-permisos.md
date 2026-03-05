<img width="1733" height="827" alt="RBAC1" src="https://github.com/user-attachments/assets/93df8f31-8163-4aea-93ae-e3a3522022fd" />
<img width="1643" height="511" alt="RBAC2" src="https://github.com/user-attachments/assets/1bfbd4fe-108d-4741-b6f3-110bc93e3ca4" />
<img width="1532" height="377" alt="RBAC3" src="https://github.com/user-attachments/assets/b22bfe85-615f-4639-9d36-6e62110e88b4" />
<img width="1590" height="442" alt="RBAC4" src="https://github.com/user-attachments/assets/a8ca77fd-9b2c-4835-b4f9-1afc5d3a995c" />
<img width="1611" height="347" alt="RBAC5" src="https://github.com/user-attachments/assets/8b30e009-1fac-41ca-8c4b-aacef508e5c5" />
<img width="1547" height="357" alt="RBAC6" src="https://github.com/user-attachments/assets/bf3afd79-1692-43da-95f0-8076262333d6" />
<img width="1556" height="471" alt="RBAC7" src="https://github.com/user-attachments/assets/1bce685a-78ab-481f-9eb1-fcbd63f9337a" />
<img width="1531" height="262" alt="RBAC8" src="https://github.com/user-attachments/assets/1423cee3-be55-44ea-96db-40e9a18dc82d" />
<img width="1582" height="327" alt="RBAC9" src="https://github.com/user-attachments/assets/3afa37ea-880f-4153-b191-b6d8e51289d8" />
# Matriz de Roles y Permisos (RBAC) — Sistema Traductor

## Estado
Borrador

## Objetivo

Este documento describe el **modelo de control de acceso basado en roles (RBAC)** utilizado en el sistema **Traductor**, una aplicación de **traducción asistida por inteligencia artificial con arquitectura local-first**.

El objetivo del RBAC es definir:

- Qué **roles existen en el sistema**
- Qué **acciones puede realizar cada rol**
- Qué operaciones están **permitidas, condicionadas o denegadas**

Esto permite mantener **seguridad, control y claridad en las responsabilidades de cada usuario**.

---

# Contexto del Sistema

El sistema **Traductor** es una aplicación de traducción asistida por IA que funciona con un enfoque **local-first**, lo que significa que:

- Los documentos **no salen del dispositivo del usuario**
- El almacenamiento se realiza **localmente**
- Los modelos de IA pueden ejecutarse **en el dispositivo**
- Los índices vectoriales utilizados para RAG también se generan **localmente**

Esto reduce riesgos de privacidad y garantiza control sobre los datos.

---

# Arquitectura Local-First

Actualmente el sistema funciona **100% local**, lo que implica:

- No requiere conexión a Internet
- Utiliza almacenamiento local (IndexedDB / LocalStorage)
- Mantiene sesión local del usuario
- Los documentos se procesan dentro del dispositivo

### Futuro planeado

En versiones posteriores se planea agregar:

- Google Sign-In opcional
- Backup cifrado en la nube
- Colaboración entre usuarios

---

# Roles del Sistema

El RBAC define cinco roles principales.

## Usuario Invitado
Usuario que aún **no ha iniciado sesión**.

Restricciones:
- No puede acceder a proyectos
- No puede acceder a documentos
- Solo puede iniciar sesión

---

## Usuario Autenticado
Usuario que ha iniciado sesión en el sistema.

Permisos principales:

- crear proyectos
- editar proyectos
- gestionar documentos
- iniciar traducciones
- gestionar glosarios
- utilizar modelos de IA

Este rol representa al **usuario base de la aplicación**.

---

## Administrador del Workspace
Usuario con **permisos administrativos** dentro del sistema.

Puede realizar todas las operaciones del sistema, incluyendo:

- gestión completa de proyectos
- gestión completa de documentos
- administración de modelos de IA
- administración de glosarios
- gestión de índices de contexto

Este rol tiene **control total sobre el workspace local**.

---

## Traductor / Editor
Usuario que trabaja activamente en la **traducción de documentos**.

Permisos principales:

- iniciar traducciones
- seleccionar modelos de IA
- importar archivos
- editar documentos
- gestionar glosarios
- crear versiones de documentos

Este es el **actor principal del sistema**.

---

## Usuario Viewer
Usuario con acceso **solo lectura**.

Puede:

- ver documentos
- ver proyectos
- ver estado de traducciones
- acceder a archivos locales exportados

No puede:

- modificar documentos
- iniciar traducciones
- crear proyectos
- editar glosarios

---

# Interpretación de la Matriz RBAC

La matriz utiliza tres tipos de estados de permiso:

✔ **Permitido**  
El rol puede ejecutar la acción sin restricciones.

✔ (condición) **Permitido con condición**  
El rol puede ejecutar la acción bajo ciertas condiciones.

❌ **Denegado**  
El rol no puede ejecutar la acción.

---

# Dominios de Permisos

Los permisos se agrupan por **dominios funcionales del sistema**.

---

# Gestión de Sesión

Controla la autenticación local del usuario.

Permisos:

- iniciar sesión local
- cerrar sesión

Todos los usuarios autenticados pueden cerrar sesión, mientras que los usuarios invitados solo pueden iniciar sesión.

---

# Gestión de Proyectos

Permite organizar el trabajo de traducción.

Permisos:

- crear proyecto
- editar proyecto
- eliminar proyecto
- ver proyecto

Usuarios autenticados y traductores pueden trabajar con proyectos, mientras que el viewer solo puede visualizarlos.

---

# Gestión de Documentos

Controla la manipulación de documentos dentro de proyectos.

Permisos:

- crear documento
- editar documento
- eliminar documento
- ver documento
- crear nuevas versiones

Los traductores y administradores tienen acceso completo, mientras que los viewers solo pueden visualizar.

---

# Gestión de Archivos Locales

Controla el acceso al almacenamiento local.

Permisos:

- importar archivo
- acceder archivo local
- exportar documento traducido

Esto permite mantener **los documentos dentro del dispositivo del usuario**.

---

# Gestión de Traducción

Representa el núcleo del sistema.

Permisos:

- iniciar traducción
- ver estado de traducción
- cancelar traducción
- seleccionar modelo de IA

Los traductores y administradores tienen acceso completo, mientras que los viewers solo pueden consultar estados.

---

# Gestión de Modelos de IA

Permite controlar qué modelos se utilizan para la traducción.

Permisos:

- seleccionar modelo
- cambiar configuración del modelo

Esto permite ajustar el comportamiento del sistema de traducción.

---

# Gestión de Glosarios

Los glosarios permiten mantener consistencia terminológica.

Permisos:

- crear glosario
- editar glosario
- eliminar glosario
- agregar término
- editar término
- eliminar término

Los traductores pueden administrar términos para mejorar las traducciones.

---

# Gestión de Índices de Contexto

Permite gestionar los índices vectoriales utilizados para RAG.

Permisos:

- crear índice de documento
- actualizar índice
- eliminar índice

Estos índices permiten que el modelo tenga **contexto adicional del documento**.

---

# Importancia del RBAC

El modelo RBAC permite:

- separar responsabilidades entre usuarios
- evitar accesos no autorizados
- proteger documentos y datos sensibles
- organizar las operaciones del sistema

Además, este modelo sirve como base para:

- implementación de permisos en backend
- control de acceso en la interfaz
- futuras funcionalidades colaborativas

---

# Conclusión

La matriz RBAC define claramente qué operaciones puede realizar cada tipo de usuario dentro del sistema Traductor.

Gracias al enfoque **local-first**, el RBAC no solo controla permisos de usuario, sino también el acceso a **datos sensibles almacenados localmente**, asegurando privacidad y control del usuario sobre su información.
