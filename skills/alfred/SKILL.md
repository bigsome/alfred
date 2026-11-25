---
name: alfred
description: >
  Asistente documental y de protocolo. Inicializa y mantiene la estructura de documentación (docs/)
  de cualquier proyecto. Gestiona el ciclo de vida de las features coordinado con git, Linear, grill-me y geoffrey.
  Se activa automáticamente al iniciar un proyecto sin carpeta docs/, al recibir el traspaso de geoffrey,
  y obligatoriamente cada vez que el usuario valide una entrega o use frases de cierre ("listo", "perfecto",
  "cerramos", "siguiente tarea", "pasa a otra cosa") tras iteraciones de código, o antes de compactar la sesión.
---

# Alfred — Asistente de Estructuración y Protocolo Documental

Este skill actúa como el mayordomo y asistente técnico del proyecto. Su misión es doble:
1. **Inicializar** una estructura de documentación ("Vault") limpia, modular y de bajo consumo de contexto en proyectos nuevos que carezcan de ella.
2. **Mantener** la integridad de esta documentación a lo largo del ciclo de vida de cada feature, coordinándose con Git, Linear y los procesos de planificación (`grill-me` y `geoffrey`).

---

## Paso 0 — Inicialización de Proyecto (Solo si no existe `docs/`)

Al iniciar sesión en un proyecto, verifica si existe la carpeta `docs/` en la raíz del espacio de trabajo. 

Si **no existe**, debes crearla e inicializar la siguiente estructura de archivos "boilerplate" con su frontmatter YAML correspondiente:

### 1. `docs/INDEX.md` (Mapa del Vault y Estado Vivo)
```markdown
---
id: index
title: "Índice de Documentación y Estado Vivo"
category: meta
layer: context
role_context: "Cualquier rol / Agente IA"
tags: [index, mapa, navegacion, estado-vivo]
related: []
last_updated: "YYYY-MM-DD"
ai_directives:
- "Lee SIEMPRE primero este archivo al abrir una conversación nueva. No cargues otros .md salvo que la tarea dependa de ellos."
---

# Índice de Documentación del Proyecto

Bienvenido al vault de documentación. Este documento sirve de mapa y resumen ejecutivo del estado actual del proyecto.

## Estado Vivo (Contexto Rápido para Agentes)
- **Sprint / Foco Actual:** [Definir objetivo vigente]
- **Últimas 5 tareas cerradas:**
  - *(Ninguna todavía)*
- **Decisiones de arquitectura vigentes:**
  - *(Pendiente de inicializar)*
- **Bloqueos o alertas activas:**
  - *(Ninguno)*

## Estructura del Vault

- [[ROADMAP]] — Estado actual del sprint y metas del proyecto.
- [[BACKLOG]] — Listado priorizado de tareas y features pendientes.
- [[USER_STORIES]] — Historias de usuario y requerimientos de producto.
- [[CHANGELOG]] — Historial de cambios y releases por versión.
- [[ARCHITECTURE]] — Decisiones técnicas, esquemas de bases de datos e infraestructura.
- [[LESSONS]] — Aprendizajes, preferencias del cliente y reglas de prevención de errores.
```

### 2. `docs/ROADMAP.md` (Hoja de Ruta del Proyecto)
```markdown
---
id: roadmap
title: "Roadmap del Proyecto"
category: product
layer: strategy
role_context: "Product Owner / Developer"
tags: [roadmap, sprints, planificacion]
related:
- "[[INDEX]]"
- "[[BACKLOG]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Mantén este documento actualizado marcando las tareas del sprint actual como completadas."
---

# Roadmap del Proyecto

## Sprint Actual
- [ ] Feature 1
- [ ] Feature 2

## Siguientes Hitos (Q1/Q2)
- [ ] Hito A
- [ ] Hito B
```

### 3. `docs/BACKLOG.md` (Listado de Tareas Pendientes)
```markdown
---
id: backlog
title: "Backlog del Proyecto"
category: product
layer: strategy
role_context: "Product Owner / Developer"
tags: [backlog, tareas, backlog-items]
related:
- "[[ROADMAP]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Prioriza las tareas y añade nuevos requerimientos técnicos o de negocio aquí."
---

# Backlog de Desarrollo

## Prioridad Alta
- [ ] Tarea prioritaria 1

## Prioridad Media
- [ ] Tarea 2

## Ideas / Icebox
- [ ] Idea 1
```

