# Intérprete de Python en VS Code

> Cómo seleccionar y configurar el intérprete que Visual Studio Code
> utiliza para trabajar con Python.

## 1. Concepto

Un **intérprete de Python** es el programa que ejecuta el código Python.

Un equipo puede tener varias instalaciones o intérpretes:

-   Una instalación global de Python.
-   Varias versiones de Python.
-   Entornos virtuales diferentes para distintos proyectos.

VS Code necesita saber qué intérprete debe utilizar para ejecutar el
código y ofrecer funcionalidades como análisis, autocompletado y
depuración.

## 2. Extensiones necesarias

Para trabajar cómodamente con Python se recomienda instalar la extensión
oficial **Python**, publicada por Microsoft.

Identificador:

``` text
ms-python.python
```

Esta extensión aporta, entre otras funciones, selección de intérprete,
ejecución y depuración de archivos Python.

Otras extensiones pueden complementar la experiencia. Por ejemplo,
Pylance proporciona análisis de código y autocompletado avanzado.

La extensión Python no instala por sí misma el intérprete de Python en
el equipo: Python debe estar instalado por separado.

## 3. Seleccionar el intérprete

1.  Abre la carpeta del proyecto en VS Code.
2.  Pulsa `Ctrl + Shift + P` para abrir la paleta de comandos.
3.  Busca `Python: Select Interpreter`.
4.  Selecciona el intérprete que corresponde al proyecto.

Si el proyecto utiliza un entorno virtual llamado `.venv`, selecciona el
ejecutable situado dentro de esa carpeta.

Rutas habituales:

Windows:

``` text
.venv\Scripts\python.exe
```

Linux y macOS:

``` text
.venv/bin/python
```

Si no aparece en la lista, utiliza la opción para introducir o buscar
manualmente la ruta del intérprete, o actualiza la lista de entornos
disponibles si la opción está presente en tu versión.

## 4. Detección de entornos virtuales

VS Code puede detectar entornos virtuales de Python en el proyecto y
ofrecerlos como intérpretes disponibles.

Una estructura convencional facilita esa detección:

``` text
mi-proyecto/
├── .venv/
├── main.py
└── README.md
```

Si el entorno se creó después de abrir el proyecto, puede ser necesario
volver a seleccionar el intérprete o actualizar la lista de entornos.

La detección automática no sustituye la comprobación de que se ha
seleccionado el entorno correcto.

## 5. Ejecutar un archivo Python

Abre un archivo `.py` y utiliza la acción de ejecución de Python que
ofrece la extensión, normalmente disponible como **Run Python File**.

También puedes ejecutarlo desde la terminal:

``` bash
python main.py
```

En este segundo caso, el resultado depende del `python` que resuelva la
terminal. Comprueba que la terminal utiliza el entorno esperado.

## 6. Intérprete seleccionado y terminal integrada

Son conceptos relacionados, pero no idénticos:

-   El **intérprete seleccionado** determina el entorno que la extensión
    de Python utiliza para funciones como ejecutar, analizar y depurar
    código.
-   La **terminal integrada** es una sesión de shell independiente en la
    que se ejecutan comandos.

VS Code suele activar automáticamente el entorno seleccionado en
terminales nuevas, si la opción correspondiente está habilitada y la
extensión puede hacerlo.

Si no ocurre:

1.  Comprueba el intérprete seleccionado.
2.  Abre una terminal nueva.
3.  Comprueba si aparece `(.venv)` en el prompt.
4.  Si no está activo, actívalo manualmente con el comando
    correspondiente al sistema operativo.

No des por hecho que una terminal que ya estaba abierta cambiará de
entorno al seleccionar otro intérprete.

## 7. Configuración del proyecto mediante `.vscode/settings.json`

VS Code permite guardar ajustes específicos del workspace dentro de:

``` text
.vscode/settings.json
```

Por ejemplo, algunas configuraciones pueden controlar el comportamiento
de la extensión de Python o de la terminal.

Históricamente se utilizaba `python.defaultInterpreterPath` para indicar
una ruta predeterminada:

``` json
{
    "python.defaultInterpreterPath": "${workspaceFolder}/.venv"
}
```

Esta opción puede ayudar a establecer el intérprete inicial, pero no
fuerza el cambio de un intérprete que ya haya sido seleccionado para el
workspace. La selección efectiva se gestiona mediante VS Code.

Evita añadir ajustes innecesarios. Es preferible compartir solo los que
aporten valor al proyecto.

## 8. Comprobar el intérprete utilizado

En la terminal integrada:

``` bash
python -c "import sys; print(sys.executable)"
```

El resultado debería apuntar al ejecutable del entorno virtual del
proyecto.

También puedes comprobarlo desde un script:

``` python
import sys

print(sys.executable)
print(sys.version)
```

## 9. Problemas habituales

  -----------------------------------------------------------------------
  Problema                            Posible solución
  ----------------------------------- -----------------------------------
  No aparece                          Comprobar que la extensión Python
  `Python: Select Interpreter`        está instalada y habilitada.

  No aparece `.venv`                  Comprobar que el entorno existe y
                                      actualizar la lista de intérpretes.

  VS Code ejecuta otro Python         Volver a seleccionar el intérprete
                                      y comprobar `sys.executable`.

  La terminal no activa `.venv`       Abrir una terminal nueva o activar
                                      el entorno manualmente.

  El editor marca imports como        Comprobar que el intérprete
  inexistentes                        seleccionado es el entorno donde se
                                      instaló el paquete.

  La configuración no cambia el       Seleccionar el intérprete desde la
  intérprete                          paleta de comandos;
                                      `python.defaultInterpreterPath` no
                                      sobrescribe necesariamente una
                                      selección previa.
  -----------------------------------------------------------------------

## Referencias

-   [VS Code --- Python
    environments](https://code.visualstudio.com/docs/python/environments)
-   [VS Code --- Python
    tutorial](https://code.visualstudio.com/docs/python/python-tutorial)
-   [VS Code --- User and workspace
    settings](https://code.visualstudio.com/docs/configure/settings)
-   [Python --- documentación oficial](https://docs.python.org/3/)
