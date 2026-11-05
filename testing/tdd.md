# Test-Driven Development (TDD)

## ¿Qué es TDD?

TDD (*Test-Driven Development*, desarrollo guiado por pruebas) es una metodología de desarrollo en la que se escriben pruebas antes de implementar la funcionalidad correspondiente.

Las pruebas describen el comportamiento esperado y sirven como guía para construir el programa de forma incremental.

TDD no significa simplemente escribir pruebas al terminar el código. El orden de trabajo es una parte esencial de la metodología.

## El ciclo RED-GREEN-REFACTOR

TDD se organiza en ciclos pequeños de tres pasos:

### 1. RED: escribir una prueba que falle

Se define un comportamiento esperado y se escribe una prueba que lo compruebe.

La prueba debe fallar inicialmente porque la funcionalidad todavía no existe o no está implementada correctamente.

El fallo inicial confirma que la prueba está ejecutándose y que detectaría la ausencia del comportamiento.

### 2. GREEN: implementar lo mínimo necesario

Se escribe el código de producción más sencillo que permita superar la prueba.

El objetivo no es anticipar todas las necesidades futuras ni construir una solución compleja, sino satisfacer el comportamiento que acaba de especificarse.

Después se ejecutan las pruebas para comprobar que pasan.

### 3. REFACTOR: mejorar el diseño

Con las pruebas pasando, se mejora el código sin cambiar su comportamiento observable.

Por ejemplo:

- Eliminar duplicaciones.
- Mejorar nombres de variables y funciones.
- Simplificar condiciones.
- Separar responsabilidades.
- Mejorar la estructura.

Después del refactor se vuelven a ejecutar las pruebas. Si alguna falla, el cambio ha alterado un comportamiento comprobado o ha introducido un defecto.

El ciclo comienza de nuevo con el siguiente comportamiento.

## Ejemplo conceptual

Imagina que se necesita una función `add(a, b)` que sume dos números.

1. **RED:** escribir una prueba que espere que `add(2, 3)` devuelva `5`. La prueba falla porque la función aún no existe.
2. **GREEN:** implementar `add()` con la operación necesaria para que la prueba pase.
3. **REFACTOR:** revisar si la implementación necesita mejoras. Si no las necesita, no hay que modificarla por obligación.
4. Repetir el ciclo para otro comportamiento, por ejemplo, sumar números negativos.

Es importante escribir primero la prueba y no implementar toda la función antes de comprobarla.

## Buenas prácticas

- Trabajar en incrementos pequeños.
- Escribir una prueba que describa un comportamiento concreto.
- Comprobar que la prueba falla por el motivo esperado.
- Implementar únicamente lo necesario para hacerla pasar.
- Ejecutar todas las pruebas relevantes después de cada cambio.
- Refactorizar con las pruebas pasando.
- Utilizar nombres de pruebas que expliquen qué comportamiento se comprueba.
- Evitar que las pruebas dependan innecesariamente unas de otras.

## Ventajas

- Obliga a concretar el comportamiento esperado antes de implementarlo.
- Proporciona comprobaciones frecuentes durante el desarrollo.
- Puede facilitar cambios y refactorizaciones con menor riesgo.
- Ayuda a detectar defectos pronto.
- Las pruebas pueden servir como documentación ejecutable del comportamiento.

## Limitaciones y precauciones

TDD no garantiza por sí solo que el diseño sea bueno ni que el programa esté libre de errores.

También requiere práctica: formular buenas pruebas y elegir incrementos pequeños puede resultar difícil al principio.

No todos los aspectos son igual de sencillos de probar. Interfaces visuales, integraciones externas o requisitos ambiguos pueden requerir técnicas complementarias.

Tampoco conviene escribir pruebas únicamente para alcanzar un porcentaje de cobertura. Lo importante es comprobar comportamientos relevantes.

## TDD y testing

TDD utiliza pruebas automatizadas como parte del proceso de desarrollo, pero testing y TDD no son sinónimos.

- **Testing:** conjunto de prácticas para comprobar el software.
- **TDD:** metodología que utiliza pruebas escritas previamente para guiar la implementación.

Consulta [Software Testing](software-testing.md) para los niveles y conceptos generales de testing.

## Herramientas

TDD es independiente del lenguaje y del framework utilizado.

Algunas herramientas habituales son:

- Python: [pytest](pytest.md).
- Java: JUnit 5 (JUnit Jupiter).

Las herramientas ejecutan las pruebas; el ciclo RED-GREEN-REFACTOR es la metodología de trabajo.