### 4. `docs/USER_STORIES.md` (Casos de Uso e Historias de Usuario)
```markdown
---
id: user-stories
title: "Historias de Usuario y Requerimientos"
category: product
layer: requirements
role_context: "Product Owner / Developer"
tags: [user-stories, requerimientos, UX]
related:
- "[[ROADMAP]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Documenta las especificaciones funcionales detalladas de cada feature de usuario aquí."
---

# Historias de Usuario

## US-01: Nombre de la Historia de Usuario
- **Como** [Usuario]
- **Quiero** [Acción]
- **Para** [Beneficio]

### Criterios de Aceptación
- [ ] Criterio 1
- [ ] Criterio 2
```

### 5. `docs/CHANGELOG.md` (Historial de Cambios)
```markdown
---
id: changelog
title: "Historial de Cambios (Changelog)"
category: devops
layer: infrastructure
role_context: "Developer / DevOps"
tags: [changelog, releases, versiones]
related:
- "[[INDEX]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Registra aquí cada release relevante del software."
---

# Historial de Cambios

## [Unreleased]

### Añadido
- Inicialización del proyecto y estructura documental básica.
```

### 6. `docs/ARCHITECTURE.md` (Documentación Técnica)
```markdown
---
id: architecture
title: "Arquitectura Técnica del Proyecto"
category: engineering
layer: architecture
role_context: "Tech Lead / Developer"
tags: [architecture, tech-stack, backend, frontend]
related:
- "[[INDEX]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Actualiza este documento si cambia el stack tecnológico, base de datos o lógica clave."
---

# Arquitectura Técnica

## Stack Tecnológico
- **Frontend**: [Especificar, ej. React / Next.js / HTML & JS]
- **Backend/Base de Datos**: [Especificar, ej. Node.js / PostgreSQL / Supabase]

## Flujos de Datos Core
(Describir el flujo principal utilizando un diagrama de flujo de Mermaid y un breve texto explicativo. Consulta el skill `mermaid` para la sintaxis y diseño).

```mermaid
flowchart TD
    subgraph Cliente
        FE["Frontend (Web/Mobile)"]
    end
    subgraph API
        BE["Backend API"]
    end
    subgraph DB
        Database[(Base de Datos)]
    end
    FE -->|Solicitud API| BE
    BE -->|Query/Persistir| Database
