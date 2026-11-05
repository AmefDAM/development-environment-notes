# pip

> Instalación y gestión de paquetes de Python mediante `pip`.

## 1. Concepto

**pip** es el instalador de paquetes de Python más utilizado. Permite
instalar paquetes publicados en repositorios de paquetes, como PyPI, y
gestionar sus versiones.

Un paquete puede proporcionar funcionalidades que no forman parte de la
biblioteca estándar de Python.

Ejemplos:

-   `requests`: facilita realizar peticiones HTTP.
-   `pandas`: proporciona herramientas para trabajar con datos
    tabulares.
-   `pytest`: permite ejecutar pruebas automatizadas.

`pip` instala paquetes en el entorno asociado al intérprete con el que
se ejecuta. Por eso es importante utilizarlo junto al entorno virtual
correcto.

## 2. ¿Por qué utilizar `python -m pip`?

En lugar de ejecutar directamente:

``` bash
pip install requests
```

es recomendable utilizar:

``` bash
python -m pip install requests
```

Así se ejecuta el módulo `pip` utilizando ese intérprete de Python. Esto
reduce el riesgo de instalar el paquete en un entorno distinto del que
se pretende utilizar.

Si el entorno virtual está activado, `python` debería apuntar al
intérprete de dicho entorno.

## 3. Instalar paquetes

``` bash
python -m pip install requests
```

Instalar varios paquetes:

``` bash
python -m pip install requests pandas pytest
```

Instalar una versión concreta:

``` bash
python -m pip install requests==2.32.3
```

Instalar una versión mínima:

``` bash
python -m pip install "requests>=2.30"
```

Los especificadores de versión permiten expresar restricciones. No todos
significan lo mismo:

-   `==`: versión exacta.
-   `>=`: versión igual o superior.
-   `<=`: versión igual o inferior.
-   `!=`: excluir una versión.
-   `~=`: compatibilidad aproximada según las reglas de versionado de
    Python.

## 4. Desinstalar paquetes

``` bash
python -m pip uninstall requests
```

Para evitar la confirmación interactiva:

``` bash
python -m pip uninstall -y requests
```

Desinstalar un paquete no implica necesariamente eliminar todas las
dependencias que se instalaron junto a él. Comprueba los paquetes
restantes si necesitas limpiar el entorno.

## 5. Actualizar paquetes

Actualizar un paquete:

``` bash
python -m pip install --upgrade requests
```

Actualizar `pip`:

``` bash
python -m pip install --upgrade pip
```

Actualizar paquetes puede introducir cambios de comportamiento o
incompatibilidades. En proyectos existentes conviene revisar y probar
los cambios antes de incorporarlos.

## 6. Consultar paquetes instalados

Mostrar todos los paquetes instalados en el entorno:

``` bash
python -m pip list
```

Mostrar información de un paquete:

``` bash
python -m pip show requests
```

Consultar las dependencias incompatibles o inconsistentes:

``` bash
python -m pip check
```

Buscar paquetes desactualizados:

``` bash
python -m pip list --outdated
```

## 7. Instalar desde otras fuentes

Además de instalar paquetes por nombre desde el índice configurado,
`pip` puede instalar desde otros orígenes.

Por ejemplo, desde un archivo local:

``` bash
python -m pip install ./ruta/al/paquete
```

O desde un repositorio Git:

``` bash
python -m pip install "git+https://github.com/usuario/proyecto.git"
```

Instalar desde repositorios o direcciones no confiables puede ejecutar
código durante el proceso de instalación. Utiliza fuentes de confianza.

## 8. Diferencia entre pip y los módulos de Python

`pip` gestiona la instalación de paquetes; no es el mecanismo que
importa módulos en el código.

Por ejemplo:

``` bash
python -m pip install requests
```

Instala el paquete. Después, dentro del código Python, se importa:

``` python
import requests
```

Instalar un paquete y utilizarlo son operaciones distintas.

## 9. Buenas prácticas

-   Activar el entorno virtual antes de instalar paquetes.
-   Preferir `python -m pip` para asociar claramente `pip` al
    intérprete.
-   Evitar instalar paquetes globalmente si pertenecen a un proyecto
    concreto.
-   Revisar las versiones y compatibilidades antes de actualizar.
-   Registrar las dependencias necesarias para poder reconstruir el
    entorno.
-   No asumir que todos los paquetes instalados en un entorno son
    dependencias directas del proyecto.

## 10. Problemas habituales

  --------------------------------------------------------------------------------------
  Problema                            Posible solución
  ----------------------------------- --------------------------------------------------
  `No module named pip`               Comprobar la instalación de Python y la
                                      disponibilidad de `pip`; consultar
                                      `python -m ensurepip --upgrade` cuando
                                      corresponda.

  `pip` instala en otro entorno       Ejecutar `python -m pip` y comprobar
                                      `python -c "import sys; print(sys.executable)"`.

  Error de permisos                   Comprobar que se está usando un entorno virtual;
                                      evitar recurrir a permisos de administrador sin
                                      necesidad.

  No encuentra una versión            Comprobar el nombre del paquete, la versión de
                                      Python y las restricciones de compatibilidad.

  Conflictos de dependencias          Revisar las restricciones de versiones y probar en
                                      un entorno limpio.
  --------------------------------------------------------------------------------------

## Referencias

-   [pip --- documentación oficial](https://pip.pypa.io/en/stable/)
-   [Python Packaging User Guide](https://packaging.python.org/)
-   [PyPI --- Python Package Index](https://pypi.org/)
