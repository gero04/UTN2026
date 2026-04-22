# **Soluciones en Programación Lineal, Teoremas Fundamentales y Algoritmo Simplex**

**Materia:** Investigación Operativa  
**Resumen en una oración:** La clase repasó la resolución gráfica de programas lineales, profundizó en la clasificación de las soluciones (factibles, básicas, degeneradas), explicó los tres teoremas fundamentales basados en la convexidad y describió de forma intuitiva/gráfica cómo opera el algoritmo Simplex para encontrar el óptimo.

## **Conceptos clave**

* **Problema Canónico (Máximo/Mínimo):** Un programa lineal de maximización está en forma canónica cuando *todas* sus restricciones estructurales son de menor o igual ($\le$). Si es de minimización, es canónico cuando todas son de mayor o igual ($\ge$).  
* **Problema Estándar:** Un programa lineal donde todas las restricciones están expresadas como igualdades ($=$).  
* **Variables de Holgura:** Variables que se suman a una restricción de menor o igual ($\le$) para convertirla en igualdad. Representan la cantidad de recurso disponible que *no* se está utilizando.  
* **Variables de Excedente:** Variables que se restan a una restricción de mayor o igual ($\ge$) para convertirla en igualdad. Representan lo que está por encima del límite mínimo requerido.  
* **Solución (en Programación Matemática):** Un vector con valores numéricos que cumple con todas las restricciones del programa, incluyendo las variables de holgura/excedente. (Nota: en la matemática general, pueden ser valores negativos, nulos o positivos).  
* **Solución Factible o Posible:** Un vector que cumple con las restricciones funcionales (ecuaciones) y además cumple con la restricción de no negatividad del modelo de programación lineal (todos sus valores son $\ge 0$).  
* **Solución Básica:** Dentro de las infinitas soluciones de un sistema indeterminado, es un subconjunto finito que se obtiene anulando (haciendo cero) $n - m$ variables (donde $n$ es el total de variables y $m$ las restricciones).  
* **Solución Factible Básica:** Una solución que tiene como máximo $m$ valores positivos y los restantes $n - m$ valores son nulos, y además cumple con la no negatividad. Gráficamente, corresponden a los **vértices** del poliedro de soluciones.  
* **Solución Factible Básica Degenerada:** Ocurre cuando la solución tiene *menos* valores positivos que el número de ecuaciones $m$ (es decir, hay más ceros de los esperados). Gráficamente se ve como la intersección de más de dos rectas o restricciones en un mismo vértice.  
* **Combinación Lineal Convexa:** Operación entre dos o más vectores (puntos) multiplicados por escalares $\alpha_i$, donde se imponen dos condiciones: $0 \le \alpha_i \le 1$, y la suma de todos los $\alpha_i$ es igual a 1\. El resultado es un punto que recae sobre el segmento de recta que une a los puntos originales.  
* **Conjunto Convexo:** Un conjunto de puntos donde, si se toman dos puntos cualesquiera del conjunto y se unen con un segmento de recta, todo ese segmento de recta pertenece también al conjunto (ej. un círculo o un polígono sin huecos ni entrantes; una estrella *no* es convexa).

## **Desarrollo de la clase**

### **1\. Resolución Gráfica y Restricciones Limitantes**

La clase inició retomando un ejemplo práctico de una consultora de microservicios. Al observar el gráfico de la región factible, el docente explicó cómo identificar qué restricciones dictan el punto óptimo:

* **Restricciones limitantes:** Son aquellas sobre las cuales se asienta el punto óptimo (la intersección de sus rectas forma el vértice óptimo). Significa que se utiliza la totalidad de ese recurso. Algebraicamente, se comprueba porque el valor de su variable de holgura es cero.  
* **Restricciones no limitantes:** Son aquellas cuyo límite no fue alcanzado por el punto óptimo. Para saber cuánto recurso se usó realmente, se reemplazan los valores óptimos ($x_1, x_2$) en la inecuación de la restricción. La diferencia entre lo disponible y lo usado es el valor de la variable de holgura.

### **2\. Variables de Holgura y Excedente**

