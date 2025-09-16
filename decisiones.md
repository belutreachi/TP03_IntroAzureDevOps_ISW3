# decisiones.md — TP03 Introducción a Azure DevOps

## Contexto
Nuestro equipo debe migrar su proceso de trabajo a Azure DevOps y estructurar un proyecto con seguimiento ágil, code review y políticas de calidad.


## 1. Configuración inicial del proyecto

### Organización y Proyecto
- **Organización**: `belutp` (región: South Brazil)  
  *Justificación:* menor latencia desde Argentina y orden por materia/TP.
- **Proyecto**: `TP3-IntroAzureDevOps`
- **Repositorio**: Git (por integración directa con Pull Requests y políticas de rama).

### Elección de Metodología (Proceso de trabajo)
- **Proceso elegido:** **Scrum (Azure DevOps)**.
- **Por qué Scrum y no Agile/CMMI/Basic:**
  - El TP solicita explícitamente *sprints* y *seguimiento de tareas*. Scrum en Azure DevOps modela esto nativamente con *Product Backlog Items (PBIs)*, *Tasks* y *Sprints*.
  - Facilita el **flujo iterativo** (sprints cortos) y la **inspección/adaptación** en cada cierre.
  - Permite métricas típicas (velocidad, quemado) y tableros preconfigurados alineados a prácticas de Scrum.
  - **Azure Boards** con Scrum trae artefactos y estados simples, lo que reduce fricción para un equipo académico.
- **Implicancias:**
  - Trabajaremos con **PBIs** para representar valor de usuario y **Tasks** para el trabajo técnico.
  - Planificación y revisión por sprint; retrospectivas para mejora continua.
  - Roadmap/Release se gestiona mediante sprint planning y priorización de PBIs.

![alt text](image.png)
![alt text](image-1.png)

### Configuración de equipos

![alt text](image-2.png)

- **Equipos**:
  - `TP3-AzureDevOps Team` (equipo default)
  - `Team-Frontend` → Área por defecto: `TP3-AzureDevOps\App`
  - `Team-Backend` → Área por defecto: `TP3-AzureDevOps\API`
  - `Team-Infra` → Área por defecto: `TP3-AzureDevOps\Infra`
  - `Team-QA` → Área por defecto: `TP3-AzureDevOps\QA`
- **Criterio de diseño**:
  - Las **Áreas** agrupan trabajo por **módulo/componente** para facilitar foco y reportes por disciplina.
  - Cada **Team** tiene un **Default Area Path** para que sus PBIs/Tasks aparezcan en su tablero por defecto.

### Configuración de áreas
**Creación de las subáreas:**
![alt text](image-3.png)

**Asigno un área por equipo:**
Team Backend:
![alt text](image-4.png)
Team Frontend:
![alt text](image-5.png)
Team Infra:
![alt text](image-6.png)
Team QA:
![alt text](image-7.png)


## 2. Gestión del trabajo con Azure Boards

### Creación de un Epic
Epic creado: **Gestión de Usuarios**
![alt text](image-8.png)
![alt text](image-9.png)

### Creación de 3 user stories relacionadas al Epic

Como elegí la metodología Scrum, las User Story no aparecen, por lo que debo usar **Product Backlog Item (PBI)** que es el equivalente en Scrum.

- Epic *Gestión de Usuarios* con los PBI:
  - Registro de nuevos usuarios
  - Autenticación mediante login
  - Administración del perfil del usuario
![alt text](image-10.png)

### Creación de 2 Tasks por cada User Story y 2 bugs de ejemplo

- PBI *Registro de nuevos usuarios* con:
  - Task 1: Diseñar formulario de registro.
  - Task 2: Implementar validaciones de campos.
  - Bug: Error al validar email duplicado.
![alt text](image-11.png)

- PBI *Autenticación mediante login* con:
  - Task 1: Diseñar pantalla de login.
  - Task 2: Implementar autenticación con base de datos.
![alt text](image-12.png)

- PBI *Administración del perfil del usuario* con:
  - Task 1: Crear vista de edición del perfil.
  - Task 2: Implementar actualización de datos en el servidor.
  - Bug: No se guarda la foto de perfil actualizada.
