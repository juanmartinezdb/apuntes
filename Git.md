# Sota, Caballo Rey
### Bajar
- `git pull`
### Subir
- `git add .`
- `git commit -m "mensaje"`
- `git push -u origin main`
### Clonar
- `git clone direccionURL`
## Configuración Inicial

Inicializa un nuevo repositorio Git en el directorio actual.

- **`git init`**

Clona un repositorio remoto en tu máquina local.

- **`git clone <URL>`**

Establece tu nombre de usuario para todos los repositorios.

- **`git config --global user.name "Tu Nombre"`**

Establece tu correo electrónico para todos los repositorios.

- **`git config --global user.email "tuemail@example.com"`**

---

## Trabajando con Archivos

Agrega todos los cambios en el directorio actual al área de preparación.

- **`git add .`**

Agrega un archivo específico al área de preparación.

- **`git add <archivo>`**

Muestra el estado actual de los archivos en el repositorio.

- **`git status`**

Confirma los cambios en el área de preparación con un mensaje.

- **`git commit -m "Mensaje del commit"`**

Agrega y confirma cambios en un solo paso (solo para archivos rastreados).

- **`git commit -am "Mensaje del commit"`**

---

## Sincronización con Repositorios Remotos

Añade un repositorio remoto y lo nombra "origin".

- **`git remote add origin <URL>`**

Envía tus commits al repositorio remoto y establece "origin master" como predeterminado.

- **`git push -u origin master`**

Envía los commits al repositorio remoto configurado.

- **`git push`**

Descarga y fusiona cambios desde el repositorio remoto a tu rama actual.

- **`git pull`**

Descarga cambios del repositorio remoto sin fusionarlos.

- **`git fetch`**

---

## Manejo de Ramas

Lista todas las ramas locales.

- **`git branch`**

Crea una nueva rama.

- **`git branch <nombre-rama>`**

Cambia a la rama especificada.

- **`git checkout <nombre-rama>`**

Crea y cambia a una nueva rama.

- **`git checkout -b <nombre-rama>`**

Fusiona la rama especificada en la rama actual.

- **`git merge <nombre-rama>`**

Elimina una rama que ya ha sido fusionada.

- **`git branch -d <nombre-rama>`**

---

## Revertir y Deshacer Cambios

Restablece el repositorio al último commit, descartando cambios locales.

- **`git reset --hard`**

Quita un archivo del área de preparación.

- **`git reset <archivo>`**

Crea un nuevo commit que revierte los cambios de un commit específico.

- **`git revert <commit>`**

Deshace cambios no confirmados en un archivo.

- **`git checkout -- <archivo>`**

---

## Visualización y Búsqueda

Muestra el historial de commits.

- **`git log`**

Muestra el historial de commits en una sola línea por commit.

- **`git log --oneline`**

Muestra diferencias entre archivos no confirmados y el último commit.

- **`git diff`**

Muestra detalles de un commit específico.

- **`git show <commit>`**

---

## Otros Comandos Útiles

Guarda temporalmente cambios no confirmados.

- **`git stash`**

Recupera cambios guardados en el stash.

- **`git stash pop`**

Crea una etiqueta en el commit actual.

- **`git tag <nombre-etiqueta>`**

Elimina un archivo del repositorio y del sistema de archivos.

- **`git rm <archivo>`**

Mueve o renombra un archivo.

- **`git mv <archivo-origen> <archivo-destino>`**