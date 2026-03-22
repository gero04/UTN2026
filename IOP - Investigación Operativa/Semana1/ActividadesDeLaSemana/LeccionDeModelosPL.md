# Investigacion Operativa
## 1. Modelo Matematico
* Consigna

Escribe un Modelo matemático general de la Programación Lineal en forma explícita canónica que tenga n variables y m restricciones e identifica cada una de sus partes: función objetivo, restricciones y restricción de no negatividad.

* Respuesta

Funcion objetivo

Max (Min) Z = c_1 x_1 + c_2 x_2 + ... + c_n x_n

Restricciones

$$a_{11} x_1 + a_{12} x_2 + ... + a_{1n} x_n = b_1$$
$$a_{21} x_1 + a_{22} x_2 + ... + a_{2n} x_n = b_2$$
$$ ... $$
$$a_{m1} x_1 + a_{m2} x_2 + ... + a_{mn} x_n = b_m$$

Restriccion de no negatividad

$\forall x_j \geq 0 $ tal que j = (1, 2, ..., n)

## 2. Primer paso en la formulación de modelos

* Consigna

Lee el Problema N° 3 de la Guía de Problemas para Clases Prácticas, analizando a qué se dedica la empresa, el proceso productivo que se quiere optimizar, las limitaciones o restricciones que posee y los datos que se proporcionan. Reescribe con tus palabras esta información.

* Respuesta

La empresa se dedica a la produccion de insumos y piezas industriales de precision, fundamentalmente latexy derivados. Quieren optimizar el proceso de produccion de sus principales productos de exportacion (AC1, AC2 y AC3). Las restricciones que se poseen son 3200 unidades de materia prima por semana, siendo que el producto AC1 requiere 40, el producto AC2 80 y el AC3 30 unidades de materia prima por pieza a producir. Cada pieza consume 100, 50 y 75 horas de mano de obra y dan, de utilidad, $110, $40 y $7 respectivamente. Por ultimo se requiere fabricar al menos 10 unidades entre los 3 productos

## 3. Segundo paso en la formulacion de modelos

* Consigna

Extrae los datos que se proporcionan, organizándolos en una tabla

* Respuesta

| Producto       | AC1 | AC2 | AC3 | Disponibilidad   |
|----------------|-----|-----|-----|------------------|
| Materia prima  | 40  | 80  | 30  | 3200             |
| Hs Mano Obra   | 100 | 50  | 75  | No especifica    |
| Utilidad       | 110 | 40  | 7   | No especifica    |

## 4. Objetivo

* Consigna

El objetivo de las Industrias Vandelay es:

* Respuesta 

Maximizar las utilidades por la producción y venta de sus productos de exportación

## 5. Definicion de variables

* Consigna

Las variables pueden ser definidas de la siguiente forma:
$X_1$: Unidades a producir del producto AC1 en la semana
$X_2$: Unidades a producir del producto AC2 en la semana
$X_3$: Unidades a producir del producto AC3 en la semana

* Respuesta

Verdadero

## 6. Forma Matematica

* Consigna

El objetivo del problema en forma matemática es:

* Respuesta

$Max\ 110\ X_1\ +\ 40\ X_2\ +\ 7\ X_3$

## 7. Restricciones o limitaciones

* Consigna

Identifique las restricciones o limitaciones que encuentran las Industrias Vandelay para lograr su objetivo.

* Respuesta

Las restricciones que se poseen son 3200 unidades de materia prima por semana, siendo que el producto AC1 requiere 40, el producto AC2 80 y el AC3 30 unidades de materia prima por pieza a producir, y se tienen que fabricar al menos 10 unidades en total entre todas las piezas. Cada pieza consume 100, 50 y 75 horas de mano de obra, con un maximo de 5000 horas por semana.

## 8. Restricciones o limitaciones parte 2

* Consigna

¿Cuál de las siguientes opciones indica todas las restricciones o limitaciones que encuentran las Industrias Vandelay para lograr su objetivo?

* Respuesta

Disponibilidad semanal de materia prima y mano de obra a utilizar y cantidad mínima de productos a fabricar.

## 9. Forma matematica de las restricciones

* Consigna

Exprese en forma matemática cada una de las restricciones del problema, en forma de ecuaciones o inecuaciones lineales

* Respuesta

Restricciones de materia prima
$$
40\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC1\ [Unidad\ producida]\ +\ 80\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC2\ [Unidad\ producida]\ +\ 30\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC3\ [Unidad\ producida]\ \leq \ 3200\ [Unidad\ de\ materia\ prima]
$$

Restricciones de mano de obra
$$
100\ \frac{[Horas]}{[Unidad]}\ AC1\ [Unidad]\ +\ 50\ \frac{[Horas]}{[Unidad]}\ AC2\ [Unidad]\ +\ 75\ \frac{[Horas]}{[Unidad]}\ AC3\ [Unidad]\ \leq\ 5000\ [Horas]
$$

Restricciones de produccion minima
$$
AC1\ [Unidad]\ +\ AC2\ [Unidad]\ +\ AC3\ [Unidad]\ \geq\ 10\ [Unidad]
$$

Restriccion de no negatividad
$$
AC1,\ AC2,\ AC3\ \geq 0
$$

## 10. Forma matematica de las restricciones parte 2

* Consigna

El modelo lineal completo es:

Max 110X1 + 40X2 + 7X3                            (Maximizar las utilidades)

s.a.

40X1 + 80X2 + 30X3 ≤ 3200     (disponibilidad de materia prima)

100X1 + 50X2 + 75X3 ≤ 5000     (disponibilidad de horas de mano de obra)

X1 +    X2 +     X3 ≥ 10         (cantidad mínima a fabricar)

X1, X2, X3 ≥ 0            (restricción de no negatividad)

* Respuesta

Verdadero

## 11. Variables de holgura

* Consigna

Agregue las variables de holgura indicando su significado en forma completa.

* Respuesta

Restricciones de materia prima: $S_1$ representa las unidades de materia prima no utilizadas
$$
40\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC1\ [Unidad\ producida]\ +\ 80\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC2\ [Unidad\ producida]\ +\ 30\ \frac{[Unidad\ de\ materia\ prima]}{[Unidad\ producida]}\ AC3\ [Unidad\ producida]\ +\ S_1\ =\ 3200\ [Unidad\ de\ materia\ prima]
$$

Restricciones de mano de obra: $S_2$ representa las horas de mano de obra no utilizadas
$$
100\ \frac{[Horas]}{[Unidad]}\ AC1\ [Unidad]\ +\ 50\ \frac{[Horas]}{[Unidad]}\ AC2\ [Unidad]\ +\ 75\ \frac{[Horas]}{[Unidad]}\ AC3\ [Unidad]\ +\ S_2\ =\ 5000\ [Horas]
$$

Restricciones de produccion minima: $S_4$ representa la cantidad de unidades producidas por encima de la cantidad minima necesaria
$$
AC1\ [Unidad]\ +\ AC2\ [Unidad]\ +\ AC3\ [Unidad]\ +\ S_4\ =\ 10\ [Unidad]
$$

Restriccion de no negatividad
$$
AC1,\ AC2,\ AC3\ \geq 0
$$

## 12. Variables de holgura parte 2

* Consigna

La variable de holgura correspondiente a la restricción de horas de MO, se puede definir como:

S2: horas de mano de obra disponibles para la producción de los productos

* Respuesta

Falso