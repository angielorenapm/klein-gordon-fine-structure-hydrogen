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


## Ecuación de Klein–Gordon para el átomo de hidrógeno

Para un electrón ligado a un potencial Coulombiano,

$$
V(r) = -\frac{Ze^2}{r},
$$

la ecuación de Klein–Gordon puede escribirse como:

$$
\left[
\nabla^2
+
\frac{(E - V(r))^2 - m^2c^4}{\hbar^2c^2}
\right]\psi(\vec{r}) = 0.
$$

Debido a la simetría esférica del problema, la función de onda se separa como:

$$
\psi(\vec{r}) = R(r)Y_l^m(\theta,\phi),
$$

donde (R(r)) es la función radial y (Y_l^m(\theta,\phi)) son los armónicos esféricos.

La forma radial de la ecuación permite estudiar los niveles de energía del átomo de hidrógeno. Sin embargo, en la formulación estándar, los niveles dependen del número cuántico orbital (l), pero no del momento angular total (j). Esto evidencia la ausencia del espín electrónico en el modelo.

---

## Corrección escalar de Ducharme

El enfoque de Ducharme propone modificar la barrera centrífuga de la ecuación radial de Klein–Gordon para incorporar efectos asociados al espín. En lugar de depender únicamente del momento angular orbital, se introduce una dependencia efectiva con el momento angular total.

La ecuación radial corregida puede escribirse de forma general como:

$$
\frac{d^2R}{dr^2}
+
\frac{2}{r}\frac{dR}{dr}
+
\left[
\frac{\varepsilon^2 - 1}{\alpha^2}
+
\frac{2Z\varepsilon}{r}
+
\frac{\eta(1-\eta)}{r^2}
\right]R(r) = 0.
$$

Aquí:

$$
\varepsilon = \frac{E}{mc^2},
$$

$$
\eta = j+\frac{1}{2}
--------------------

\sqrt{
\left(j+\frac{1}{2}\right)^2
----------------------------

Z^2\alpha^2
}.
$$

En esta formulación, el término efectivo (\eta) permite introducir la dependencia con el número cuántico total (j), lo cual corrige una de las limitaciones centrales de la ecuación de Klein–Gordon estándar.

---

## Metodología computacional con PINNs

Las **Physics-Informed Neural Networks (PINNs)** permiten resolver ecuaciones diferenciales incorporando directamente las leyes físicas dentro de la función de pérdida.

En este proyecto, la red neuronal aproxima la función radial:

$$
R(r) \approx R_{\theta}(r),
$$

donde (\theta) representa los parámetros entrenables de la red neuronal.

La red se entrena minimizando una función de pérdida total compuesta por diferentes términos físicos:

$$
\mathcal{L}_{total}
===================

w_{DE}\mathcal{L}*{DE}
+
w*{BC}\mathcal{L}*{BC}
+
w*{norm}\mathcal{L}*{norm}
+
w_E\mathcal{L}*{E}.
$$

Cada término cumple una función específica:

### Residual de la ecuación diferencial

$$
\mathcal{L}_{DE}
================

\frac{1}{N_r}
\sum_{i=1}^{N_r}
\left|
\mathcal{R}(r_i)
\right|^2,
$$

donde el residual físico está dado por:

$$
\mathcal{R}(r)
==============

\frac{d^2R_{\theta}}{dr^2}
+
\frac{2}{r}\frac{dR_{\theta}}{dr}
+
\left[
\frac{\varepsilon^2 - 1}{\alpha^2}
+
\frac{2Z\varepsilon}{r}
+
\frac{\eta(1-\eta)}{r^2}
\right]R_{\theta}(r).
$$

### Condiciones de frontera

Se imponen condiciones físicas sobre la solución radial:

$$
R(0) = 0,
\qquad
R(r_{max}) = 0.
$$

El término de pérdida asociado es:

$$
\mathcal{L}_{BC}
================

|R_{\theta}(0)|^2
+
|R_{\theta}(r_{max})|^2.
$$

### Normalización

La función radial debe satisfacer la condición de normalización:

$$
\int_{0}^{r_{max}}
|R(r)|^2 r^2 dr = 1.
$$

Por tanto, el término de normalización se define como:

$$
\mathcal{L}_{norm}
==================

\left(
\int_{0}^{r_{max}}
|R_{\theta}(r)|^2 r^2 dr
------------------------

1
\right)^2.
$$

### Restricción energética

Para guiar el aprendizaje del autovalor de energía, se incluye un término de pérdida energética:

$$
\mathcal{L}_{E}
===============

\left(
E_{PINN}
--------

E_{ref}
\right)^2.
$$

---

## Estados estudiados

En la implementación computacional se analizaron cuatro estados hidrogenoides relevantes para comparar la estructura fina del átomo de hidrógeno dentro del enfoque corregido de Ducharme:

| Estado     | (n) | (l) |   (j) | (\kappa) | (E_{\mathrm{lig}}) (eV) |
| ---------- | --: | --: | ----: | -------: | ----------------------: |
| (2s_{1/2}) |   2 |   0 | (1/2) |     (-1) |           (-3.40147984) |
| (2p_{1/2}) |   2 |   1 | (1/2) |     (+1) |           (-3.40147984) |
| (2p_{3/2}) |   2 |   1 | (3/2) |     (-2) |           (-3.40143456) |
| (3p_{1/2}) |   3 |   1 | (1/2) |     (+1) |           (-1.51176379) |

Estos estados permiten observar la dependencia energética con el número cuántico total (j) y el parámetro relativista (\kappa). En particular, la comparación entre los estados (2p_{1/2}) y (2p_{3/2}) permite evidenciar el desdoblamiento asociado a la estructura fina, mientras que el estado (2s_{1/2}) comparte la misma energía de ligadura que (2p_{1/2}), mostrando la degeneración relativista esperada para esos niveles.

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

