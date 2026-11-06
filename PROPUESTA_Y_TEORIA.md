# Segunda actividad de autoaprendizaje

**Estudiante:** Carolina Lohrmann  
**Asignatura:** Desarrollo web  
**Proyecto:** Registro Salud - sitio estático académico  
**Plataforma propuesta:** GitHub  
**Fecha:** 5 de noviembre de 2026

## 1. Investigación teórica

### Git local y repositorio remoto

Git es un sistema de control de versiones distribuido que registra cambios en el equipo de trabajo: conserva commits, ramas y el historial para comparar o recuperar versiones. GitHub es una plataforma web que aloja repositorios Git y añade herramientas de colaboración, como incidencias, revisión de cambios, permisos y automatización. El repositorio remoto es la copia alojada en un servidor; permite respaldar commits y compartirlos con otras personas.

| Elemento | Git local | GitHub remoto |
|---|---|---|
| Dónde vive | En el equipo, dentro de `.git` | En servidores de GitHub |
| Para qué sirve | Crear commits, ramas y revisar el historial local | Compartir commits, colaborar y publicar el sitio |
| Requiere Internet | No para operaciones locales | Sí para sincronizar y colaborar |
| Ejemplos | `git add`, `git commit`, `git switch` | `git push`, Pull Request, GitHub Pages |

### Comandos de sincronización

- `git remote -v` muestra los remotos configurados. `git remote add origin <URL>` vincula el repositorio local con la URL remota usando el alias `origin`.
- `git push -u origin main` envía commits de la rama local `main` a GitHub y configura su rama de seguimiento para los siguientes envíos.
- `git fetch origin` descarga referencias y commits remotos, pero no los integra por sí solo en la rama activa.
- `git pull origin main` descarga los cambios de `main` e intenta integrarlos en la rama local activa mediante merge o rebase, según la configuración.
- `git clone <URL>` crea una copia local completa de un repositorio remoto y configura el remoto de origen.

### Pull Request y revisión de código

Un Pull Request (PR) propone integrar una rama de trabajo en otra, por ejemplo `feature/despliegue` en `main`. En la página del PR se comparan los cambios, se conversa sobre el código, se pueden dejar comentarios y sugerir correcciones. Tras revisar la pestaña **Files changed**, una persona revisora puede aprobar, solicitar cambios o comentar. Al integrar el PR, la rama destino recibe los commits aprobados. Este proceso deja un registro visible de la revisión.

### Autenticación SSH y PAT

Con SSH, el equipo conserva una clave privada y GitHub recibe únicamente la clave pública asociada a la cuenta. La clave privada no se debe compartir. Para HTTPS puede usarse un Personal Access Token (PAT) en lugar de una contraseña; el token se crea con permisos limitados y se guarda en un gestor de credenciales. No se debe escribir un token dentro del repositorio, README ni capturas. Para esta práctica se recomienda SSH si ya existe una clave configurada; de lo contrario, HTTPS mediante Git Credential Manager evita exponer el token en los comandos del historial.

### GitHub Pages

GitHub Pages publica archivos web estáticos (HTML, CSS, JavaScript e imágenes) desde un repositorio. En este proyecto se usa GitHub Actions: un flujo descarga el código de `main`, prepara los archivos como artefacto y los publica en Pages. El sitio se actualiza cuando un cambio ya integrado llega a `main`. Pages no ejecuta un servidor de aplicaciones ni guarda datos de pacientes; el formulario de este prototipo no almacena ni envía información.

## 2. Propuesta de flujo remoto

- **Proyecto:** Registro Salud, prototipo de formularios HTML y CSS.
- **Repositorio público:** `web2_remoto_practica`.
- **Rama estable:** `main`, con la versión que se publicará.
- **Rama de mejora:** `feature/despliegue`, para agregar `README.md` y documentar el sitio.
- **Integración:** abrir un Pull Request de `feature/despliegue` a `main`, describir el cambio, revisar los archivos, aprobar e integrar.
- **Despliegue:** seleccionar **Settings → Pages → Build and deployment → GitHub Actions**. El workflow `.github/workflows/pages.yml` publica el contenido de `main`.
- **Mantenimiento:** realizar cada mejora en una rama nueva, sincronizarla con `origin`, revisar el PR e integrar antes de publicar.

## 3. Implementación y comandos

El repositorio local contiene la portada, la pantalla de acceso, el formulario de ejemplo y un listado vacío. Los registros personales de demostración se retiraron para evitar publicar información que parezca real. El formulario aclara que no almacena ni transmite datos.

Después de crear en GitHub un repositorio **público** vacío con nombre `web2_remoto_practica`, copia su URL SSH o HTTPS. En PowerShell, desde la carpeta local del proyecto:

```powershell
git remote add origin <URL_DEL_REPOSITORIO>
git push -u origin main
git switch -c feature/despliegue
git push -u origin feature/despliegue
```

El README se prepara en la rama `feature/despliegue`. Después de abrir e integrar el PR en GitHub, vuelve a `main` y sincroniza:

```powershell
git switch main
git pull origin main
```

Para la autenticación SSH, se puede generar una clave Ed25519 con `ssh-keygen -t ed25519 -C "correo-de-GitHub"`, añadir la clave pública `.pub` a **GitHub → Settings → SSH and GPG keys**, y comprobar la conexión con `ssh -T git@github.com`. Si se usa HTTPS, Git Credential Manager puede abrir el inicio de sesión; si pide contraseña de Git, se usa un PAT y se guarda con el administrador de credenciales, nunca en un archivo del proyecto.

## 4. Enlaces y capturas para completar

- **Repositorio público:** `[PEGAR URL DEL REPOSITORIO]`
- **Sitio publicado:** `[PEGAR URL QUE APAREZCA EN SETTINGS → PAGES]`
- **Captura del Pull Request aprobado e integrado:** `[INSERTAR CAPTURA]`
- **Captura de Settings → Pages con el despliegue activo:** `[INSERTAR CAPTURA]`

Las dos capturas forman parte del entregable solicitado. Deben mostrar el PR con estado aprobado e integrado y la configuración de Pages con su URL. No deben incluir tokens, claves privadas ni datos personales de pacientes.

## Referencias

- Git, documentación oficial: [git-scm.com/docs](https://git-scm.com/docs)
- GitHub Docs, repositorios remotos: [About remote repositories](https://docs.github.com/en/get-started/git-basics/about-remote-repositories)
- GitHub Docs, revisión de Pull Requests: [Review pull requests](https://docs.github.com/en/pull-requests/how-tos/review-pull-requests)
- GitHub Docs, autenticación SSH: [Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- GitHub Docs, publicación con Pages: [Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