```

## Arquitectura de Datos / Entidades
(Describir el modelo de datos principal mediante un diagrama de entidad-relación (ERD) en Mermaid).

```mermaid
erDiagram
    USUARIOS ||--o{ SESIONES : "tienen"
```
```

### 7. `docs/LESSONS.md` (Aprendizajes y Reglas del Proyecto/Cliente)
```markdown
---
id: lessons
title: "Aprendizajes y Reglas Operativas"
category: meta
layer: context
role_context: "Cualquier rol / Agente IA"
tags: [lessons, reglas, cliente, errores-evitados]
related:
- "[[INDEX]]"
last_updated: "YYYY-MM-DD"
ai_directives:
- "Consulta este archivo antes de diseñar o picar código para no repetir errores pasados ni violar preferencias del cliente."
---

# Aprendizajes y Reglas del Proyecto

## Preferencias de Producto / Cliente
- *(Registrar aquí criterios específicos del cliente o del producto)*

## Errores Evitados y Patrones Técnicos
- *(Registrar aquí soluciones a bugs recurrentes o restricciones de arquitectura)*
```

*Nota: Al crear estos archivos, reemplaza `YYYY-MM-DD` con la fecha actual y pídele al usuario un resumen rápido de la tecnología o negocio para rellenar los valores básicos (como el stack tecnológico en `ARCHITECTURE.md`).*

---

## Paso 1 — Coordinación con la Planificación (`grill-me` y `geoffrey`)

Cuando el usuario requiera planificar una nueva feature relevante o cuando `geoffrey` entregue sus artefactos aprobados:
1. **Ejecuta o apóyate en `grill-me` / `geoffrey`** según corresponda para cerrar la definición funcional y de UX.
2. Consolida las conclusiones creando un archivo de propuesta técnica específico en `docs/` (ej. `docs/PROPOSAL_FEATURE_NAME.md`) o inyecta el diseño en `docs/USER_STORIES.md`, vinculando los artefactos de UX si existen. **Incorpora diagramas de flujo o de secuencia en Mermaid** verificados con el skill `mermaid`.
3. Registra el documento en `docs/INDEX.md`, vincula la feature al `docs/ROADMAP.md` en el sprint actual y sincroniza el estado del ticket en **Linear** (si está conectado).

---

## Paso 2 — Triggers de Actualización Documental (Feature Completada o Cierre de Iteración)

Este paso se dispara automáticamente cuando se completa una feature/fix relevante o cuando el usuario valida el resultado con frases de cierre (*"listo"*, *"perfecto"*, *"cerramos"*, *"siguiente tarea"*):

### A. Actualizar Estado Vivo, Changelog e Historial
- **Estado Vivo (`docs/INDEX.md`):** Añade la tarea recién cerrada al principio de `Últimas 5 tareas cerradas` (manteniendo un máximo de 5 entradas rotativas) y actualiza decisiones de arquitectura o bloqueos si han cambiado.
- **Changelog y Roadmap:** Actualiza `docs/CHANGELOG.md` y marca el ítem como completado en `docs/ROADMAP.md`. Sincroniza el estado en **Linear** si aplica.
- **Arquitectura:** Si los cambios alteran el modelo relacional, endpoints críticos o flujos core, actualiza los diagramas Mermaid en `docs/ARCHITECTURE.md`.
- **Aprendizajes (`docs/LESSONS.md`):** Si durante la iteración el usuario corrigió un patrón, marcó una preferencia específica o se resolvió un fallo sutil, añade una línea breve en `docs/LESSONS.md`.
- **Idiomas:** Si el proyecto tiene localización activa (i18n), verifica que las claves nuevas estén registradas.

### B. Generar el Mapa de Archivos e Integración de Código
- **Cómo detectar los archivos:** Ejecuta un comando de Git (`git status --porcelain` o `git diff --name-only main` / rama base) para identificar exactamente qué archivos de código han sido creados o modificados.
- **Filtro de exclusión (CRÍTICO):** Excluye de la lista cualquier archivo dentro de la carpeta `docs/` (`docs/**`), artefactos temporales del agente (`task.md`, `walkthrough.md`, `implementation_plan.md`) y archivos irrelevantes. Esto evita autorreferencias infinitas.
- **Formateo de enlaces:** Convierte la lista filtrada de archivos en enlaces absolutos locales clickables en tu editor utilizando el formato `file:///` (ej. `[MiComponente.jsx](file:///absolute/path/to/src/components/MiComponente.jsx)`).
- **Dónde inyectarlo:** Al final del archivo `.md` específico de la feature (si se creó en el Paso 1) o bajo la sección correspondiente en `docs/USER_STORIES.md`.
- **Formato esperado:**
  ```markdown
  ## Implementación y Código

  ### Archivos Implicados
  - [NombreArchivo.ext](file:///absolute/path/to/archivo) — Rol/cambio realizado.

  ### Contratos y APIs (si aplica)
  - `POST /api/mi-endpoint` (Descripción del contrato de API o esquema de base de datos).
  
  *(Nota: NO incrustar bloques de código de implementación completos para evitar duplicación y desactualización rápida. Usa enlaces locales y resúmenes de contratos en su lugar).*
  ```

---

## Paso 3 — Lo que NO debe hacerse

- No crees ningún documento `.md` en `docs/` sin su frontmatter YAML canónico (`id`, `title`, `category`, `layer`, `role_context`, `tags`, `related`, `last_updated`, `ai_directives`).
- No dupliques código fuente en los documentos `.md`; usa enlaces locales `file:///` y resúmenes de contratos.
- No cargues ni leas todos los archivos de `docs/` al arrancar una tarea: empieza siempre por `docs/INDEX.md` y `docs/LESSONS.md`.

---

## Paso 4 — Comprobación de Integridad y Protocolo Pre-Compactación

Antes de dar por concluida la sesión de trabajo, cerrar una tarea o **antes de ejecutar cualquier compactación de contexto (`/compact`)**, ejecuta esta verificación rápida:
- [ ] Todos los nuevos documentos en `docs/` tienen frontmatter YAML canónico completo.
- [ ] `docs/INDEX.md` tiene actualizada la sección `Estado Vivo` (últimas 5 tareas) y los enlaces del vault.
- [ ] Si se completó una feature o fix, se han actualizado `docs/CHANGELOG.md`, `docs/ROADMAP.md` y Linear.
- [ ] Se ha inyectado la sección `## Implementación y Código` con enlaces `file:///` clickables respetando los filtros de exclusión.
- [ ] Si hubo correcciones o reglas nuevas del usuario/cliente, se han anotado en `docs/LESSONS.md`.
- [ ] El campo `last_updated` de los documentos modificados tiene la fecha actual (`YYYY-MM-DD`).
