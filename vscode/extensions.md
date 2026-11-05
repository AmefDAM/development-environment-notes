# Extensiones de VS Code

> Registro de extensiones que amplían las funcionalidades de Visual
> Studio Code.

## 1. Concepto

Las extensiones permiten añadir funcionalidades a VS Code sin que todas
formen parte del editor base.

Pueden proporcionar:

-   Soporte para lenguajes.
-   Autocompletado y análisis estático.
-   Depuración.
-   Integración con herramientas externas.
-   Mejoras en el control de versiones.
-   Visualización y edición de formatos específicos.

No todas las extensiones son necesarias para todos los proyectos.
Conviene instalar las que aporten una utilidad concreta.

## 2. Extensiones para Python

### Python

-   **Publicador:** Microsoft.
-   **Identificador:** `ms-python.python`.
-   **Finalidad:** soporte general para trabajar con Python.

Funciones habituales:

-   Selección de intérprete.
-   Ejecución de archivos Python.
-   Depuración.
-   Integración con otras herramientas del ecosistema Python.

La extensión no instala el intérprete de Python en el sistema.

### Pylance

-   **Publicador:** Microsoft.
-   **Identificador:** `ms-python.vscode-pylance`.
-   **Finalidad:** análisis del código y asistencia de lenguaje para
    Python.

Funciones habituales:

-   Autocompletado.
-   Detección de errores y posibles problemas.
-   Información de tipos.
-   Navegación por símbolos y definiciones.

Pylance trabaja junto a la extensión Python.

### Jupyter

-   **Publicador:** Microsoft.
-   **Identificador:** `ms-toolsai.jupyter`.
-   **Finalidad:** trabajar con notebooks de Jupyter (`.ipynb`) desde VS
    Code.

Funciones habituales:

-   Abrir y ejecutar celdas.
-   Visualizar resultados.
-   Seleccionar kernels.
-   Trabajar con notebooks y código Python.

Un notebook puede utilizar un entorno virtual como kernel, siempre que
esté disponible y correctamente configurado.

## 3. Otras extensiones útiles

### GitLens

-   **Publicador:** GitKraken.
-   **Identificador:** `eamodio.gitlens`.
-   **Finalidad:** ampliar la información disponible sobre el historial
    y los cambios de Git.

Puede mostrar información sobre autores, commits, líneas modificadas y
evolución de archivos.

No sustituye a Git ni es imprescindible para utilizarlo.

## 4. Cómo instalar una extensión

1.  Abre la vista de extensiones con `Ctrl + Shift + X`.
2.  Busca el nombre de la extensión o su identificador.
3.  Comprueba el publicador y la extensión correcta.
4.  Pulsa **Install**.

También se puede instalar desde la terminal con el comando de VS Code:

``` bash
code --install-extension ms-python.python
```

Para desinstalar:

``` bash
code --uninstall-extension ms-python.python
```

## 5. Consultar extensiones instaladas

Desde la terminal:

``` bash
code --list-extensions
```

Para obtener también las versiones:

``` bash
code --list-extensions --show-versions
```

Estos comandos requieren que el comando `code` esté disponible en el
PATH.

## 6. Recomendaciones

-   Instalar extensiones de fuentes confiables.
-   Revisar el publicador, las valoraciones, las actualizaciones y los
    permisos relevantes.
-   Evitar instalar varias extensiones que hacen exactamente lo mismo.
-   Deshabilitar o desinstalar extensiones que ya no se utilizan.
-   Revisar la compatibilidad con la versión de VS Code.
-   No confundir una extensión del editor con un paquete de Python
    instalado mediante `pip`.

## 7. Registro personal de extensiones

Este documento también puede utilizarse como inventario. Para añadir una
extensión, se puede mantener esta ficha:

``` text
Nombre:
Publicador:
Identificador:
Finalidad:
Funciones relevantes:
Motivo para utilizarla:
Observaciones:
```

## Referencias

-   [VS Code ---
    Extensions](https://code.visualstudio.com/docs/configure/extensions)
-   [Visual Studio
    Marketplace](https://marketplace.visualstudio.com/vscode)
-   [Python en VS
    Code](https://code.visualstudio.com/docs/python/python-tutorial)
