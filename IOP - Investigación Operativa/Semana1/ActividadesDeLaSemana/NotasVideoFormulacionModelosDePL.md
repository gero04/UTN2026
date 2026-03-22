# Introducción a la Programación Lineal: Planteo y Formulación de Modelos
*Materia:* IOP (Investigación Operativa)
*Resumen en una oración:* La clase aborda el proceso de traducir problemas reales a un lenguaje matemático formal mediante el uso de variables de decisión, funciones objetivo, restricciones y variables de holgura.

---

## Conceptos clave

* **Formulación de un modelo de Programación Lineal**: Es el acto de traducir a la forma matemática general un problema de la realidad. Consiste en identificar los elementos del problema (datos, parámetros y variables) y expresarlos mediante símbolos matemáticos.
* **Variables de Decisión ($X_j$)**: Son las incógnitas que se desean determinar al resolver el problema. Representan las cantidades o decisiones sobre las cuales se tiene control. Deben definirse con precisión, incluyendo unidad de medida y unidad de tiempo.
* **Función Objetivo**: Es la expresión matemática que se busca optimizar (maximizar o minimizar). Representa la meta del problema, como puede ser el beneficio total o el costo de producción. Por ejemplo: 

$$
Max (Min) Z = c_1 x_1 +c_2 x_2 + c_3 x_3 + ... + c_n x_n
$$

* **Cuerpo de Restricciones**: Conjunto de limitaciones o requerimientos (expresados como inecuaciones de $\le$, $\ge$ o igualdades $=$) que las variables de decisión deben satisfacer. Por ejemplo:

$$a_{11} x_1 + a_{12} x_2 + a_{13} x3 + ... + a_{1n} x_n \le b_1$$
$$a_{21} x_1 + a_{22} x_2 + a_{23} x_3 + ... + a_{2n} x_n = b_n$$
$$...$$
$$a_{m1} x_1 + a_{m2} x_2 +a_{m3} x_3 + ... + a_{mn} x_n \ge b_m$$

* **Parámetros ($C_j, A_{ij}, B_j$)**: Son datos ciertos o constantes del problema. Los $C_j$ acompañan a las variables en la función objetivo, los $A_{ij}$ son coeficientes en las restricciones y los $B_j$ representan las limitaciones o requerimientos (lado derecho).
* **Restricción de No Negatividad**: Condición que establece que todas las variables de decisión deben ser mayores o iguales a cero ($X_j \ge 0$). Por ejemplo

$$\forall x_j \geq 0 (j = 1, 2, ..., n)$$

* **Variables de Holgura ($S_n$)**: Son variables adicionales que se suman o restan a las inecuaciones de las restricciones para convertirlas en ecuaciones (igualdades). Representan recursos no utilizados o excesos sobre un límite mínimo.

---

## Desarrollo de la clase

### El proceso de formulación
Para llevar un problema real a una forma matemática general, el docente sugiere seguir una serie de pasos lógicos que aseguren que no se pierda información relevante del contexto:

1.  **Lectura y comprensión**: Analizar de qué trata la situación, qué se quiere determinar y cuál es el objetivo final.
2.  **Identificación de objetivos y limitaciones**: Listar verbalmente qué se busca optimizar y qué barreras o requerimientos existen.
3.  **Definición de variables de decisión**: Es fundamental definirlas de forma completa, especificando qué representan, su unidad de medida y de tiempo.
4.  **Traducción matemática**: Construir la función objetivo, el cuerpo de restricciones y la condición de no negatividad respetando la homogeneidad de las unidades de medida en cada término.

### Supuestos de la Programación Lineal
El docente menciona supuestos críticos que validan el uso de este modelo:
* **Certidumbre**: Se asume que todos los parámetros ($C_j, A_{ij}, B_j$) son conocidos y precisos.
* **Aditividad**: El valor total de la función objetivo y el uso total de recursos resultan de la suma de las contribuciones individuales de cada variable.
* **No negatividad**: Las variables no pueden tomar valores negativos en el mundo real (no se pueden producir $-10$ jabones).

### Aplicación práctica: Caso "La Espuma S.A."
Se analiza el problema 9 de la guía. La empresa fabrica tres productos: jabón de tocador (JT), detergente para vajillas (DV) y jabón para ropa (JR). El objetivo es maximizar el beneficio total.

