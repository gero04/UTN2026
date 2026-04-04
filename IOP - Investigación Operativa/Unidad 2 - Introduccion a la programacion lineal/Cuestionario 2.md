## Problema 1.2 - Industrias Veidile

Una empresa desea planificar su producción para la próxima semana. Esta empresa produce un producto envasado en tres tamaños diferentes: de 120 gramos, de 200 gr. y de 360 gr. En la bodega dispone de 3 toneladas del producto a envasar. No puede producir más de él, debido a que requiere de un proceso de cocción lento. El otro insumo para el envasado son los envases vacíos de cada tipo. Hoy se tienen 3000 envases de 120 gr; 2000 de 200 gr. y 1500 de 360 gr. La única máquina que posee la empresa trabaja 20 horas al día de lunes a viernes; 12 horas los sábados y 8 horas los domingos. Para envasar los productos se requiere de 1 minuto para el envase de 120 gr; 2 minutos para el de 200 gr; y 4 minutos para el de 360 gr. Se tiene comprometida una venta de 300 unidades de envases de 200 gr a un conocido supermercado. Cada unidad del envase de 120 gr. genera un ingreso neto de $25; el de 200 gr. un ingreso neto de $50; el de 360 gr. un ingreso neto de $110.

## Formulacion Matematica

### Tabla de valores

| Recurso         | T1 | T2 | T3 | Disponibilidad |
|-----------------|-------|-------|-------|----------------|
|Producto (gramos)|120|200|360|3.000.000|
|Envases 120 g   |1|0|0|3.000|
|Envases 200 g   |0|1|0|2.000|
|Envases 360 g   |0|0|1|1.500|
|Tiempo de produccion|1|2|4|7.200|
|Ingreso neto|25|50|110|XXXXXX|


### Definicion de variables de decision

$T_1$: Unidades de producto en envase de 120 gramos a producir semanalmente
$T_2$: Unidades de producto en envase de 200 gramos a producir semanalmente
$T_3$: Unidades de producto en envase de 360 gramos a producir semanalmente

### Funcion Objetivo

MAX Z = 25 $T_1$ + 50 $T_2$ +110 $T_3$

### Cuerpo de restricciones sin variables de holgura

* Restriccion de cantidad de producto:

$$120\ \frac{[Gramos]}{[Unidad]}\ T_1\ [Unidad]\ +\ 200\ \frac{[Gramos]}{[Unidad]}\ T_2\ [Unidad]\ +\ 360\ \frac{[Gramos]}{[Unidad]}\ T_3\ [Unidad]\ \leq\ 3.000.000\ [Gramos]$$

* Restriccion de envases de 120 gr.:

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ \leq\ 3000\ [Envase]$$

* Restriccion de envases de 200 gr.:

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ \leq\ 2000\ [Envase]$$

* Restriccion de envases de 360 gr.:

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ \leq\ 1500\ [Envase]$$

* Restriccion de tiempo de envasado:

$$1\ \frac{[Minutos]}{[Unidad]}\ T_1\ [Unidad]\ +\ 2\ \frac{[Minutos]}{[Unidad]}\ T_2\ [Unidad]\ +\ 4\ \frac{[Minutos]}{[Unidad]}\ T_3\ [Unidad]\ \leq\ 7200\ [Minutos]$$

* Restriccion de venta a supermercado:

$$T_1\ [Unidad]\ =\ 300\ [Unidad]$$

### Cuerpo de restricciones con variables de holgura

* Restriccion de cantidad de producto: $S_1$ representa la cantidad de producto en gramos que no se utiliza

$$120\ \frac{[Gramos]}{[Unidad]}\ T_1\ [Unidad]\ +\ 200\ \frac{[Gramos]}{[Unidad]}\ T_2\ [Unidad]\ +\ 360\ \frac{[Gramos]}{[Unidad]}\ T_3\ [Unidad]\ +\ S_1\ =\ 3.000.000\ [Gramos]$$

* Restriccion de envases de 120 gr.: $S_2$ representa la cantidad de envases de 120 gramos que no se utilizan

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ +\ S_2\ =\ 3000\ [Envase]$$

* Restriccion de envases de 200 gr.: $S_3$ representa la cantidad de envases de 200 gramos que no se utilizan

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ +\ S_3\ =\ 2000\ [Envase]$$

* Restriccion de envases de 360 gr.: $S_4$ representa la cantidad de envases de 360 gramos que no se utilizan

$$1\ \frac{[Envase]}{[Unidad]}\ T_1\ [Unidad]\ +\ S_4\ =\ 1500\ [Envase]$$

* Restriccion de tiempo de envasado: $S_5$ representa los minutos de envasado que no se utilizan

$$1\ \frac{[Minutos]}{[Unidad]}\ T_1\ [Unidad]\ +\ 2\ \frac{[Minutos]}{[Unidad]}\ T_2\ [Unidad]\ +\ 4\ \frac{[Minutos]}{[Unidad]}\ T_3\ [Unidad]\ +\ S_5\ =\ 7200\ [Minutos]$$

* Restriccion de venta a supermercado: No requiere de uso de variables de holgura