![alt text](image-13.png)

**Estructura de work items y por qué:**
La estructura que definimos en Azure Boards sigue la jerarquía recomendada en Scrum y se adapta a la consigna del TP:
- **Epic**: usamos un Epic (“Gestión de Usuarios”) como contenedor de alto nivel que agrupa funcionalidades completas y de largo plazo.
- **Product Backlog Items (PBI)**: en Scrum los User Stories se representan como PBIs. Cada PBI describe una funcionalidad específica que aporta valor al usuario (ej: “Registro de nuevos usuarios”, “Autenticación mediante login”, “Administración del perfil”).
- **Tasks**: cada PBI se descompone en Tasks técnicas que indican qué trabajo concreto debe realizarse para implementar la funcionalidad (ej: diseñar formularios, programar validaciones, implementar autenticación).
- **Bugs**: añadimos Bugs de ejemplo para reflejar problemas que pueden surgir en la aplicación y que deben ser solucionados dentro del mismo marco de trabajo.

**Justificación:**

Esta estructura permite mantener la trazabilidad y el orden: los Epics muestran la visión global, los PBIs representan necesidades del usuario, las Tasks detallan el trabajo técnico necesario, y los Bugs aseguran la calidad corrigiendo errores. De esta forma, el tablero refleja claramente qué se está construyendo, por qué y cómo.

### Configuración de un Sprint de 2 semanas
Configuramos el Sprint 1 de la fecha 16/09/2025 al 30/09/2025 (dos semanas).
![alt text](image-14.png)
![alt text](image-15.png)

### Asignar los work items al Sprint
Asignamos cada work item al Sprint 1:
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)
En la planificación del Sprint, asignamos a `Sprint 1` los Product Backlog Items (equivalentes a User Stories), junto con sus Tasks y Bugs asociados.  
El Epic “Gestión de Usuarios” no se incluyó en el Sprint ya que, por definición, un Epic abarca múltiples iteraciones y sirve como contenedor de alto nivel.  
De esta forma, el Sprint refleja únicamente el trabajo planificable y ejecutable en dos semanas.


## 3. Control de versiones con Azure Repos

### Importar o crear un repositorio con código de una aplicación
Importo un repositorio vacío creado para este TP:
![alt text](image-19.png)
![alt text](image-20.png)

### Configuración de políticas de branch para la rama principal
Configuramos políticas para la rama principal **main**:
- Requerir Pull Request.
- Mínimo **1** reviewer.
- Vincular Work Items al PR (trazabilidad).
- Merge por **Squash** (historial limpio).
![alt text](image-22.png)
![alt text](image-23.png)

### Creación de ramas
Creamos dos ramas de feature:
1. **`feature/login-ui`** con base en main.
2. **`feature/profile-edit`** con base en main.

![alt text](image-21.png)

### Realizar cambios en cada rama
Desde la rama **`feature/login-ui`**, creo un archivo:
![alt text](image-24.png)
Creo la interfaz de login en el archivo creado:
![alt text](image-25.png)
Subo los cambios:
![alt text](image-26.png)

Desde la rama **`feature/profile-edit`**, creo un archivo:
![alt text](image-30.png)
Creo la edición de perfil en el archivo creado:
![alt text](image-31.png)
Subo los cmabios:
![alt text](image-32.png)

### Crear Pull Requests
- **`feature/login-ui`**
![alt text](image-27.png)
Para que se complete el Pull Request, el otro reviewer tiene que aprobarlo:
![alt text](image-29.png)

- **`feature/profile-edit`**
![alt text](image-33.png)
Para que se complete el Pull Request, el otro reviewer tiene que aprobarlo:
![alt text](image-34.png)

Resultado final al completarse los Pull Requests:
![alt text](image-35.png)


## Problemas encontrados y soluciones aplicadas
- **No aparecía la opción “User Story”** → En Scrum se llaman PBIs. Usamos PBIs como equivalente.
- **Asignación del Epic al Sprint** → No se incluyó, ya que un Epic abarca múltiples iteraciones y no corresponde planificarlo en un Sprint.