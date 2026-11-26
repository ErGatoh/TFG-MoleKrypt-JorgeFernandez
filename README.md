<div align="center">

# 🐾 MoleKrypt

### Tu privacidad, tus archivos, tus reglas.

**Plataforma de seguridad y almacenamiento cifrado con galerías privadas y espacios colaborativos.**

![Estado](https://img.shields.io/badge/estado-en%20planificaci%C3%B3n-orange?style=flat-square)
![Proyecto](https://img.shields.io/badge/proyecto-2%C2%BA%20DAM-blue?style=flat-square)
![Plataforma](https://img.shields.io/badge/plataforma-Android-green?style=flat-square)
![Base de datos](https://img.shields.io/badge/base%20de%20datos-PostgreSQL-336791?style=flat-square)

</div>

> **Estado del proyecto:** MoleKrypt es un proyecto de fin de ciclo de **Desarrollo de Aplicaciones Multiplataforma (DAM)**. Este repositorio documentará su diseño y desarrollo incremental. Las funcionalidades descritas representan el alcance previsto y se irán incorporando progresivamente; no implican que estén implementadas en este momento.

## 📖 ¿Qué es MoleKrypt?

MoleKrypt nace con la idea de ofrecer una aplicación Android desde la que proteger, organizar y compartir fotografías y vídeos sin perder el control sobre ellos. Combinará una **bóveda personal cifrada**, **bóvedas compartidas con permisos**, **almacenamiento local y remoto opcional**, y distintas herramientas de organización y seguridad.

El objetivo es que el usuario decida **qué guarda, dónde lo guarda, con quién lo comparte y quién puede modificarlo**. MoleKrypt podrá detectar problemas o recomendar acciones, pero **no eliminará, modificará ni compartirá archivos sin autorización expresa**.

El proyecto también contempla dos áreas web diferenciadas: un **panel personal de estadísticas** y un **panel de administración del servicio**. La aplicación Android será el producto principal para gestionar las bóvedas.

## ✨ Funcionalidades previstas

### 🔒 Personal Vault

La bóveda personal permitirá:

- Importar fotografías y vídeos de forma individual o masiva, navegando por fechas y seleccionando grupos completos para después descartar elementos concretos.
- Organizar y visualizar el contenido desde una galería privada.
- Guardar archivos cifrados localmente y decidir qué contenido se sincroniza con una nube privada.
- Gestionar por separado copias locales y remotas, siempre con confirmaciones para operaciones destructivas.
- Consultar los **metadatos disponibles** de cada fotografía o vídeo desde el propio visor. El análisis estará integrado: **no habrá un apartado independiente de inspección**.
- Añadir comentarios o anotaciones privadas a fotografías.
- Marcar favoritos y utilizar carpetas restringidas, cuya consulta será normal tras acceder a MoleKrypt, pero cuyo borrado exigirá una autenticación adicional.

**No habrá cámara fotográfica integrada.** Las imágenes y los vídeos se importarán desde el dispositivo o mediante las integraciones que permita Android.

### 👥 Shared Vault

Los usuarios podrán crear álbumes privados y compartirlos con otras cuentas de MoleKrypt:

- Invitaciones a miembros y **permisos configurables**: propietario, administrador, colaborador y visualizador, con capacidades individuales.
- Sincronización de nuevas aportaciones para los miembros autorizados.
- **Cuota asociada al propietario**: el espacio compartido se contabilizará en la capacidad de quien crea o financia el álbum, no en la de cada invitado.
- Identificación de quién añadió cada fotografía y cuándo.
- **Historial de actividad**: incorporaciones, retiradas, cambios de miembros y permisos.
- Comentarios privados asociados a fotografías y vídeos.
- **Chat propio de cada Shared Vault, limitado a texto y emojis**: los archivos multimedia se subirán a la bóveda, nunca al chat.
- Solicitudes de fotografías dentro del álbum para pedir aportaciones a otros miembros.

Se contempla a futuro una función opcional de conservación y transferencia autorizada de la propiedad de un álbum (**Legacy**).

### 🔎 Detective integrado

Detective no será una pantalla ni un módulo independiente del menú. Funcionará **dentro de Personal Vault y Shared Vault**:

- Comprobará posibles duplicados al procesar contenido nuevo o modificado.
- Distinguirá archivos idénticos, coincidencias de metadatos e imágenes visualmente similares; **los metadatos iguales por sí solos no prueban que dos fotos sean la misma**.
- Mostrará un aviso discreto en la parte superior cuando haya coincidencias que revisar.
- Permitirá comparar los archivos y elegir qué copias retirar.
- **Nunca eliminará nada automáticamente**. En Shared Vault también respetará los permisos del miembro.

### 🔐 Auth y protección de aplicaciones

MoleKrypt contará con cuentas de usuario, sesiones y métodos de autenticación seguros. Se estudiará la incorporación de biometría del sistema (huella o reconocimiento facial cuando el dispositivo sea compatible) y autenticación multifactor.

La función **MoleKrypt Lock** pretende proteger aplicaciones Android seleccionadas utilizando los métodos de autenticación configurados. Su alcance final dependerá de las restricciones y permisos permitidos por Android.

La única utilización prevista de la cámara dentro de MoleKrypt será la que gestione el sistema para la **autenticación facial compatible**, sin construir una cámara propia ni almacenar fotografías del rostro para ese fin.

### 🔁 MoleKrypt Direct

Se prevé una función de transferencia segura entre dispositivos autorizados, especialmente entre Android y PC, para mover fotografías y vídeos sin depender necesariamente del almacenamiento remoto. El mecanismo y la experiencia concreta en PC siguen en estudio; **el panel web administrativo no sustituye a Direct**.

### ☁️ Almacenamiento híbrido y seguridad

- Almacenamiento local cifrado, con funcionamiento sin conexión para las funciones que lo permitan.
- Sincronización remota **opcional** de archivos cifrados.
- Gestión de cuotas y espacio ocupado.
- Comprobación de la integridad de las transferencias y recuperación de los archivos sincronizados.
- Separación entre autenticación, autorización y gestión de claves.
- Uso previsto de criptografía contrastada, como **AES-256-GCM**, sin inventar un algoritmo propio para proteger datos reales.

El diseño de claves para compartir álbumes cifrados y recuperar el acceso se tratará como una parte esencial de la arquitectura de seguridad.

## 🖥️ Interfaces del proyecto

| Interfaz | Destinatarios | Propósito |
|---|---|---|
| **MoleKrypt Android** | Usuarios | Vault personal y compartida, importación, Detective integrado, autenticación y demás funciones móviles. |
| **Web de usuario** | Cada usuario autenticado | Dashboard personal: cuota, almacenamiento ocupado y libre, distribución por tipos, archivos más grandes, gráficos y estadísticas propias. **También sugerencias de ahorro de espacio, duplicados y copias locales recuperables.** |
| **Web de administración** | Administradores autorizados | Dashboard general, estadísticas del servicio, cuentas, cuotas, volumen de archivos, Shared Vaults y monitorización operativa. **Sin recomendaciones personales de limpieza.** |

La administración del servicio **no debe permitir leer fotografías, vídeos, comentarios ni chats privados de otros usuarios**. El panel trabajará con información operativa autorizada, preservando el cifrado y la privacidad de los contenidos.

## 🧰 Tecnologías previstas

El stack se mantendrá deliberadamente reducido para priorizar la **fluidez de Android**, la mantenibilidad y el aprendizaje. Algunas herramientas siguen siendo candidatas y se confirmarán conforme avance el desarrollo.

| Área | Tecnología | Estado |
|---|---|---|
| Android | **Kotlin + Jetpack Compose** | Propuesta principal |
| Datos locales | Room + SQLite | Propuesta |
| Galería eficiente | Coil + Paging 3 | Propuesta |
| Tareas asíncronas | Kotlin Coroutines + WorkManager | Propuesta |
| Comunicación | Ktor Client | Propuesta |
| Backend | Kotlin + Ktor Server | Propuesta |
| Base de datos central | **PostgreSQL** | **Elegida** |
| Paneles web | SvelteKit + TypeScript | Propuesta |
| Gráficos web | Apache ECharts | Candidato |
| Despliegue | Docker Compose | Propuesta |

No se pretende añadir frameworks por cantidad. Se elegirán las dependencias necesarias para cada función y se medirá su impacto real, especialmente en el móvil. Las fotografías y vídeos cifrados se almacenarán como archivos; PostgreSQL gestionará sus registros y relaciones.

## 🧩 Organización y desarrollo modular

El proyecto seguirá una filosofía de **monorepositorio y desarrollo incremental**. Se plantean áreas diferenciadas para Android, backend, web, base de datos, infraestructura y documentación; las carpetas exactas se ajustarán cuando se cree la base del proyecto.

Cada funcionalidad se desarrollará en cambios pequeños, con criterios de aceptación y pruebas. Por ejemplo, crear un Shared Vault, invitar a un miembro y registrar su actividad serán entregas separadas, no una única tarea gigante.

### 🌿 Estrategia de ramas

| Rama | Función |
|---|---|
| `main` | Versiones estables e identificadas mediante tags, por ejemplo `v0.1.0`, `v0.5.0`, `v1.0.0`. |
| `develop` | Integración de funcionalidades verificadas. |
| `feature/*` | Desarrollo de una mejora pequeña desde `develop`, mediante Pull Request. |
| `fix/*` | Corrección ordinaria de errores. |
| `hotfix/*` | Corrección urgente de una versión publicada. |

Las nuevas features se fusionarán a `develop` después de revisarlas y probarlas. Cuando exista un conjunto estable, se preparará una versión para `main`. GitHub Issues y Pull Requests permitirán documentar qué se ha implementado y por qué.

## 🎯 Objetivos del proyecto

1. Aprender y aplicar tecnologías modernas de desarrollo Android, backend, web y bases de datos.
2. Diseñar un sistema de almacenamiento cifrado con control explícito del usuario sobre sus datos.
3. Incorporar álbumes colaborativos privados con permisos, aportaciones, historial y comunicación sencilla.
4. Ofrecer una experiencia de galería fluida con metadatos y detección integrada de duplicados.
5. Crear paneles web de estadísticas y administración con separación estricta de permisos.
6. Desarrollar el proyecto de forma modular, comprobable y documentada, de cara a su presentación como Proyecto Integrador de DAM.

## 🚧 Estado y próximos pasos

**Proyecto aprobado y en preparación del desarrollo.** Los requisitos funcionales se han trabajado a nivel conceptual, pero todavía no debe interpretarse esta lista como un compromiso cerrado para una versión concreta.

Los siguientes pasos serán concretar la arquitectura, documentar las decisiones de seguridad, preparar la estructura del repositorio y dividir el desarrollo en issues pequeños. El alcance de cada versión dependerá de las pruebas, la viabilidad y el tiempo disponible.

---

<div align="center">

**MoleKrypt** · Proyecto Integrador de 2.º DAM

*Privacidad, organización y colaboración bajo el control del usuario.*

</div>