Para pasar de un modelo gráfico/canónico a la resolución algebraica (necesaria para el Simplex), es obligatorio transformar las inecuaciones en igualdades incorporando variables extra:

* Las variables no se pueden definir "en general", su significado depende del problema y de la unidad de medida de la restricción (ej. horas de arquitectura no usadas).  
* En la función objetivo ($Z$), estas variables llevan un coeficiente de $0$, porque el simple hecho de que sobren recursos no aporta utilidad, a menos que el problema indique explícitamente que el recurso sobrante se puede vender (en cuyo caso dejaría de ser una variable de holgura para ser una de decisión).  
* **Total de variables del modelo:** $n = \text{Variables de decisión} + \text{Variables de holgura/excedente}$.

### **3\. Clasificación de Soluciones en Sistemas de Ecuaciones**

Un sistema de restricciones lineal ($m$ ecuaciones, $n$ variables, donde $n > m$) es un sistema compatible indeterminado con infinitas soluciones.

* Para encontrar las **soluciones básicas**, se igualan a cero $n - m$ variables. Las variables que quedan forman un sistema de $m \times m$ que arroja valores.  
* El número *máximo* de soluciones básicas está dado por el número combinatorio de $n$ elementos tomados de $m$ en $m$: $\binom{n}{m}$. Esta fórmula marca la cota superior o límite máximo de vértices que podría tener el problema.

### **4\. Los Tres Teoremas Fundamentales**

El docente explicó la teoría matemática que permite que el algoritmo Simplex funcione, sin pedir demostraciones algebraicas, pero exigiendo su comprensión conceptual.

* **Teorema 1 (De convexidad de soluciones):** "Toda combinación lineal convexa de soluciones factibles de un programa lineal da como resultado otra solución factible".  
  * *¿Qué demuestra?* Que el conjunto (poliedro) de soluciones factibles de cualquier programa lineal es siempre un conjunto convexo.  
  * *Consecuencia:* Un programa lineal solo puede tener 3 estados de soluciones factibles: el conjunto es vacío (cero soluciones), tiene un único elemento (una solución), o tiene infinitas soluciones. No existen problemas con "20" o "100" soluciones aisladas.  
* **Teorema 2 (Líneas de isoutilidad/isocosto):** "Toda combinación lineal convexa de dos o más soluciones factibles que le dan a $Z$ el *mismo* valor, dará otra solución factible con exactamente ese mismo valor para $Z$".  
  * *¿Qué demuestra?* La existencia de las "rectas de Z" (isoutilidad). Si unimos dos puntos óptimos, todos los puntos del segmento que los une también son óptimos.  
  * *Consecuencia:* Al igual que las soluciones factibles, un programa lineal puede no tener solución óptima, tener UNA única solución óptima, o tener INFINITAS soluciones óptimas (cuando $Z$ es paralela a una restricción limitante).  
* **Teorema 3 (Teorema Fundamental de la Programación Lineal):** "Si un problema es resoluble (posee óptimo), la solución óptima se encontrará en *al menos una* de sus soluciones factibles básicas (vértices)".  
  * Por esto, no hace falta buscar el óptimo en el centro del polígono de soluciones; basta con explorar únicamente los vértices.

### **5\. Cómo trabaja el Algoritmo Simplex (Enfoque Gráfico)**

El método desarrollado por George Dantzig aprovecha el Teorema 3\. En vez de calcular todas las combinaciones $\binom{n}{m}$ posibles, Simplex hace una búsqueda inteligente:

1. **Fase inicial:** Identifica una primera solución factible básica. En problemas de máximo canónico apoyados en el origen, esta es muy fácil de hallar: $x_1 = 0, x_2 = 0$. En ese punto (el origen), las variables de holgura toman el valor total del lado derecho de las restricciones ($s_1 = b_1$, etc.).  
2. **Evaluación de optimalidad:** Se pregunta si la solución actual es óptima. Para ello, evalúa el "incremento marginal unitario" en Z si se moviera a los vértices adyacentes.  
3. **Iteración (Movimiento):** Si la solución no es óptima, se mueve a un vértice adyacente que mejore la función objetivo. Gráficamente, esto significa recorrer una arista del poliedro. Matemáticamente, significa que *una* variable que era cero (ej. $x_1$) se vuelve positiva, y *una* variable que era positiva (la holgura de la restricción que ahora será limitante) se vuelve cero.  
4. **Parada:** El proceso se repite hasta llegar a un vértice donde cualquier movimiento hacia un vértice adyacente hace decrecer (o empeorar) a Z. Como la región es convexa, un óptimo relativo frente a sus vértices adyacentes es garantizadamente el óptimo absoluto.