#### Adaptación de datos unitarios
Un punto crucial explicado es que la información suele venir en bloques (ej. datos cada 100 unidades o costos cada 20 unidades). Para el planteo matemático, es obligatorio **convertir todo a base unitaria**. Por ejemplo, si el beneficio es de $\$200$ por cada 20 unidades de jabón, el coeficiente $C_j$ para la función objetivo será de $\$10$ por unidad.

#### Construcción de restricciones
* **Insumo base**: Se suman los consumos unitarios de cada producto multiplicados por su respectiva variable y se limita al total disponible ($4.500$ litros).
* **Presupuesto y Horas**: Se sigue la misma lógica para las 320 horas de proceso y los $\$600.000$ disponibles. Es importante notar que si un recurso (como las horas de empaque) no tiene límite, no constituye una restricción para el modelo.
* **Relaciones de producción**:
    * *Detergente vs. Jabón para ropa*: El detergente debe ser exactamente el $30\%$ de la producción de jabón para ropa ($DV = 0,30 \cdot JR$).
    * *Relación de costos*: El costo de producir jabón de tocador debe ser al menos el $20\%$ del costo total de producción.
    * *Límite de mercado*: El detergente no debe superar las 500 unidades ($DV \le 500$).

#### Objetivo
Maximizar el beneficio total por la produccion de los tres articulos de limpieza

#### Definicion de variables
* JT = Numero de unidades de jabon de tocador a producir
* DV = Numero de unidades de detergente para vajilla a producir
* JR = Numero de unidades de jabon para ropa a producir

#### Limitaciones
* Litros de insumo base
* Horas de proceso
* Presupuesto
* Relaciones entre variables
* Relaciones entre costos
* Produccion maxima de detergente para vajilla

#### Formulacion matematica - Planteo de la funcion objetivo

$$
Max\ Z\ [\$]= 10\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad] + 25\ \frac{[\$]}{[Unidad]}\ DV\ [Unidad] + 22\ \frac{[\$]}{[Unidad]}\ JR\ [Unidad] 
$$

#### Formulacion matematica - Planteo de las restricciones

* Litros de insumo base
$$
0,08\ \frac{[Litros]}{[Unidad]}\ JT\ [Unidad]\ +\ 0,12\ \frac{[Litros]}{[Unidad]}\ DV\ [Unidad]\ +\ 0,2\ \frac{[Litros]}{[Unidad]}\ JV\ [Unidad]\ \leq\ 4500\ [Litros]
$$

* Horas de proceso
$$
0,1\ \frac{[Hora]}{[Unidad]}\ JT\ [Unidad]\ +\ 0,16\ \frac{[Hora]}{[Unidad]}\ DV\ +\ 0,14\ \frac{[Hora]}{[Unidad]}\ JR\ \leq 320\ [Hora]
$$

* Presupuesto
$$
5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ +\ 15\ \frac{[\$]}{[Unidad]}\ DV\ [Unidad]\ +\ 18\ \frac{[\$]}{[Unidad]}\ JR\ [Unidad]\ \leq\ 600.000\ [\$]
$$

* Relacion detergente - jabon para ropa
$$
0,3\ DV\ [Unidad]\ =\ JR\ [Unidad]
$$

* Relacion de costos
$$
5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ \geq\ 0,2\ \left(5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ +\ 15\ \frac{[\$]}{[Unidad]}\ DV\ [Unidad]\ +\ 18\ \frac{[\$]}{[Unidad]}\ JR\ [Unidad]\right)
$$

* Produccion de detergente
$$
DV\ [Unidad]\ \leq\ 500\ [Unidad]
$$

* Supuesto de no negatividad
$$
JT\ [Unidad],\ DV\ [Unidad],\ JR\ [Unidad]\ \geq\ 0
$$

### Incorporación de Variables de Holgura
Una vez planteado el modelo original con desigualdades (inecuaciones), se introducen las variables de holgura para convertirlas en igualdades, lo cual es necesario para ciertos métodos de resolución.
* En restricciones de **menor o igual ($\le$)**, la variable de holgura se **suma** ($+S$). Representa el recurso que **no se utilizó** o lo que falta para llegar al límite.
* En restricciones de **mayor o igual ($\ge$)** (como el caso del costo mínimo), la variable representa cuánto se **excedió** el límite mínimo.
* En restricciones de **igualdad ($=$)**, no se agregan variables de holgura.

Trasladandolo al ejercicio

