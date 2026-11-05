# requirements.txt y dependencias

> Cómo registrar las dependencias de un proyecto Python y reconstruirlas
> en otro entorno.

## 1. Concepto

Un proyecto Python puede depender de paquetes que no forman parte de la
biblioteca estándar del lenguaje.

Por ejemplo, un proyecto puede necesitar `requests` y `pandas`. Para que
otra persona pueda ejecutarlo, necesita instalar las dependencias
compatibles.

Un archivo `requirements.txt` es un archivo de texto que suele contener
especificaciones de paquetes que `pip` debe instalar.

Ejemplo:

``` text
requests==2.32.3
pandas>=2.2
```

El archivo puede llamarse de otra manera, pero `requirements.txt` es una
convención muy extendida.

## 2. Dependencias directas y transitivas

-   **Dependencia directa:** paquete que el proyecto utiliza
    explícitamente.
-   **Dependencia transitiva:** paquete que necesita otra dependencia
    para funcionar.

Por ejemplo, si el proyecto utiliza directamente el paquete A y A
necesita B, B es una dependencia transitiva del proyecto.

Esta distinción importa porque registrar absolutamente todo lo instalado
en un entorno no siempre equivale a describir de forma limpia las
dependencias directas del proyecto.

## 3. Generar requirements.txt con pip freeze

Con el entorno virtual activado:

``` bash
python -m pip freeze > requirements.txt
```

`pip freeze` muestra los paquetes instalados y sus versiones, en un
formato que puede utilizarse como entrada de instalación para `pip`.

El operador `>` redirige la salida a un archivo. Si el archivo ya
existe, su contenido se sobrescribe.

Ejemplo de salida:

``` text
certifi==2024.8.30
charset-normalizer==3.4.0
idna==3.10
requests==2.32.3
urllib3==2.2.3
```

En este ejemplo, algunos paquetes pueden ser dependencias de `requests`,
no paquetes utilizados directamente por el código del proyecto.

**Importante:** `pip freeze` registra lo instalado en el entorno actual;
no determina por sí solo cuáles son las dependencias directas ni crea un
archivo de bloqueo completo con todas las garantías de otras
herramientas de gestión.

## 4. Instalar dependencias desde requirements.txt

Después de crear y activar un entorno virtual:

``` bash
python -m pip install -r requirements.txt
```

`-r` indica a `pip` que lea los requisitos desde el archivo
especificado.

Esto permite reconstruir un entorno de trabajo en otro equipo o después
de eliminar el entorno anterior.

## 5. Actualizar el archivo

Cuando se añadan, eliminen o actualicen dependencias, hay que revisar el
archivo para que refleje las necesidades del proyecto.

Se puede volver a generarlo:

``` bash
python -m pip freeze > requirements.txt
```

Pero conviene revisar el resultado antes de incorporarlo al repositorio,
porque puede incluir paquetes instalados para tareas puntuales o
dependencias que no son directas.

## 6. Especificadores de versión

Ejemplos habituales:

``` text
requests==2.32.3
pandas>=2.2
pytest>=8,<9
package!=1.4.0
```

  Especificador   Significado
  --------------- ----------------------------
  `==`            Versión exacta.
  `>=`            Versión igual o superior.
  `<=`            Versión igual o inferior.
  `>`             Versión superior.
  `<`             Versión inferior.
  `!=`            Excluye una versión.
  `~=`            Compatibilidad aproximada.

Fijar versiones exactas puede facilitar la reproducción de un entorno,
aunque también puede dificultar recibir actualizaciones. Elegir
restricciones amplias o estrictas depende de las necesidades del
proyecto.

## 7. Organización de archivos de dependencias

Para proyectos pequeños puede bastar con un único `requirements.txt`.

En proyectos mayores pueden separarse las dependencias, por ejemplo:

``` text
requirements.txt
requirements-dev.txt
```

El segundo podría incluir herramientas necesarias durante el desarrollo
y las pruebas, como `pytest` o `ruff`.

Un archivo puede referenciar otro:

``` text
-r requirements.txt
pytest
ruff
```

Así se instalan las dependencias principales y las de desarrollo.

No es necesario adoptar esta separación en todos los proyectos.

## 8. Flujo habitual de trabajo

1.  Crear el proyecto.
2.  Crear el entorno virtual.
3.  Activar el entorno.
4.  Instalar las dependencias necesarias.
5.  Desarrollar y probar el proyecto.
6.  Actualizar y revisar el archivo de dependencias.
7.  Incluir el archivo en Git.
8.  Excluir `.venv/` de Git.

Para reconstruir el entorno:

``` bash
python -m venv .venv
```

Activarlo según el sistema operativo y después:

``` bash
python -m pip install -r requirements.txt
```

## 9. Buenas prácticas y limitaciones

-   Versionar `requirements.txt` cuando sea necesario para instalar el
    proyecto.
-   No versionar la carpeta `.venv`.
-   Generar el archivo desde el entorno correcto.
-   Revisar el resultado de `pip freeze` antes de guardarlo.
-   No confundir `requirements.txt` con el código fuente ni con el
    propio entorno virtual.
-   Recordar que la compatibilidad también puede depender de la versión
    de Python, del sistema operativo y de otras herramientas externas.
-   Para proyectos con requisitos de resolución y bloqueo más avanzados,
    valorar herramientas especializadas de gestión de dependencias.

## Referencias

-   [pip --- Requirements File
    Format](https://pip.pypa.io/en/stable/reference/requirements-file-format/)
-   [pip --- `freeze`](https://pip.pypa.io/en/stable/cli/pip_freeze/)
-   [Python Packaging User Guide](https://packaging.python.org/)
