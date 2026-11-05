# Software Testing

## ¿Qué es el testing?

El *software testing* (pruebas de software) es el proceso de comprobar que un programa se comporta como se espera y de detectar defectos antes de que provoquen problemas.

Una prueba define unas condiciones, ejecuta una parte del sistema y compara el resultado obtenido con el resultado esperado.

El testing ayuda a:

- Detectar errores durante el desarrollo.
- Comprobar que los requisitos se cumplen.
- Evitar que cambios posteriores rompan funcionalidades existentes.
- Documentar el comportamiento esperado del programa.
- Aumentar la confianza al modificar o ampliar el código.

Las pruebas no demuestran que un programa esté libre de errores: comprueban determinados comportamientos bajo unas condiciones concretas.

## Testing manual y automatizado

### Testing manual

Una persona ejecuta el programa e interactúa con él para comprobar su comportamiento.

Por ejemplo, introducir datos en un formulario y comprobar visualmente el resultado.

### Testing automatizado

Se escriben instrucciones que ejecutan comprobaciones automáticamente. Un framework de testing puede ejecutar muchas pruebas y comunicar cuáles han pasado o fallado.

La automatización resulta especialmente útil cuando hay que repetir las mismas comprobaciones después de cada cambio.

## Niveles de prueba

Los niveles describen el alcance de lo que se comprueba. No son metodologías de desarrollo ni herramientas concretas.

### Pruebas unitarias (*unit tests*)

Comprueban una unidad pequeña del programa de forma aislada, normalmente una función, método o componente.

Ejemplo: comprobar que una función que suma dos números devuelve el resultado esperado.

### Pruebas de integración (*integration tests*)

Comprueban que varios componentes funcionan correctamente al interactuar entre sí.

Ejemplo: comprobar que una función lee un archivo, procesa su contenido y devuelve los elementos esperados.

### Pruebas end-to-end (E2E)

Comprueban un flujo completo desde el punto de vista de quien utiliza el sistema.

Ejemplo: introducir información en una aplicación, iniciar el proceso de clasificación y comprobar que se muestra el resultado.

## Qué debería comprobar una prueba

Una buena prueba suele centrarse en un comportamiento concreto y verificable.

Conviene considerar:

- **Caso habitual:** el programa recibe datos válidos y debe producir el resultado esperado.
- **Casos límite:** valores vacíos, mínimos, máximos o situaciones poco habituales.
- **Entradas inválidas:** datos que no cumplen las condiciones esperadas.
- **Errores y excepciones:** cómo debe reaccionar el programa ante fallos previsibles.
- **Regresiones:** comprobar que una funcionalidad que ya funcionaba sigue haciéndolo después de modificar el código.

## Pruebas y regresiones

Una regresión ocurre cuando un cambio introduce un error en una funcionalidad que anteriormente funcionaba.

Una suite de pruebas automatizadas permite volver a ejecutar comprobaciones anteriores después de modificar el programa. Así se detectan regresiones con mayor facilidad.

## Cobertura de código

La cobertura (*code coverage*) mide qué parte del código se ejecuta al ejecutar las pruebas. Puede medirse, por ejemplo, por líneas o ramas ejecutadas.

Una cobertura elevada no garantiza que las pruebas sean buenas: una línea puede ejecutarse sin que se compruebe correctamente su resultado.

La cobertura es una métrica orientativa, no un objetivo que deba perseguirse a cualquier precio.

## Testing y TDD

El testing es la práctica general de comprobar el comportamiento del software.

TDD (*Test-Driven Development*) es una metodología de desarrollo en la que las pruebas guían la implementación: primero se escribe una prueba que falla, después se implementa lo mínimo para hacerla pasar y finalmente se mejora el código.

Consulta [TDD](tdd.md) para conocer el ciclo RED-GREEN-REFACTOR y [pytest](pytest.md) para su aplicación en Python.

## Ideas clave

- Las pruebas comprueban comportamientos concretos; no demuestran la ausencia absoluta de errores.
- Las pruebas unitarias, de integración y E2E se diferencian por su alcance.
- Las pruebas automatizadas permiten repetir comprobaciones de forma consistente.
- Las pruebas de regresión ayudan a detectar errores introducidos por cambios.
- La cobertura indica qué código se ejecuta, no necesariamente la calidad de las comprobaciones.
