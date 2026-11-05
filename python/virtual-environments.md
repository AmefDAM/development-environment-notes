# Entornos virtuales de Python

> Qué son los entornos virtuales, por qué conviene utilizarlos y cómo
> crearlos y gestionarlos con `venv`.

## 1. Concepto

Un **entorno virtual** es un directorio que contiene una instalación
aislada de Python y los paquetes instalados para un proyecto.

Permite que cada proyecto gestione sus propias dependencias sin
modificar ni depender de los paquetes instalados en otros proyectos o en
la instalación global de Python.

Python incluye el módulo `venv` para crear entornos virtuales. No es
necesario instalarlo mediante `pip`.

## 2. ¿Por qué utilizar un entorno virtual?

Imagina dos proyectos:

-   Proyecto A necesita `requests` en una versión determinada.
-   Proyecto B necesita otra versión de `requests`.

Si ambos utilizan la misma instalación global, actualizar o cambiar una
dependencia para un proyecto puede afectar al otro.

Con entornos virtuales independientes, cada proyecto mantiene sus
propios paquetes.

Ventajas principales:

-   **Aislamiento:** las dependencias de un proyecto no interfieren
    normalmente con las de otro.
-   **Reproducibilidad:** facilita instalar en otro equipo las
    dependencias que necesita el proyecto.
-   **Orden:** evita llenar la instalación global de Python con paquetes
    de proyectos distintos.
-   **Mantenimiento:** permite eliminar el entorno y reconstruirlo sin
    borrar el código del proyecto.

Un entorno virtual no aísla completamente el proyecto ni instala
necesariamente una versión independiente del intérprete: normalmente
utiliza la instalación base de Python con la que se creó.

## 3. Ubicación y nombre

Es habitual crear el entorno dentro de la carpeta raíz del proyecto y
llamarlo `.venv`:

``` text
mi-proyecto/
├── .venv/
├── src/
├── tests/
├── README.md
└── .gitignore
```

El punto inicial hace que `.venv` sea un directorio oculto en sistemas
Unix y macOS. En Windows no implica necesariamente que se oculte en el
Explorador.

`venv`, `.venv` y `env` son nombres posibles. `.venv` es una convención
extendida y suele ser reconocido automáticamente por herramientas como
VS Code.

## 4. Crear un entorno virtual

Primero, abre una terminal en la carpeta raíz del proyecto.

### Windows

Con el lanzador de Python:

``` powershell
py -m venv .venv
```

También puede utilizarse:

``` powershell
python -m venv .venv
```

### Linux y macOS

``` bash
python3 -m venv .venv
```

En algunos sistemas, el comando disponible también puede ser `python`.

### ¿Qué hace el comando?

-   `python` o `py`: ejecuta el intérprete de Python.
-   `-m`: ejecuta un módulo como programa.
-   `venv`: indica que se quiere utilizar el módulo de creación de
    entornos virtuales.
-   `.venv`: nombre y ubicación del directorio que se creará.

Si el directorio ya existe, `venv` puede reutilizarlo y modificar su
contenido. Para empezar desde cero, elimina primero el entorno anterior.

## 5. Activar el entorno virtual

La activación modifica las variables y rutas de la sesión de terminal
para que los comandos `python` y `pip` apunten al entorno virtual.

### Windows --- PowerShell

``` powershell
.\.venv\Scripts\Activate.ps1
```

### Windows --- CMD

``` bat
.venv\Scripts\activate.bat
```

### Linux y macOS --- Bash o Zsh

``` bash
source .venv/bin/activate
```

Cuando se activa correctamente, normalmente aparece el nombre del
entorno al principio de la línea de comandos:

``` text
(.venv) PS C:\ruta\mi-proyecto>
```

La activación afecta a esa sesión de terminal. No activa el entorno en
todas las terminales ni configura automáticamente todos los editores.

### Si PowerShell bloquea la activación

En algunos equipos, la política de ejecución de PowerShell impide
ejecutar el script de activación.

Una alternativa es utilizar CMD o seleccionar el intérprete desde VS
Code. También puede ajustarse la política para el usuario actual, si se
tiene autorización y se comprende el alcance:

``` powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

No cambies políticas de seguridad de un equipo administrado sin
consultar antes con su administrador.

La activación no es imprescindible para utilizar el entorno: se puede
ejecutar directamente el intérprete situado dentro de `.venv`.

## 6. Comprobar qué intérprete se está utilizando

Con el entorno activado:

``` bash
python --version
```

Para localizar el ejecutable:

Windows:

``` powershell
where.exe python
```

Linux y macOS:

``` bash
which python
```

La ruta debería apuntar al directorio `.venv`.

También se puede consultar desde Python:

``` bash
python -c "import sys; print(sys.executable)"
```

Esto permite comprobar qué ejecutable se ha utilizado realmente.

## 7. Desactivar el entorno virtual

``` bash
deactivate
```

El comando desactiva el entorno en la terminal actual. No elimina el
directorio ni los paquetes instalados.

## 8. Eliminar un entorno virtual

Un entorno virtual puede eliminarse borrando su directorio. Primero
conviene desactivarlo y cerrar las terminales o procesos que lo estén
utilizando.

Windows --- PowerShell:

``` powershell
Remove-Item -Recurse -Force .venv
```

Linux y macOS:

``` bash
rm -rf .venv
```

**Precaución:** estos comandos eliminan el directorio indicado.
Comprueba la ruta antes de ejecutarlos.

El código fuente del proyecto no se elimina si está fuera de `.venv`.
Después se puede crear un entorno nuevo e instalar de nuevo las
dependencias.

## 9. Buenas prácticas

-   Crear un entorno virtual por proyecto, especialmente cuando sus
    dependencias sean diferentes.
-   Utilizar un nombre convencional como `.venv`.
-   No incluir el entorno virtual en Git.
-   Registrar las dependencias del proyecto en un archivo, por ejemplo
    `requirements.txt`.
-   Crear el entorno con la versión de Python compatible con el
    proyecto.
-   No copiar un entorno virtual entre equipos o sistemas operativos:
    normalmente es preferible reconstruirlo.
-   No instalar paquetes en el entorno global por costumbre cuando se
    está trabajando en un proyecto.

## 10. Problemas habituales

  -----------------------------------------------------------------------
  Problema                            Posible causa o solución
  ----------------------------------- -----------------------------------
  `python` no se reconoce             Python no está en PATH o el comando
                                      disponible es `py` (Windows) o
                                      `python3` (Linux).

  No se encuentra `venv`              En algunas distribuciones Linux hay
                                      que instalar el paquete del sistema
                                      que proporciona `venv`.

  PowerShell bloquea `Activate.ps1`   Política de ejecución; probar CMD o
                                      revisar la política con los
                                      permisos adecuados.

  Se instala un paquete en el lugar   Comprobar que el entorno está
  equivocado                          activo y consultar
                                      `sys.executable`.

  VS Code no detecta `.venv`          Seleccionar manualmente el
                                      intérprete desde
                                      `Python: Select Interpreter`.

  El entorno deja de funcionar tras   Recrear el entorno en su nueva
  mover el proyecto                   ubicación.
  -----------------------------------------------------------------------

## Referencias

-   [Python --- `venv`](https://docs.python.org/3/library/venv.html)
-   [Python Packaging User Guide --- Creating and using virtual
    environments](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)
