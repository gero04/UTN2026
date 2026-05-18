# **Método Simplex: Casos de Minimización y Técnica de la Base Artificial**

**Materia:** Investigación Operativa
**Resumen en una oración:** La clase repasa los pasos generales del algoritmo Simplex, explica en detalle cómo adaptar el método para resolver problemas de minimización y presenta la Técnica de la Base Artificial para encontrar una solución básica factible inicial cuando el modelo tiene restricciones de mayor o igual ($\ge$).

## **Conceptos clave**

* **Método Simplex:** Es un algoritmo iterativo (mecánico) utilizado para resolver problemas de programación lineal. A diferencia de la formulación del modelo (que requiere interpretación y representación matemática de la realidad), el Simplex es un proceso sistemático que, con práctica, no debería presentar problemas.  
* **Valor $C_j - Z_j$:** Representa el incremento neto unitario, incremento marginal unitario, o tasa de crecimiento de la función objetivo ($Z$). Indica cuánto crecerá (o disminuirá) $Z$ si el valor de una variable no básica se incrementa en una unidad (pasando de 0 a un valor positivo).  
* **Variable de Holgura / Excedente:** Variables que se agregan a las restricciones para convertirlas de inecuaciones a ecuaciones (forma estándar). Tienen coeficiente $0$ en la función objetivo porque no aportan valor al mismo.  
* **Vectores $i$\-ésima unidad (o vectores unidad):** Vectores columna en la matriz de coeficientes que tienen un $1$ en una posición $i$ y $0$ en el resto. Son fundamentales para armar la matriz identidad que conforma la base inicial del Simplex.  
* **Variables Artificiales:** Variables ficticias que se agregan al modelo matemático original para forzar la creación de vectores unidad y así poder obtener una primera solución básica factible. No pertenecen al problema real.  
* **Penalización (Costo o "M"):** Coeficiente artificialmente muy grande (negativo en maximización, positivo en minimización) que se le asigna a las variables artificiales en la función objetivo para obligar al algoritmo a sacarlas de la base óptima.

## **Desarrollo de la clase**

### **1\. Tratamiento de problemas de Mínimo en Simplex**

Existen dos formas de trabajar un problema de minimización con el método Simplex:  
**Forma 1 (Matemática \- No recomendada por la profesora):**

* Minimizar una función $Z$ es matemáticamente equivalente a maximizar la función $-Z$.  
* Se multiplica toda la función objetivo por $-1$ y se resuelve el problema como si fuera de maximización.  
* Al llegar al resultado final, se debe volver a multiplicar el valor de $Z$ por $-1$.  
* *Desventaja:* Suele generar confusiones en los exámenes (los estudiantes dudan si multiplicar también las restricciones o se olvidan de revertir el signo al final).

**Forma 2 (Directa \- La que se usa en la cátedra):**

* Se trabaja el problema como un mínimo real. Para esto, **solo cambian dos cosas**: el criterio de optimidad y el criterio de la variable que entra a la base.  
* **Criterio de optimidad:** La solución es óptima cuando todos los valores de la fila $C_j - Z_j$ son mayores o iguales a cero ($\ge 0$). Esto significa que cualquier cambio futuro solo incrementaría el valor de $Z$ (y como buscamos el mínimo, no queremos que incremente).  
* **Variable que entra a la base:** Si la solución no es óptima (hay valores negativos en $C_j - Z_j$), ingresa a la base la variable que tenga el valor **más negativo** (el mínimo, el más alejado del origen/cero). Esta variable es la que hará disminuir a $Z$ más rápidamente.

### **2\. Criterio de la variable que sale de la base (¡IMPORTANTE\!)**

* **Regla de oro:** El criterio para decidir qué variable SALE de la base **NO CAMBIA**, sin importar si el problema es de máximo o de mínimo.  
* Se calcula el cociente $\theta$ (Tita): Se divide la columna Solución ($\lambda_i$) entre los valores de la columna de la variable que entra ($\lambda_{ij}$), *solo para denominadores mayores a cero*.  
* **Se elige siempre el mínimo cociente $\theta$.**  
* *¿Por qué no cambia?* Porque este criterio no tiene nada que ver con la función objetivo, sino con la región factible. Garantiza que nos movamos de un vértice adyacente a otro dentro del poliedro de soluciones.  
* *¿Qué pasa si no elijo el mínimo?* Nos iríamos a una solución básica NO factible, lo cual se evidenciaría en la siguiente tabla al aparecer valores negativos en la columna solución.

### **3\. Repaso general de los pasos del Método Simplex**

1. **Llevar el problema a la forma estándar:** Convertir inecuaciones en igualdades agregando variables de holgura (sumadas para $\le$) o excedente (restadas para $\ge$).  
2. **Identificar la primera solución factible básica:** Buscar $m$ vectores $i$\-ésima unidad en la matriz de coeficientes (tantos como restricciones haya) para formar la base canónica. Las variables correspondientes a estos vectores serán las básicas (positivas) y el resto serán nulas.  
3. **Armar la tabla inicial y analizar la optimidad:** Calcular la fila $C_j - Z_j$.  
   * *Máximo:* Óptimo si todos son $\le 0$. Entra el más positivo.  
   * *Mínimo:* Óptimo si todos son $\ge 0$. Entra el más negativo.  
4. **Determinar variable que sale:** Calcular $\theta$ (mínimo cociente válido). El valor de $\theta$ indica con qué valor físico ingresará la nueva variable a la base.  
5. **Actualizar la tabla (Operaciones elementales de fila):**  
   * Intersección de variable que entra y sale \= Elemento Pivot.  
   * Dividir toda la fila pivot por el elemento pivot para obtener un $1$.  
   * Hacer ceros por arriba y por abajo del pivot multiplicando la fila pivot por el opuesto del número a anular y sumándolo a la fila correspondiente.  