### **6\. Tratamiento de Valores Negativos en el Lado Derecho (RHS)**

Antes de empezar Simplex (y antes de agregar las variables de holgura), el sistema debe estar preparado. Si una restricción tiene un valor negativo a la derecha de la desigualdad:

* **Regla:** Multiplicar **ambos lados** de la inecuación por $-1$.  
* **Efecto:** Se invierte el sentido de la desigualdad ($\le$ pasa a ser $\ge$, o viceversa) y el valor del lado derecho queda positivo.  
* **Por qué se hace:** Porque el lado derecho formará parte de la primera solución básica factible. Si se deja negativo, se violaría la restricción de no negatividad de las variables desde el inicio.

## **Ejemplos y casos mencionados**

* **La consultora de software:** Ejemplo base utilizado para ver la resolución gráfica de variables (Microservicios A y B, uso de horas de arquitectura y programación).  
* **El problema "no acotado" (utopía):** El docente dio el ejemplo de una función de máximo donde la región factible está abierta hacia el infinito (se puede producir infinito de A y B). Aclaró que esto *no existe en la realidad* ("nadie tiene más hambre ni problemas de plata"), pero matemáticamente puede suceder e indica que el modelo está mal formulado o le faltan restricciones reales del sistema.

## **Puntos que el docente remarcó explícitamente (¡IMPORTANTE\!)**

* **Ojo con la definición de Holgura:** Es FALSO que las variables de holgura puedan ser negativas. Las variables de holgura **siempre son no negativas**. El hecho de que una variable de excedente vaya restada en la ecuación (con coeficiente \-1) no significa que la variable en sí valga un número negativo. *Aclaró que esta confusión les costó puntos a muchos alumnos en parciales anteriores.*  
* **Concepto vs. Mecánica:** La parte de formular/modelizar es la más complicada porque no es mecánica; requiere entrenar y practicar con los ejercicios de la guía.  
* **Algoritmo Simplex de Karkar (Interior Point Method):** Mencionó un algoritmo que va por "adentro" de la región factible y que matemáticamente es más eficiente, pero aclaró que por simulaciones empíricas, Simplex demostró ser más veloz en la mayoría de problemas industriales; por eso los softwares modernos usan el Simplex Revisado.

## **Para el trabajo práctico / evaluación**

* **Glosario:** El docente recomendó enfáticamente ir armando un "glosario de conceptos básicos" (solución factible, canónico, estándar, limitante, etc.) porque se da por sentado que los alumnos los manejan y no se volverán a explicar clase a clase.  
* **Evaluaciones teóricas:** Suelen haber preguntas de "Verdadero/Falso y justifique" sobre los conceptos de soluciones y holguras.  
* **Material de apoyo:** Instó repetidas veces a usar el libro de la cátedra, los videos y la guía, los cuales tienen ejercicios con sus respectivas respuestas. También sugirió que se puede usar ChatGPT (con buenos prompts) para que funcione como tutor paso a paso, pero advirtió sobre la diferencia de enfoque (IA usa vértices desde el principio, la cátedra prefiere el análisis visual de las curvas de nivel o rectas Z).

## **Dudas y cosas para revisar antes de la próxima clase**

* **Para la próxima clase (Algoritmo Simplex en tabla):** El docente indicó que es crucial repasar:  
  * **Operaciones elementales entre filas** (Álgebra).  
  * **Resolución de sistemas mediante método de Gauss-Jordan**.  
  * *Razón:* El núcleo de la fase iterativa de Simplex se basa enteramente en realizar operaciones elementales en matrices para actualizar la tabla.