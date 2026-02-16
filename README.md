## Demos, practicas en serverless framework


## GitHub Actions y Configuración de Repositorio

### Configurar un GitHub Actions básico
- Crear archivos de workflow en `.github/workflows/`
- Definir triggers (push, pull_request, schedule)
- Especificar jobs y steps para CI/CD
- Usar acciones reutilizables de GitHub Marketplace

### Proteger una rama específica
- Ir a Settings → Branches → Add rule
- Especificar el patrón de rama (ej: `main`, `develop`)
- Requerir pull request reviews antes de merge
- Descartar cambios stale cuando hay nuevos commits

### Configurar que no puede eliminarse una rama
- En Settings → Branches → Branch protection rule
- Habilitar "Restrict who can push to matching branches"
- Habilitar "Allow deletions" solo para administradores
- O deshabilitar completamente con "Restrict deletions"

### Construir una imagen Docker y guardarla en AWS
- Usar Amazon ECR (Elastic Container Registry)
- Configurar credenciales AWS en GitHub Secrets
- Utilizar acciones como `aws-actions/configure-aws-credentials`
- Construir imagen con `docker build` y pushear a ECR con `docker push`

### Configurar approvals dentro de un GitHub Actions
- En el workflow, usar el step `environment` con protecciones
- Requerir aprobadores en Settings → Environments
- Los approvers deben ser miembros del equipo
- Configurar tiempo de espera para approval (timeout)

### Verificar los tipos de cuenta GitHub de cada uno
- Revisar Settings → Billing & Plans para el tipo de cuenta
- Validar permisos de cada miembro en la organización
- Usar `gh api` CLI para auditar roles: `gh api /orgs/{org}/members`
- Documentar permisos necesarios por rol (Admin, Maintainer, Developer)

### Descripción del workflow `.github/workflows/demo.yml`

Este repositorio incluye un workflow de demostración en `.github/workflows/demo.yml` para ilustrar cómo funcionan los triggers y jobs básicos en GitHub Actions. Resumen:

- Triggers:
  - `push`: se ejecuta automáticamente al hacer push a cualquier rama.
  - `workflow_dispatch`: permite ejecutar el workflow manualmente desde la interfaz de GitHub.

- Jobs definidos:
  - `job-demo`: muestra ejemplos de pasos útiles para depuración y contexto:
    - Imprime un mensaje indicando qué evento disparó el workflow.
    - Muestra la fecha (`date`), el directorio actual (`pwd`) y el usuario (`whoami`).
  - `job-build`: simula una etapa de build con un mensaje placeholder.
  - `job-context`: muestra variables/contexto de GitHub (`echo ${{ github }}`) para entender la información disponible en el runner.

Uso rápido:

- Para ejecutarlo automáticamente, haz push a la rama donde trabajas.
- Para ejecutarlo manualmente, ve a Actions → selecciona "GHA demo" → "Run workflow".

Notas:

- Este workflow es una plantilla demostrativa; reemplaza los pasos de build por comandos reales (instalación de dependencias, tests, compilación, etc.) según tu proyecto.
- Evita imprimir secretos en logs; usa GitHub Secrets y variables de entorno protegidas para credenciales.
