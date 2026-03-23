# Cuestionario 1
## Problema 1.2 - Industrias Veidile

Industrias Veidile provee de máquinas y motores de alto rendimiento a diferentes fábricas automotrices de la región centro de nuestro país. Actualmente, fabrica dos tipos de motores: M1 y M2. Un estudio detallado de costos y precios ha permitido calcular que se obtiene una utilidad de $ 100 por cada unidad del primero y $ 120 por cada una del segundo. Además, debe considerarse que, durante la fabricación de estos motores, los recursos principales son las horas de proceso de maquinado, armado y montaje requeridas por cada unidad. Dispone semanalmente de 480, 600 y 540 hs de cada proceso respectivamente. Para fabricar un motor M1 se necesitan 4 hs de maquinado, 5 de armado y 12 de montaje. Por otro lado, un motor M2 requerirá 8 hs de maquinado, 6 de armado y 8 de montaje. Considerando una demanda creciente e insatisfecha de sus productos, puede asumir que todo lo que produzca será vendido. Por ello, hasta tener la posibilidad de ampliar la planta, un plan de producción ineficiente significaría un costo de oportunidad importante.

## Formulacion Matematica

### Tabla de valores

|Producto|Motor M1|Motor M2|Disponibilidad|
|--------|--------|--------|--------------|
|Maquinado|4|8|480|
|Armado|5|6|600|
|Montaje|12|8|540|
|Utilidad|$100|$120|XXXXXXXXX|

### Definicion de variables de decision

* $M_1$ = Unidades de Motores tipo 1 a fabricar semanalmente
* $M_2$ = Unidades de Motores tipo 2 a fabricar semanalmente

### Funcion Objetivo

$$ Max Z = 100 M_1 + 120 M_2$$

### Cuerpo de restricciones sin variables de holgura

$$4\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 480\ [Horas]$$
$$5\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 6\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 600\ [Horas]$$
$$12\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 540\ [Horas]$$

### Cuerpo de restricciones con variables de holgura

* Restriccion de horas de maquinado: $S_1$ representa las horas de maquinado que no se utilizan

$$4\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ +\ S_1\ =\ 480\ [Horas]$$

* Restriccion de horas de armado: $S_2$ representa las horas de armado que no se utilizan

$$5\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 6\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ +\ S_2\ =\ 600\ [Horas]$$

* Restriccion de horas de montaje: $S_3$ representa las horas de montaje que no se utilizan

$$12\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ +\ S_3\ =\ 540\ [Horas]$$

### Restriccion de no nulidad

$\forall x_j \geq 0 $ tal que j = (1, 2, ..., n)

## Pregunta 1

¿Cuál de las siguientes afirmaciones representa al objetivo del problema?
* Maximizar el Ingreso Total por la producción y venta semanal de motores M1 y M2 
* Minimizar el uso de los recursos
* Maximizar el Ingreso Total anual por la elaboración de los productos
* Maximizar la Utilidad Total semanal por la producción y venta de motores M1 y M2 
* Maximizar la producción semanal de motores M1 y M2

La afirmacion que representa al objetivo del problema es

* Maximizar la Utilidad Total semanal por la producción y venta de motores M1 y M2

## Pregunta 2

Las variables pueden definirse como:

* xi = Motores tipo  i a fabricar semanalmente
* x1 = cantidad de Motores tipo 1 a fabricar semanalmente y x2 = cantidad de Motores tipo 2 a fabricar semanalmente
* x1 = Motores tipo 1 a fabricar semanalmente y x2 = Motores tipo 2 a fabricar semanalmente
* xi = Motor tipo Mi
* x1 = Motores  M1 y x2 = Motores M2
* x1 = unidades de Motores tipo 1 a fabricar semanalmente y x2 = unidades de Motores tipo 2 a fabricar semanalmente
* xj = unidades de Motores tipo j a fabricar semanalmente para j =1, 2

Las respuestas correctas son

* x1 = unidades de Motores tipo 1 a fabricar semanalmente y x2 = unidades de Motores tipo 2 a fabricar semanalmente
* xj = unidades de Motores tipo j a fabricar semanalmente para j =1, 2

## Pregunta 3

¿Cuál/cuáles de las siguientes afirmaciones corresponden a restricciones del problema?
* Se deben utilizar 480 hs de maquinado
* Se pueden utilizar hasta de 600 hs de armado
* Se pueden utilizar como mínimo 600 hs de armado
* Se deben utilizar al menos 540 hs de montaje
* Se pueden utilizar no más de 480 hs de maquinado
* Como máximo se pueden utilizar 540 hs de montaje

Las respuestas correctas son

* Se pueden utilizar hasta de 600 hs de armado
* Se pueden utilizar no más de 480 hs de maquinado
* Como máximo se pueden utilizar 540 hs de montaje

## Pregunta 4

Si x1 y x2 representan a las variables del problema entonces, matemáticamente el objetivo del problema se escribe como:

* max 100 M1 + 120 M2
* max 100 (7) M1 + 120 (7) M2
* min 480 (x1 + x2) + 540 (x1 + x2) + 600 (x1 + x2)
* max 100 x1 + 120 x2
* min 100 x1 + 120 x2
* max 100 (7) x1 + 120 (7) x2

La respuesta correcta es

* max 100 x1 + 120 x2

## Pregunta 5

¿Cuál/Cuáles de las siguientes funciones representan restricciones del problema?

* 6 M1 + 5 M2≤ 600
* 4 x1 + 8 x2 = 480
* 4 x1 + 8 x2 ≤ 480
* 5 x1 + 6 x2 = 600
* 4 x1 + 8 x2  ≥ 480
* 12 x1 + 8 x2 ≤ 540
* 12 x1 + 8 x2≥540

Las respuestas correctas son

* 4 x1 + 8 x2 ≤ 480
* 12 x1 + 8 x2 ≤ 540

## Pregunta 6

De acuerdo con la restricción de No Negatividad, los valores de las variables de todo programa lineal deben ser positivas.

* Verdadero
* Falso 

La respuesta correcta es

* Falso

## Pregunta 7

El modelo de programación lineal del problema analizado queda formulado en forma: [explicita, vectorial, matricial] y [canonica, mixta, estandar].

La respuesta correcta es

El modelo de programación lineal del problema analizado queda formulado en forma: explicita y canonica.