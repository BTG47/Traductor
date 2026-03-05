<img width="1360" height="1760" alt="Diagrama de caso de uso (1)" src="https://github.com/user-attachments/assets/be3aad99-bdce-4d66-8567-6522c377abc3" />
# Diagrama de Casos de Uso — Sistema Traductor

## Descripción general

El siguiente diagrama de casos de uso muestra las principales funcionalidades del **Sistema Traductor**, una aplicación diseñada para realizar traducciones asistidas por inteligencia artificial. El sistema permite gestionar documentos, realizar traducciones, y administrar glosarios de términos para mejorar la precisión de las traducciones.

El objetivo del diagrama es representar:

- Los **actores que interactúan con el sistema**
- Las **funcionalidades disponibles**
- Cómo cada actor puede utilizar dichas funciones

El sistema se encuentra representado dentro de un límite llamado **TRADUCTOR**, donde se agrupan todos los casos de uso.

---

# Actores del Sistema

El sistema cuenta con tres tipos principales de usuarios.

## Usuario sin autenticar

Este actor representa a un usuario que aún **no ha iniciado sesión en el sistema**.

Su única interacción posible es:

- **Iniciar sesión**

Una vez autenticado, el usuario puede acceder a las funcionalidades del sistema.

---

## Usuario autenticado (básico)

Este actor representa a un usuario que ya ha iniciado sesión y puede realizar operaciones básicas dentro del sistema.

Entre sus capacidades se encuentran:

- importar archivos
- editar documentos
- exportar documentos traducidos
- ver traducciones
- seleccionar idioma
- crear glosarios
- administrar glosarios

Este usuario puede utilizar las funcionalidades principales del sistema de traducción.

---

## Usuario premium

El **usuario premium** tiene acceso a funcionalidades más avanzadas del sistema, incluyendo la gestión completa de proyectos y documentos.

Entre sus capacidades se encuentran:

- importar archivos
- editar documentos
- exportar documentos con traducción
- eliminar proyectos
- elegir idioma de traducción
- visualizar traducciones
- traducir palabras con definición contextual
- crear y administrar glosarios
- editar documentos

Este tipo de usuario tiene mayor control sobre la gestión de información dentro del sistema.

---

# Casos de Uso del Sistema

Las funcionalidades del sistema se encuentran organizadas en tres grupos principales.

---

# 1. Gestión de Sesión

Permite controlar el acceso al sistema.

Casos de uso:

- **Iniciar sesión**
- **Cerrar sesión**

Estos procesos permiten autenticar al usuario antes de que pueda interactuar con el sistema.

---

# 2. Administración de Documentos

Este conjunto de funcionalidades permite manejar documentos dentro del sistema.

Incluye los siguientes casos de uso:

- **Importar archivo**
- **Editar documento**
- **Exportar documento con traducción**
- **Eliminar proyecto**

Estas acciones permiten al usuario trabajar con documentos que posteriormente serán procesados por el sistema de traducción.

---

# 3. Traducciones

Estas funcionalidades representan el núcleo del sistema.

Casos de uso incluidos:

- **Elegir idioma**
- **Ver traducción**
- **Traducir palabra con su definición contextual**

Estas operaciones permiten que el sistema utilice inteligencia artificial para generar traducciones y mostrar resultados al usuario.

---

# 4. Gestión de Glosarios

Los glosarios permiten mejorar la consistencia terminológica de las traducciones.

Casos de uso:

- **Crear glosario**
- **Administrar glosario**

Esto permite que el sistema mantenga un conjunto de términos personalizados que pueden utilizarse durante el proceso de traducción.

---

# Flujo de uso del sistema

Un flujo típico de uso del sistema sería el siguiente:

1. El usuario abre la aplicación.
2. Si no está autenticado, debe **iniciar sesión**.
3. Una vez dentro del sistema, puede **importar un archivo**.
4. El usuario puede **editar el documento** si es necesario.
5. Selecciona el **idioma de traducción**.
6. El sistema genera la traducción utilizando IA.
7. El usuario puede **visualizar la traducción**.
8. Puede **exportar el documento traducido**.
9. Finalmente puede **cerrar sesión**.

---

# Conclusión

El diagrama de casos de uso permite visualizar de forma clara cómo interactúan los distintos tipos de usuarios con el sistema Traductor.

Este modelo ayuda a:

- comprender las funcionalidades principales del sistema
- definir permisos y niveles de acceso
- estructurar el diseño del software
- servir como base para el desarrollo del sistema
