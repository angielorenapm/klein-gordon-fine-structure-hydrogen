# Revisitando la Ecuación de Klein–Gordon mediante PINNs

Este repositorio contiene el desarrollo teórico, histórico y computacional del proyecto **“Revisitando la Ecuación de Klein–Gordon en átomos hidrogenoides: correcciones de espín de Ducharme, densidad de probabilidad y redes neuronales informadas por la física (PINNs)”**.

El trabajo estudia la ecuación de Klein–Gordon como uno de los primeros intentos de formular una teoría cuántica relativista. A partir de su desarrollo histórico y matemático, se analizan sus principales limitaciones al describir el átomo de hidrógeno, especialmente su incapacidad para reproducir correctamente la estructura fina debido a que no incorpora explícitamente el espín del electrón.

Además, se explora la formulación propuesta por **Robert Ducharme**, en la cual se introduce una corrección escalar asociada al espín dentro de una ecuación tipo Klein–Gordon. Finalmente, se implementa una metodología computacional basada en **Physics-Informed Neural Networks (PINNs)** para aproximar soluciones radiales y niveles de energía del problema.

---

## Objetivo del proyecto

Analizar las limitaciones de la ecuación de Klein–Gordon aplicada al átomo de hidrógeno y estudiar una alternativa corregida mediante el enfoque de Ducharme, usando redes neuronales informadas por la física para resolver el problema radial relativista.

---

## Contenido del repositorio

El repositorio incluye los siguientes archivos principales:

| Archivo                                         | Descripción                                                                           |
| ----------------------------------------------- | ------------------------------------------------------------------------------------- |
| `KG_EQUATION_Final.pdf`                         | Artículo final del proyecto, con el desarrollo histórico, matemático y computacional. |
| `Diapositivas.pdf`                              | Presentación usada para explicar el proyecto.                                         |
| `KG_PINNS.ipynb`                                | Notebook principal con la implementación de las PINNs.                                |
| `KG_densidadprobabilidad (1).ipynb`             | Notebook relacionado con el análisis de la densidad de probabilidad de Klein–Gordon.  |
| `Poster -Articulo_revision_QM (1).pdf`          | Póster inicial del trabajo de revisión.                                               |
| `Kragh1984 - Equation with the many fathers...` | Referencia histórica base sobre el origen de la ecuación de Klein–Gordon.             |
| `kg_thomas.html`                                | Material complementario relacionado con la corrección de Thomas.                      |
| `README.md`                                     | Descripción general del repositorio.                                                  |

---

## Contexto físico

La ecuación de Klein–Gordon surge al cuantizar la relación relativista energía–momento:

[
E^2 = p^2c^2 + m^2c^4
]

Aunque esta ecuación fue un avance importante en la construcción de una mecánica cuántica relativista, presenta dificultades cuando se aplica a partículas fermiónicas como el electrón. Entre sus principales limitaciones se encuentran:

* No incorpora explícitamente el espín del electrón.
* No reproduce correctamente la estructura fina del átomo de hidrógeno.
* Presenta una densidad de probabilidad que no siempre es definida positiva.
* No describe de forma completa partículas con espín semi-entero.

Estas dificultades motivaron el desarrollo posterior de la ecuación de Dirac. Sin embargo, el enfoque de Ducharme permite reconsiderar la ecuación de Klein–Gordon desde una formulación escalar corregida, incorporando efectos asociados al espín sin usar directamente matrices de Dirac.

---

## Metodología

La metodología del proyecto combina tres partes principales:

### 1. Revisión histórica y conceptual

Se estudia el origen de la ecuación de Klein–Gordon y las contribuciones de autores como Schrödinger, Klein, Gordon, Fock, Pauli y Dirac. También se analiza por qué esta ecuación fue desplazada por la ecuación de Dirac en la descripción relativista del electrón.

### 2. Desarrollo matemático

Se revisa la ecuación de Klein–Gordon para el átomo de hidrógeno, su acoplamiento al potencial de Coulomb y sus limitaciones en la predicción de la estructura fina. Posteriormente, se introduce la corrección de Ducharme, donde el término centrífugo radial se modifica para incluir efectos asociados al momento angular total.

### 3. Implementación computacional con PINNs

Se implementa una red neuronal informada por la física para resolver la ecuación diferencial radial. La red aproxima simultáneamente la solución radial y los niveles de energía, incorporando en la función de pérdida:

* Residual de la ecuación diferencial.
* Condiciones de frontera.
* Normalización de la función radial.
* Restricción energética respecto al valor teórico de referencia.

---

## Physics-Informed Neural Networks

Las **PINNs** permiten resolver ecuaciones diferenciales incorporando directamente las leyes físicas dentro de la función de pérdida. En este proyecto, la red neuronal no solo ajusta datos, sino que también minimiza el error asociado a la ecuación radial corregida.

De esta forma, el modelo aprende soluciones físicamente consistentes para estados cuánticos del átomo de hidrógeno, comparando la energía aprendida con los valores esperados del modelo relativista.

---

## Estados estudiados

En la implementación computacional se analizan estados hidrogenoides relevantes para estudiar la estructura fina, tales como:

* (2p_{1/2})
* (3p_{3/2})

Estos estados permiten observar cómo la corrección asociada al espín modifica la estructura energética y cómo la red neuronal aproxima las soluciones radiales correspondientes.

---

## Video explicativo

El proyecto cuenta con un video explicativo en YouTube, donde se presenta el objetivo general del trabajo, el fundamento físico y la metodología computacional usada.

[Ver video en YouTube](https://youtu.be/bgc6GzGN9K0)

---

## Autoras

**Angie Lorena Pineda**
**Ángela Sofía Malagón**

Universidad Distrital Francisco José de Caldas
Facultad de Ciencias Matemáticas y Naturales
Bogotá, Colombia

---

## Referencias principales

1. H. Kragh, *Equation with the many fathers. The Klein–Gordon equation in 1926*, American Journal of Physics, 52, 1024–1033, 1984.

2. J. P. Paz, *Apuntes de clases de Física Cuántica: Estructura fina*, Universidad de Buenos Aires, 2020.

3. R. Ducharme, *Exact Solution of the Klein-Gordon Equation for the Hydrogen Atom Including Electron Spin*.

---

## Palabras clave

`Klein-Gordon`
`Hydrogen atom`
`Fine structure`
`Ducharme correction`
`Physics-Informed Neural Networks`
`PINNs`
`Quantum mechanics`
`Relativistic quantum mechanics`

