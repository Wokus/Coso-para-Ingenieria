# Proyecto Espotify - Documento de Visión

## Descripción General

Espotify es una plataforma de música que ofrece una experiencia completa para clientes y artistas. Su diseño busca facilitar el acceso a música y contenido de artistas registrados, permitiendo a los clientes disfrutar de una experiencia personalizada y a los artistas gestionar su contenido. El sistema se compone de tres componentes principales: el Servidor Central, la Estación de Trabajo y el Servidor Web, que interactúan para proporcionar una solución integrada de gestión y distribución musical.

## Objetivos del Proyecto

- Facilitar la búsqueda y reproducción de música en línea.
- Permitir a los artistas publicar y monetizar sus álbumes.
- Crear un espacio social donde los usuarios puedan interactuar entre sí.

## 1. Componentes del Sistema

### 1.1 Servidor Central

El Servidor Central actúa como el núcleo de la lógica de negocio y se implementa como una biblioteca que puede ser utilizada por las otras aplicaciones para centralizar la lógica. Es responsable del manejo de usuarios, gestión de contenidos musicales y administración de suscripciones, entre otros.

### 1.2 Estación de Trabajo

Este componente es una aplicación GUI implementada en `Java Swing` que permite al Administrador gestionar los usuarios, géneros musicales, listas de reproducción y otros aspectos del sistema. Sirve como el punto de contacto para tareas administrativas y está diseñada para mantener la seguridad y la integridad de los datos.

### 1.3 Servidor Web

Implementado con `JSP` y `Servlets`, el Servidor Web permite la interacción de los clientes y artistas a través de un navegador web. Accede al Servidor Central para ejecutar la lógica de negocio y garantiza que las operaciones de creación y consulta de contenidos sean realizadas correctamente por los usuarios.

## 2. Funcionalidades Principales

### 2.1 Gestión de Usuarios y Roles

El sistema maneja cuatro roles principales:
- **Administrador del Sistema**: Utiliza la estación de trabajo para gestionar los usuarios y sus perfiles, listas, álbumes y subscripciones, entre otros.
- **Cliente**: Usuario que puede acceder a la plataforma, crear listas de reproducción, seguir a artistas, escuchar temas de álbumes y listas de otros usuarios y suscribirse a la plataforma para poder acceder a descargar de los temas proporcionados por la plataforma, entre otros servicios.
- **Artista**: Usuario que puede registrar álbumes y recibir remuneración por sus reproducciones.
- **Visitante**: Usuario no registrado que puede navegar por el sitio pero no acceder a funcionalidades avanzadas.

### 2.2 Reproducción de Contenidos

Los clientes pueden reproducir canciones en línea, ya sea mediante archivos subidos o enlaces a otras plataformas. Se incluye un reproductor básico para facilitar la escucha desde el sitio web.

### 2.3 Suscripción

La suscripción habilita a los clientes a descargar contenido y obtener otros beneficios. Los tipos de suscripción disponibles son semanal, mensual y anual. Su estado puede cambiar automáticamente basado en la fecha de expiración, y pueden ser modificados por el administrador o el cliente.

### 2.4 Recomendaciones

La plataforma genera recomendaciones basadas en los temas y listas favoritas del cliente, así como en las preferencias de los usuarios seguidos para garantizar una experiencia personalizada para cualquier usuario.

## 3. Requerimientos Funcionales

### 3.1 Gestión de Contenidos Musicales

- **Géneros**: Los géneros musicales pueden organizarse en una jerarquía que define relaciones padre-hijo y son creador por el administrador en la estación de trabajo.
- **Álbumes y Temas**: Los artistas pueden crear álbumes indicando el nombre, año de creación, géneros asociados y temas que lo componen, cada tema tiene una posición en su álbum y una duración.
- **Listas de Reproducción**: Existen dos tipos de listas:
  - *Por Defecto*: Creadas por el Administrador y asociadas a un género.
  - *Particulares*: Creadas por clientes con suscripción activa, pueden ser privadas o públicas y serán compuestas por todos los temas que los mismos deseen.

### 3.2 Casos de Uso Clave (Servidor Web)

- **Alta de Álbum**: El artista registrado crea un nuevo álbum ingresando su nombre, año de creación, géneros aplicables y una imagen opcional. Además, añade los temas del álbum, especificando nombre, duración y ubicación de cada tema.
- **Crear Lista de Reproducción Particular**: El cliente con suscripción vigente crea listas de reproducción particulares, asignándoles un nombre y una imagen opcional. Estas listas pueden ser privadas o públicas.
- **Seguir/Dejar de Seguir a Usuarios**: El cliente sigue o deja de seguir a otros usuarios (clientes o artistas), con lo cual recibe recomendaciones y actualizaciones basadas en las actividades de los usuarios seguidos.
- **Contratar Suscripción**: El cliente selecciona y contrata una suscripción (semanal, mensual o anual), accediendo a funcionalidades avanzadas como descargas y gestión de favoritos.

### 3.3 Casos de Uso Clave (Estación de Trabajo)

- **Alta de Género:** El administrador da de alta nuevos géneros musicales.
- **Crear Lista de Reproducción por Defecto:** El administrador da de alta nuevas listas por defecto, las cuales pertenecen únicamente a un género.
- **Agregar/Quitar Temas a Listas:** Gestión de temas dentro de listas de reproducción por defecto.
- **Consultar Usuario, Álbum, Lista:** El administrador es capaz de visualizar la información de un usuario, un álbum o una lista y todos los temas que la conforman.