* Litros de insumo base: $S_1$ representa los litros de insumo base no utilizados
$$
0,08\ \frac{[Litros]}{[Unidad]}\ JT\ [Unidad]\ +\ 0,12\ \frac{[Litros]}{[Unidad]}\ DV\ [Unidad]\ +\ 0,2\ \frac{[Litros]}{[Unidad]}\ JV\ [Unidad]\ +\ S_1\ =\ 4500\ [Litros]
$$

* Horas de proceso: $S_2$ representa las horas de proceso no utilizadas
$$
0,1\ \frac{[Hora]}{[Unidad]}\ JT\ [Unidad]\ +\ 0,16\ \frac{[Hora]}{[Unidad]}\ DV\ [Unidad]\ +\ 0,14\ \frac{[Hora]}{[Unidad]}\ JR\ [Unidad]\ +\ S_2\ =\ 320\ [Hora]
$$

* Presupuesto: $S_3$ representa el presupuesto no utilizado
$$
5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ +\ 15\ \frac{[\$]}{[Unidad]}\ DV\ [Unidad]\ +\ 18\ \frac{[\$]}{[Unidad]}\ JR\ [Unidad]\ +\ S_3\ =\ 600.000\ [\$]
$$

* Relacion detergente - jabon para ropa: No utiliza variables de holgura
$$
0,3\ DV\ [Unidad]\ =\ JR\ [Unidad]
$$

* Relacion de costos: $S_4$ representa el costo del jabon de tocador por encima del 20% del costo total de produccion
$$
5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ -\ S_4\ =\ 0.2\ \left(5\ \frac{[\$]}{[Unidad]}\ JT\ [Unidad]\ +\ 15\ \frac{[\$]}{[Unidad]}\ DV\ [Unidad]\ +\ 18\ \frac{[\$]}{[Unidad]}\ JR\ [Unidad]\right)
$$

* Produccion de detergente: $S_5$ representa las unidades de detergente para vajilla por debajo del limite maximo de 500 unidades
$$
DV\ [Unidad]\ +\ S_5\ =\ 500\ [Unidad]
$$

* Supuesto de no negatividad
$$
JT\ [Unidad],\ DV\ [Unidad],\ JR\ [Unidad]\ \geq\ 0
$$

De esta forma queda planteado el problema lineal completo con las variables de holgura añadidas

---

## Ejemplos y casos mencionados

* **Caso La Espuma S.A.**: Producción de tres artículos de limpieza (jabón de tocador, detergente y jabón para ropa).
* **Analogía de la suma de beneficios**: Explicación de cómo el beneficio total es la suma de los beneficios individuales (aditividad).
* **Cancelación de unidades**: Ejemplo pedagógico de cómo multiplicar $\$ / \text{unidad} \times \text{unidades}$ resulta en $\$$ para asegurar que la función objetivo sea homogénea.

---

## Puntos que el docente remarcó

* **Homogeneidad de unidades**: El docente enfatizó repetidamente que tanto el lado izquierdo como el derecho de una restricción deben tener la misma unidad de medida.
* **Definición de variables**: No basta con decir "X es jabón", hay que especificar: "cantidad de unidades de jabón de tocador a producir en el período X".
* **Datos unitarios**: Remarcó el cuidado que hay que tener al leer las tablas, transformando siempre los datos (costos, insumos, beneficios) a valores por unidad de producto.
* **Significado de la holgura**: Recalcó que cada variable de holgura tiene un significado físico real dependiendo de la restricción donde se aplique (litros sobrantes, horas libres, etc.).

---

## Para el trabajo práctico / evaluación

* **Problema 9 de la guía**: Es el ejercicio base utilizado para explicar toda la teoría de planteo.
* **Requerimiento del planteo**: Un planteo completo debe incluir siempre tres partes: Definición de variables (verbal), Función Objetivo (numérica) y el Cuerpo de Restricciones (incluyendo la no negatividad).

---

## Dudas y cosas para revisar

* **Variables de excedente**: Aunque mencionó variables de holgura para restricciones de "por lo menos" (como $S_4$), conviene profundizar en la distinción técnica entre variables de *holgura* (recurso sobrante) y variables de *excedente* (exceso sobre el mínimo).
* **Tratamiento de variables en el denominador**: El docente mencionó brevemente que una relación puede expresarse como cociente ($DV/JR = 30/100$), pero que es mejor pasar términos para que quede lineal. Sería útil revisar cómo linealizar restricciones más complejas.