6. **Recalcular $Z_j$ y $C_j - Z_j$:** $Z_j$ es la suma producto del vector de coeficientes de la base ($C_i$) por cada columna.  
7. **Control rápido de $Z$:** El nuevo valor de $Z$ será igual al $Z$ anterior más el incremento neto ($C_j - Z_j$) multiplicado por el valor de $\theta$.

### **4\. Técnica de la Base Artificial (Problemas sin base canónica inicial)**

Cuando tenemos restricciones de $\ge$ o $=$, al estandarizar el modelo restamos variables de excedente (coeficiente $-1$). Esto hace que no tengamos los vectores unidad positivos (ej. no tenemos el vector $(1,0,0)$). No se puede multiplicar la fila por $-1$ porque el lado derecho de la solución quedaría negativo, rompiendo la condición de no negatividad.  
**Pasos de la técnica:**

1. **Agregar variables artificiales ($A_1,A_2,...$):** Se suman a las restricciones donde haga falta generar el vector unidad. Estas variables forman la primera base.  
2. **Penalizar en la función objetivo:** Como estas variables no son parte del problema original, debemos asegurar que el algoritmo las elimine.  
   * *En Maximización:* Se les asigna un coeficiente negativo muy grande (ej. $-5000$).  
   * *En Minimización:* Se les asigna un coeficiente positivo muy grande (ej. $+5000$).  
3. **Resolver con Simplex:** Se itera normalmente. Mientras haya variables artificiales en la base con valor positivo, la solución pertenece al problema modificado, no al original.

**Tres situaciones posibles al finalizar el algoritmo:**

1. **Solución óptima normal:** Las variables artificiales salen de la base, llegamos al óptimo y tenemos la solución de nuestro problema original.  
2. **Problema Incompatible (No factible):** Se cumple la condición de optimidad en la fila $C_j - Z_j$, pero **aún queda una variable artificial en la base con un valor mayor a cero**. Esto significa que el problema original no tiene solución (las restricciones son incompatibles).  
3. **Solución Degenerada:** Se llega al óptimo y queda una variable artificial en la base, pero **su valor en la columna solución es exactamente cero ($0$)**. Es una solución válida para el problema original, pero es "degenerada" porque hay menos de $m$ variables con valor estrictamente positivo.

## **Ejemplos y casos mencionados**

* **Variable de holgura con valor económico:** La profesora aclaró que si un problema dice que "las horas de máquina no utilizadas se pueden vender o alquilar", esa diferencia deja de ser una variable de holgura con coeficiente cero y pasa a ser una variable principal / de decisión con un coeficiente real en la función objetivo.  
* **Penalización en software (Lindo):** Al cargar el modelo en un software, los coeficientes de las variables artificiales deben diferenciarse mucho de los reales. Si las variables reales ganan $100$ o $120$, a la artificial se le debe poner $-5000$ (en caso de máximo) para asegurar que el sistema la saque.

## **Puntos que el docente remarcó**

* **Criterio de salida (¡Pregunta de examen\!):** El criterio para sacar una variable de la base (el mínimo cociente $\theta$) **jamás** cambia, sea el problema de máximo o mínimo. Si no se respeta, la solución se vuelve no factible.  
* **Terminología:** $C_j - Z_j$ **no es una variable**, es una "diferencia" o un "valor". (Mencionó explícitamente no escribir "la variable $C_j - Z_j$" en los parciales).  
* **Cuidado con el signo del coeficiente artificial:** Si es Maximización y le pongo penalización de $-2000$, el coeficiente es $-2000$. Hay que tener cuidado de no cargarlo mal en la tabla, porque si se pone positivo por error, el algoritmo nunca sacará la variable artificial y dirá que el problema original no tiene solución.  
* **Sobre las evaluaciones:** Para tranquilizar a los alumnos, aclaró que en parciales y finales no van a pedir resolver a mano tablas Simplex excesivamente largas de 3 o 4 iteraciones; a lo sumo serán 2 tablas.

## **Para el trabajo práctico / evaluación**

* **Avisos administrativos importantes:** A la hora de rendir un examen, el aula que figura en el comprobante al momento de la inscripción **no es el aula real**. El aula definitiva se publica recién **24 horas antes** del examen. (Hubo estudiantes que perdieron 1 hora buscando a la profesora por este error).  
* **Tarea/Práctica:** La profesora instó a practicar haciendo por lo menos tres problemas resueltos a mano antes del examen.  
* **Material de apoyo:** \* Recomendó mucho un video grabado en pandemia por el profesor Martín Hualpa (dura unos 40-42 minutos) para quienes aún tengan dudas con la base del Simplex.  
  * Hacer el cuestionario "Simplex T" (Cuestionario Simplex Teórico) en el Aula Virtual, que permite cargar los resultados de las tablas para autoevaluarse.  
  * Hacer las "Guías de Estudio" del aula virtual, ya que responder esas preguntas teóricas sirve directamente para estudiar.

## **Dudas y cosas para revisar**

* **Completar la resolución:** Al final de la clase se asignó un ejercicio práctico de Técnica de Base Artificial que, según la profesora, requerirá "al menos dos tablas" para resolverse. Los alumnos se pusieron a trabajar en esto en clase. Conviene realizar este ejercicio por cuenta propia para asimilar el tema de la penalización $M$.  
* Revisar el capítulo 3 del libro (mencionado en clase) para repasar Operaciones Elementales de Fila (Gauss-Jordan) en caso de no recordarlo de Álgebra.