$$T_1\ [Unidad]\ =\ 300\ [Unidad]$$

### Restriccion de no nulidad

$\forall T_j \geq 0 $ tal que j = (1, 2, ..., n)

## Pregunta 1

¿Cuál de las siguientes afirmaciones representa al objetivo del problema?

* Maximizar la producción en envases de 120g, 200g y 360g para la próxima semana.
* Minimizar el uso de los recursos.
* Maximizar el Beneficio Total por la elaboración y venta del producto en envases de 120g, 200g y 360g para la próxima semana.
* Maximizar el Ingreso Total por la elaboración del producto para la próxima semana.
* Maximizar el Ingreso Total por la elaboración y venta del producto en envases de 120g, 200g y 360g para la próxima semana.

Respuesta

* Maximizar el Ingreso Total por la elaboración y venta del producto en envases de 120g, 200g y 360g para la próxima semana.

## Pregunta 2

¿Cuál/cuáles de las siguientes afirmaciones corresponden a restricciones del problema?

* Minutos que se requieren para envasar el producto en cada uno de los envases.
* Se pueden utilizar al menos 120 hs de máquina envasadora.
* Se dispone de 3 toneladas de producto a envasar.
* Disponibilidad de envases vacíos de cada tipo.
* Cantidad de horas que trabaja la máquina envasadora.
* Cantidad mínima de unidades de 200g a envasar.
* Demanda máxima de envases de 200g comprometida a un supermercado.

Respuesta

* Se dispone de 3 toneladas de producto a envasar.
* Disponibilidad de envases vacíos de cada tipo.
* Cantidad de horas que trabaja la máquina envasadora.
* Cantidad mínima de unidades de 200g a envasar.

## Pregunta 3

Las variables pueden definirse como:

* X1 = gramos de producto a envasar en tamaño de 120g para la próxima semana <br>
X2 = gramos de producto a envasar en tamaño de 200g para la próxima semana <br>
X3 = gramos de producto a envasar en tamaño de 360g para la próxima semana
* X1 = unidades del producto a producir en envases de 120g para la próxima semana <br>
X2 = unidades del producto a producir en envases de 200g para la próxima semana <br>
X3 = unidades del producto a producir en envases de 360g para la próxima semana
* X1 = producto de 120g a fabricar semanalmente <br>
X2 = producto de 200g a fabricar semanalmente <br>
X3 = producto de 360g a fabricar semanalmente 
* X1 = unidades de envases de 120g a producir para la próxima semana <br>
X2 = unidades de envases de 200g a producir para la próxima semana <br>
X3 = unidades de envases de 360g a producir para la próxima semana
* Xi = unidades del producto i a producir para la próxima semana.

Respuesta

* X1 = unidades del producto a producir en envases de 120g para la próxima semana <br>
X2 = unidades del producto a producir en envases de 200g para la próxima semana <br>
X3 = unidades del producto a producir en envases de 360g para la próxima semana

## Pregunta 4

Matemáticamente el objetivo se escribe como: [MAX, MIN] Z [<=, =, >=] [...] x1 + [...] x2 + [...] x3 

Respuesta

Matemáticamente el objetivo se escribe como: MAX Z = 25 x1 + 50 x2 + 110 x3 

## Pregunta 5

¿Cuál/Cuáles de las siguientes funciones representan restricciones del problema?

* 1 X1 + 2 X2 + 4 X3 ≤ 7.200
* X1 ≥ 3.000
* X2 ≥ 300
* 1 X1  + 2 X2 + 4 X3 ≤ 2.400
* 0,120X1 + 0,200X2 + 0,360X3  ≤ 3.000
* 120X1 + 200X2 + 360X3 ≤ 3
* X2 = 300

Respuesta

* 1 X1 + 2 X2 + 4 X3 ≤ 7.200
* X2 ≥ 300
* 0,120X1 + 0,200X2 + 0,360X3  ≤ 3.000

## Pregunta 6

Si un proveedor le ofrece envases de 120 gr. vacíos a un precio de $1 cada uno, describa lo que haría para determinar si le conviene comprarlos o no.

Respuesta (Segun DeepSeek)

Para determinar si conviene comprar envases de 120 g vacíos a $1 cada uno, se debe calcular el **precio sombra** (o valor dual) de la restricción correspondiente a la disponibilidad de envases de 120 g en el modelo de programación lineal. Ese valor indica cuánto aumentaría la utilidad óptima si se dispusiera de un envase adicional de ese tipo.

- Si el precio sombra es **mayor** que $1, entonces comprar envases a ese costo incrementa la utilidad neta.
- Si es **menor** que $1, no conviene, porque el costo supera el beneficio marginal.
- Si es **igual** a $1, es indiferente.

Para obtener el precio sombra se debe resolver el modelo lineal (con la restricción de no negatividad y la demanda mínima de envases de 200 g) y consultar el informe de sensibilidad correspondiente a la restricción de envases de 120 g.

## Pregunta 7

El modelo de programación lineal del problema analizado queda formulado en forma: [explicita, matricial, vectorial] y [canonica, estandar, mixta].

Respuesta

El modelo de programación lineal del problema analizado queda formulado en forma: explicita y mixta.