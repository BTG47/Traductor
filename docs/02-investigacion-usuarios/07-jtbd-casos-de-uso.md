<img width="8192" height="1266" alt="User Authentication and-2026-03-04-233815" src="https://github.com/user-attachments/assets/09c12594-f95d-4336-9653-9eb68f147710" />
# Diagrama de Casos de Uso — Sistema Traductor (IA Local)


## Objetivo
Este documento describe el **diagrama de casos de uso del sistema Traductor**, una aplicación de **traducción asistida por inteligencia artificial con arquitectura local-first**.

El propósito del diagrama es mostrar:

- Los **actores del sistema**
- Las **interacciones principales con el sistema**
- Las **funcionalidades principales agrupadas por dominio**
- La relación entre **usuarios y operaciones del sistema**

Este diagrama sirve como referencia para:

- diseño de funcionalidades
- definición de permisos
- documentación de arquitectura
- alineación entre frontend, backend local y modelo de dominio

---

# Contexto del Sistema

**Traductor** es una aplicación diseñada para **traducir documentos utilizando modelos de inteligencia artificial**, manteniendo **todo el contenido sensible en el dispositivo del usuario**.

El sistema sigue un enfoque **local-first**, lo que implica:

- Los documentos se almacenan **localmente**
- El texto fuente y traducido **no se envía a servidores**
- Los índices vectoriales y embeddings se generan **localmente**
- El usuario mantiene control total sobre sus datos

Actualmente el sistema **no utiliza infraestructura en la nube**.

---

# Límite del Sistema

En el diagrama aparece un contenedor llamado:

**Sistema Traductor (IA Local)**

Este representa el **límite del sistema**, dentro del cual se encuentran todos los **casos de uso** que el software ofrece.

Los **actores están fuera de este límite**, ya que representan entidades externas que interactúan con el sistema.

---

# Actores del Sistema

El diagrama incluye los siguientes actores.

## Usuario Invitado
Usuario que aún **no ha iniciado sesión**.

Puede realizar acciones limitadas como iniciar sesión.

---

## Usuario Autenticado
Usuario que ya ha iniciado sesión en el sistema.

A partir de este actor se derivan otros roles especializados.

---

## Traductor / Editor
Actor principal del sistema.

Responsable de:

- traducir documentos
- administrar proyectos
- administrar documentos
- seleccionar modelos de IA
- gestionar contexto del documento
- administrar glosarios

Este actor representa al **usuario que utiliza la aplicación para realizar traducciones**.

---

## Administrador Local
Usuario con permisos adicionales para gestionar configuraciones del sistema.

Responsabilidades principales:

- administrar modelos de IA
- gestionar glosarios
- administrar configuración del sistema
- gestionar contexto documental

---

## Viewer
Usuario con acceso de **solo lectura**.

Puede visualizar resultados pero **no modificar documentos ni iniciar traducciones**.

---

# Agrupación de Funcionalidades

Los casos de uso se agrupan en distintos dominios funcionales.

---

# Gestión de Sesión

Permite controlar el acceso al sistema.

Casos de uso:

- Iniciar sesión
- Validar sesión
- Cerrar sesión

Estos casos de uso permiten controlar **la autenticación del usuario** antes de acceder al resto del sistema.

---

# Proyectos y Documentos

Permite organizar el trabajo de traducción.

Casos de uso:

- Administrar proyectos
- Administrar documentos

Dentro de estas funcionalidades se incluyen acciones como:

- crear proyectos
- editar proyectos
- crear documentos
- editar documentos
- consultar documentos

Los documentos representan el **contenido a traducir**.

---

# Traducción Asistida por IA

Este es el núcleo del sistema.

Casos de uso principales:

- Iniciar traducción
- Seleccionar idiomas
- Seleccionar modelo de IA
- Exportar traducción

### Flujo general

1. El usuario selecciona el documento.
2. Define idioma origen y destino.
3. Selecciona el modelo de IA.
4. Inicia el proceso de traducción.
5. El sistema procesa los segmentos del documento.
6. El usuario puede exportar el resultado final.

---

# Configuración Local

Estas funcionalidades permiten ajustar el comportamiento del sistema.

Casos de uso:

- Administrar glosario
- Administrar modelos IA
- Gestionar contexto documental

---

## Administrar Glosario

Permite crear y modificar **diccionarios personalizados** para mejorar la calidad de traducción.

Incluye acciones como:

- agregar términos
- editar términos
- eliminar términos

---

## Administrar Modelos IA

Permite seleccionar y configurar **modelos de inteligencia artificial** utilizados para traducción.

Esto puede incluir:

- cambiar modelo activo
- ajustar parámetros
- consultar modelos disponibles

---

## Gestionar Contexto Documental

Permite generar y mantener el **índice contextual del documento**.

Este índice se utiliza para:

- mejorar coherencia de traducción
- recuperar contexto durante el proceso de traducción
- implementar técnicas de **RAG (Retrieval Augmented Generation)**

Este proceso se realiza **completamente local**.

---

# Relaciones entre Casos de Uso

El diagrama también muestra dependencias entre casos de uso.

Ejemplos:

**Iniciar traducción** depende de:

- seleccionar idioma
- seleccionar modelo de IA

Esto significa que estas acciones deben ocurrir **antes de ejecutar la traducción**.

---

# Flujo de Interacción Típico

Un flujo típico de uso del sistema es el siguiente:

1. El usuario inicia sesión.
2. Selecciona o crea un proyecto.
3. Importa un documento.
4. Selecciona idioma origen y destino.
5. Selecciona el modelo de IA.
6. Inicia la traducción.
7. Revisa el resultado.
8. Exporta el documento traducido.

---

# Importancia del Diagrama

Este diagrama permite entender rápidamente:

- qué usuarios interactúan con el sistema
- qué operaciones pueden realizar
- cómo se organizan las funcionalidades principales

Además sirve como base para:

- diseño de UI
- definición de permisos (RBAC)
- diseño de APIs locales
- planificación de desarrollo
