# Development Environment

> Apuntes de referencia sobre la configuración, las herramientas y los
> procedimientos que forman parte del entorno de desarrollo.

## Propósito

Este espacio reúne conocimientos transversales necesarios para preparar
y mantener proyectos de programación. No está dedicado a aprender un
lenguaje concreto ni a documentar el control de versiones en
profundidad.

La organización distingue tres ámbitos:

-   **Python:** creación de entornos virtuales y gestión de paquetes y
    dependencias.
-   **VS Code:** configuración del editor para trabajar con Python.
-   **Git:** exclusión de archivos locales o generados que no deben
    formar parte del repositorio.

## Índice

### Python

-   [Entornos virtuales](python/virtual-environments.md): qué son, por
    qué se utilizan, cómo crearlos, activarlos y eliminarlos.
-   [pip](python/pip.md): instalación, actualización y consulta de
    paquetes.
-   [requirements.txt](python/requirements.md): registro y reproducción
    de las dependencias de un proyecto.

### VS Code

-   [Intérprete de Python](vscode/python-interpreter.md): selección y
    configuración del intérprete utilizado por VS Code.
-   [Extensiones](vscode/extensions.md): registro de extensiones útiles
    para el entorno de desarrollo.

### Git

-   [gitignore](git/gitignore.md): sintaxis, patrones y exclusión de
    archivos del control de versiones.

## Criterio de organización

Estos documentos explican herramientas y procedimientos, no los
fundamentos del lenguaje Python ni el funcionamiento general de Git.

  -----------------------------------------------------------------------
  Tema                                Ubicación
  ----------------------------------- -----------------------------------
  Sintaxis, tipos, estructuras de     Python Fundamentals Notebook
  datos, funciones y clases           

  Ramas, commits, merge, rebase y     GitNotes
  flujo de trabajo Git                

  Entornos virtuales, pip y           `python/`
  dependencias                        

  Configuración de Python en VS Code  `vscode/`

  Extensiones del editor              `vscode/`

  `.gitignore` y archivos locales del `git/`
  proyecto                            
  -----------------------------------------------------------------------

## Convenciones

-   Los ejemplos se centran principalmente en Python y VS Code.
-   Se indican las diferencias entre Windows y Linux cuando afectan a
    los comandos.
-   Se utiliza `.venv` como nombre convencional para los entornos
    virtuales locales.
-   Los comandos se muestran en bloques independientes para facilitar su
    consulta.
-   Las instrucciones pueden variar según la versión de Python, VS Code
    o sus extensiones. Conviene consultar la documentación oficial
    cuando una opción cambie.

## Documentación oficial

-   [Python --- documentación](https://docs.python.org/3/)
-   [Python --- `venv`](https://docs.python.org/3/library/venv.html)
-   [Python Packaging User Guide](https://packaging.python.org/)
-   [pip --- documentación](https://pip.pypa.io/en/stable/)
-   [Visual Studio Code ---
    documentación](https://code.visualstudio.com/docs)
-   [Git --- documentación](https://git-scm.com/doc)
-   [GitHub --- documentación de
    `.gitignore`](https://docs.github.com/en/get-started/git-basics/ignoring-files)