### 3.4 Control de Suscripciones

Se controla el estado de las suscripciones de los clientes. El administrador puede actualizar el estado en caso de ser necesario y los clientes pueden renovar o cancelar sus suscripciones a voluntad, actualizando su estado automáticamente en el sistema.

## 4. Requerimientos Especiales

### 4.1 Calidad del Producto

- El sistema debe pasar pruebas automáticas utilizando `JUnit` y lograr un mínimo del 80% de cobertura en sentencias, evaluado con `JaCoCo`. También se incluyen análisis de código estático mediante `PMD` y `CheckStyle`.

### 4.2 Validación y Seguridad en el Servidor Web

- La validación de datos de usuario se realiza tanto a nivel cliente (con `JavaScript`) como en el servidor, garantizando la consistencia y el formato adecuado de los datos.

### 4.3 Verificación de Disponibilidad de Nickname y Correo Electrónico

- Se implementará una verificación automática de disponibilidad de nickname y correo electrónico en el momento de registro utilizando `AJAX`, mostrando un mensaje al usuario en tiempo real.

### 4.4 Multimedios y Manejo de Imágenes

- Cada usuario, álbum o lista puede asociarse con una imagen, mejorando la presentación del contenido en la plataforma. El tamaño y el formato de estas imágenes están estandarizados tanto en la estación de trabajo como en el servidor web.

### 4.5 Diseño de la Interfaz

En la Estación de trabajo: 
- Uso de menús para acceso a funcionalidades.
- Uso de `InternalFrames` para manejar casos de uso.
- Diseño con `ComboBox` y `JTree` para desplegar listas y categorías jerárquicas de géneros.

En el Servidor Web: 
- Navegación clara con un cabezal fijo y acceso rápido a funcionalidades como listas y álbumes.
- Búsqueda accesible en cada página, con filtros por nombre y año de creación.
- Validación de datos en el cliente, con verificación de nickname y correo en tiempo real.
- Uso de pestañas en los perfiles de usuarios para organizar la información en secciones.

### 4.6 Persistencia

- El sistema utilizará `JPA` para la persistencia de datos en una base de datos relacional.

## 5. Análisis de Riesgos

### 5.1 Estación de Trabajo

- Riesgo de Integridad de Datos en Administración: La creación, modificación o eliminación de géneros y listas de reproducción debe garantizar que los datos no se dupliquen o se pierdan accidentalmente.
  - *Mitigación*: Implementación de validaciones de integridad y alertas en el sistema para que el administrador confirme cada cambio crítico.

- Riesgo de Complejidad de Interfaz: La sobrecarga de funcionalidades en la interfaz de la Estación de Trabajo puede dificultar su uso para los administradores.
  - *Mitigación*: Simplificar y estructurar la interfaz con menús claros y organizar los casos de uso en `InternalFrames`, evitando saturar la pantalla de opciones.

- Riesgo de Seguridad de Acceso: Los datos de usuarios, listas y álbumes administrados desde esta estación requieren protección contra accesos no autorizados.
  - *Mitigación*: Establecer autenticación estricta y permisos adecuados para el acceso a la Estación de Trabajo, de manera que solo usuarios autorizados puedan acceder y realizar modificaciones.

### 5.2 Servidor Web

- Riesgo de Autenticación y Control de Sesiones: Si la autenticación no se maneja adecuadamente, usuarios no autorizados podrían acceder a información sensible o realizar acciones en la plataforma.
  - *Mitigación*: Implementación de políticas de autenticación seguras (almacenamiento cifrado de contraseñas y manejo seguro de tokens de sesión) y límite de intentos de inicio de sesión.

- Riesgo de Rendimiento en Búsquedas y Carga de Contenido: Un volumen alto de búsquedas o consultas simultáneas de contenido multimedia podría reducir el rendimiento del sitio.
  - *Mitigación*: Uso de filtros de búsqueda eficientes y una estructura de almacenamiento optimizada, como cachés de resultados y servidores dedicados para el contenido multimedia.

- Riesgo de Violación de Derechos de Autor: La capacidad de subir y compartir música en la plataforma puede derivar en infracciones de copyright si el contenido no es gestionado adecuadamente.
  - *Mitigación*: Establecer políticas claras de derechos de autor y revisar el contenido subido por los usuarios, incluyendo advertencias y procedimientos de revisión para evitar posibles conflictos legales.

- Riesgo de Disponibilidad: Dado que el servidor web estará expuesto a múltiples usuarios, es posible que esté sujeto a ataques de denegación de servicio (DoS) o problemas de disponibilidad.
  - *Mitigación*: Configuración de firewall y sistemas de detección de intrusiones (IDS), junto con políticas de escalabilidad que aseguren la disponibilidad del servidor en caso de alta demanda.

## 6. Planificación

El proyecto se llevará a cabo en varias etapas, comenzando con la implementación de la estacion de trabajo y el servicor centralizado que maneje las funcionalidades principales, posteriormente extendiéndose al servidor web y en el futuro alcanzando características más avanzadas como reproducción vía web y recomendaciones personalizadas.

## 7. Referencias

1. [Link Referenciado 1]()
2. [Link Referenciado 2]()
3. [Link Referenciado 3]()
4. [Link Referenciado 4]()