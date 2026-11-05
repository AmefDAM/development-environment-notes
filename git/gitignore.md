# .gitignore

> Cómo indicar a Git qué archivos y directorios debe ignorar en un
> repositorio.

## 1. Concepto

`.gitignore` es un archivo de configuración de Git que contiene patrones
para indicar qué archivos o directorios deben excluirse del seguimiento
cuando todavía no están siendo seguidos por Git.

Se utiliza para evitar incorporar al repositorio archivos que son:

-   Generados automáticamente.
-   Temporales.
-   Específicos de un equipo o usuario.
-   Dependientes del entorno local.
-   Sensibles y no destinados a publicarse.

Ejemplos habituales en proyectos Python:

-   Entornos virtuales (`.venv/`).
-   Caché (`__pycache__/`).
-   Archivos compilados (`*.pyc`).
-   Archivos locales de variables de entorno (`.env`).

## 2. Ubicación

Lo habitual es crear `.gitignore` en la raíz del repositorio:

``` text
mi-proyecto/
├── .git/
├── .gitignore
├── .venv/
├── src/
└── README.md
```

También pueden existir archivos `.gitignore` en subdirectorios. Sus
patrones se interpretan en relación con la ubicación del archivo que los
contiene.

## 3. Sintaxis básica

### Ignorar un archivo concreto

``` gitignore
config.local
```

Ignora los archivos llamados `config.local` que coincidan con ese patrón
según su ubicación.

### Ignorar un directorio

``` gitignore
.venv/
```

La barra final indica que el patrón representa un directorio.

### Ignorar archivos por extensión

``` gitignore
*.pyc
```

Ignora archivos que terminen en `.pyc`.

### Comodín `*`

``` gitignore
*.log
```

Coincide con cualquier secuencia de caracteres dentro del patrón.

### Comodín `?`

``` gitignore
file?.txt
```

Coincide con un carácter cualquiera en esa posición.

### Comodín `**`

``` gitignore
**/temp/
```

Coincide con directorios llamados `temp` en cualquier nivel.

### Anclar un patrón a la raíz

``` gitignore
/build/
```

La barra inicial hace que el patrón se interprete desde la ubicación del
`.gitignore`.

### Excepciones con `!`

``` gitignore
*.log
!important.log
```

Ignora los archivos `.log`, excepto `important.log`.

Las reglas de excepción tienen limitaciones cuando un directorio padre
está ignorado: Git no puede seguir un archivo dentro de un directorio
ignorado sin permitir también el acceso a ese directorio.

## 4. Ejemplo para un proyecto Python

``` gitignore
# Entorno virtual
.venv/

# Caché de Python
__pycache__/
*.py[cod]

# Archivos de variables de entorno
.env
.env.*

# Excepción para una plantilla sin secretos
!.env.example

# Archivos de distribución
build/
dist/
*.egg-info/

# Configuración local de VS Code
.vscode/
```

Este es un punto de partida, no una plantilla universal.

### ¿Debo ignorar toda la carpeta `.vscode/`?

No necesariamente.

Dentro de `.vscode/` puede haber configuraciones útiles para compartir
con otras personas, por ejemplo:

-   `extensions.json`: recomendaciones de extensiones.
-   `launch.json`: configuraciones de depuración.
-   `settings.json`: ajustes del workspace.

Si se quieren versionar esas configuraciones, no conviene ignorar
indiscriminadamente toda la carpeta.

Se puede optar por ignorar solo los archivos personales o locales que no
deban compartirse.

### ¿Debo ignorar `.env`?

Sí, normalmente se excluyen los archivos que contienen credenciales,
claves o configuraciones privadas.

Una plantilla como `.env.example`, sin secretos reales, puede
versionarse para indicar qué variables necesita el proyecto.

Ignorar un archivo no elimina un secreto que ya se haya publicado. Si
una credencial se expone, hay que revocarla o cambiarla.

## 5. Comprobar por qué se ignora un archivo

``` bash
git check-ignore -v ruta/al/archivo
```

Muestra qué regla de qué archivo `.gitignore` está provocando que se
ignore.

Para mostrar también archivos ignorados en determinadas operaciones de
estado:

``` bash
git status --ignored
```

## 6. Ignorar un archivo que Git ya está siguiendo

`.gitignore` no deja de seguir automáticamente los archivos que ya se
han añadido al índice de Git.

Si un archivo ya está versionado y se quiere dejar de seguirlo sin
borrarlo del disco:

``` bash
git rm --cached archivo
```

Para un directorio:

``` bash
git rm -r --cached directorio/
```

Después hay que confirmar el cambio con un commit.

**Precaución:** `git rm` modifica el índice y, sin `--cached`, también
elimina archivos del directorio de trabajo. Comprueba el comando antes
de ejecutarlo.

## 7. Ignorar archivos solo en el equipo local

Git permite configurar exclusiones que no se comparten con el
repositorio.

Una opción es el archivo:

``` text
.git/info/exclude
```

Su sintaxis es similar a la de `.gitignore`, pero sus reglas son locales
al repositorio y no se versionan.

También existe un archivo global de exclusiones configurado en Git, útil
para ignorar archivos del sistema o del editor en todos los
repositorios.

## 8. Buenas prácticas

-   Mantener `.gitignore` en la raíz del repositorio para las reglas
    generales.
-   Ignorar entornos virtuales, cachés y archivos generados.
-   No ignorar automáticamente archivos que el proyecto necesita para
    funcionar.
-   Revisar las reglas de `.vscode/` antes de excluir toda la carpeta.
-   No guardar secretos en el repositorio.
-   Comprobar con `git check-ignore -v` por qué se ignora un archivo.
-   Recordar que `.gitignore` no afecta a archivos que Git ya está
    siguiendo.

## 9. Problemas habituales

  -----------------------------------------------------------------------
  Problema                            Causa o solución
  ----------------------------------- -----------------------------------
  `.venv` aparece en `git status`     Comprobar que la regla `.venv/`
                                      está bien escrita y que el archivo
                                      `.gitignore` está en una ubicación
                                      adecuada.

  Un archivo ignorado sigue           Puede que ya esté siendo seguido;
  apareciendo en Git                  utilizar `git rm --cached` si se
                                      quiere dejar de seguirlo.

  Una excepción `!` no funciona       Comprobar si algún directorio padre
                                      está ignorado.

  Se ignoran archivos que sí deberían Revisar reglas demasiado generales,
  compartirse                         como `.vscode/` o `*.json`.

  No se sabe qué regla se aplica      Utilizar `git check-ignore -v`.
  -----------------------------------------------------------------------

## Referencias

-   [Git --- gitignore](https://git-scm.com/docs/gitignore)
-   [GitHub --- Ignoring
    files](https://docs.github.com/en/get-started/git-basics/ignoring-files)
-   [Git --- git
    check-ignore](https://git-scm.com/docs/git-check-ignore)
-   [Git --- git rm](https://git-scm.com/docs/git-rm)
