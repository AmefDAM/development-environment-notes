# pytest

## ¿Qué es pytest?

[pytest](https://docs.pytest.org/) es un framework de testing para Python que permite escribir y ejecutar pruebas automatizadas.

Facilita la comprobación de funciones y componentes mediante funciones de prueba, `assert` y otras herramientas como fixtures y parametrización.

pytest puede utilizarse para ejecutar pruebas en proyectos que siguen TDD, pero no exige utilizar esa metodología.

## Instalación

Es recomendable instalar pytest en el entorno virtual del proyecto, no globalmente.

Con el entorno virtual activado:

```bash
pip install pytest
```

Para declarar pytest como dependencia de desarrollo en un proyecto configurado mediante `pyproject.toml`, se puede utilizar un grupo de dependencias opcionales:

```toml
[project.optional-dependencies]
dev = [
    "pytest",
]
```

Después se instalan las dependencias de desarrollo con:

```bash
pip install -e ".[dev]"
```

El comando anterior presupone que el proyecto tiene una configuración de empaquetado válida en `pyproject.toml`.

## Convenciones de descubrimiento

Por defecto, pytest busca archivos con nombres como:

- `test_*.py`
- `*_test.py`

Dentro de ellos descubre funciones cuyo nombre comienza por `test_`.

Ejemplo:

```python
def test_add_two_positive_numbers():
    assert 2 + 3 == 5
```

También se pueden organizar pruebas en clases cuyo nombre comienza por `Test`, aunque no es necesario utilizar clases para escribir pruebas con pytest.

## Estructura habitual

En un proyecto Python con estructura `src/`:

```text
mi-proyecto/
├── src/
│   └── mi_proyecto/
│       ├── __init__.py
│       └── operations.py
├── tests/
│   └── test_operations.py
├── pyproject.toml
├── README.md
└── .gitignore
```

- `src/mi_proyecto/`: código de producción.
- `tests/`: pruebas automatizadas.
- `test_*.py`: módulos de pruebas.

La estructura `src/` ayuda a separar el código de producción de los archivos de la raíz del repositorio. Para que las importaciones funcionen correctamente, el proyecto debe estar instalado o configurado para que Python encuentre el paquete.

## Configuración básica en pyproject.toml

Una configuración sencilla para pytest puede ser:

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
```

En un proyecto con estructura `src/`, una opción habitual durante el desarrollo es instalar el paquete en modo editable:

```bash
pip install -e .
```

La configuración de empaquetado debe declarar correctamente el paquete ubicado en `src/`. No es recomendable depender de añadir rutas arbitrarias al entorno si el proyecto puede instalarse de forma adecuada.

## Escribir pruebas

Supongamos que el código de producción está en `src/mi_proyecto/operations.py`:

```python
def add(a, b):
    return a + b
```

La prueba correspondiente puede estar en `tests/test_operations.py`:

```python
from mi_proyecto.operations import add


def test_add_two_positive_numbers():
    assert add(2, 3) == 5


def test_add_positive_and_negative_numbers():
    assert add(5, -3) == 2
```

`assert` comprueba que una condición sea verdadera. Si la condición es falsa, pytest informa de que la prueba ha fallado y muestra información del resultado obtenido y el esperado.

Consulta [Assertions en Python](../../python-fundamentals-notebook/testing/assertions.md) para estudiar la sentencia `assert` como característica del lenguaje.

## Ejecutar las pruebas

Desde la raíz del proyecto:

```bash
pytest
```

Comandos útiles:

```bash
# Mostrar cada prueba y su resultado
pytest -v

# Ejecutar un archivo concreto
pytest tests/test_operations.py

# Ejecutar una prueba concreta por su nombre
pytest -k "test_add_two_positive_numbers"

# Detener la ejecución en el primer fallo
pytest -x

# Mostrar más información de los resultados
pytest -vv
```

## Interpretar los resultados

Los resultados más habituales son:

- `PASSED`: la prueba se ha superado.
- `FAILED`: la prueba se ha ejecutado, pero una comprobación ha fallado.
- `ERROR`: ha ocurrido un error durante la preparación o ejecución de la prueba.
- `SKIPPED`: la prueba se ha omitido de forma explícita o por una condición.

Una prueba fallida no siempre significa que el código de producción esté mal: también puede haber un error en la propia prueba o en sus datos.

## Funcionalidades que conviene aprender después

No es necesario aprender todas las funciones de pytest desde el principio. Una progresión razonable es:

1. Funciones de prueba y `assert`.
2. Comprobación de excepciones con `pytest.raises`.
3. Parametrización con `@pytest.mark.parametrize`.
4. Fixtures con `@pytest.fixture`.
5. Fixtures compartidas mediante `conftest.py`.
6. Uso de mocks y sustitución de dependencias externas.
7. Cobertura con una herramienta complementaria como `coverage.py` o `pytest-cov`.

## pytest y TDD

pytest es una herramienta para ejecutar pruebas. TDD es una metodología de desarrollo.

Se pueden escribir pruebas con pytest después de implementar una funcionalidad, o utilizar pytest siguiendo el ciclo RED-GREEN-REFACTOR de TDD.

Consulta [TDD](tdd.md) para conocer la metodología.
