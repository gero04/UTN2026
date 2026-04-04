# **Introducción a la Simulación, Números Pseudoaleatorios y Pruebas Estadísticas**

**Materia:** Simulación  
**Resumen en una oración:** La clase introdujo las reglas de cursado, los conceptos fundamentales de simulación (discreta vs. continua) y se centró profundamente en la generación, propiedades y validación estadística (Pruebas de la Media, Varianza y Chi-Cuadrado) de los números pseudoaleatorios.

## **Conceptos clave**

* **Simulación:** Es una disciplina práctica que combina conocimientos de cuatro materias previas: Análisis Matemático, Programación, Análisis Numérico (ecuaciones diferenciales) y Estadística.  
* **Simulación Discreta:** Modelo donde los cambios de estado del sistema ocurren en instantes separados de tiempo (eventos). El sistema permanece inactivo hasta que ocurre un suceso específico que lo "despierta".  
* **Simulación Continua:** Modelo donde las variables cambian continuamente a lo largo del tiempo. El *tiempo* es la variable fundamental que diferencia a este modelo del discreto. Se utilizan ecuaciones diferenciales para modelar estos cambios.  
* **Números Aleatorios (Puros):** Son números generados por fenómenos de la naturaleza o del azar real (lotería, física cuántica, fenómenos atmosféricos). Son verdaderamente impredecibles.  
* **Números Pseudoaleatorios (RND):** Conjunto de números en el intervalo \[0, 1\) generados mediante fórmulas matemáticas deterministas por una computadora/calculadora. Se comportan estadísticamente de manera muy similar a los números aleatorios puros, pero al conocer el algoritmo y los valores iniciales, la secuencia puede ser predicha y reproducida.  
* **Semilla (**$X_0$**):** Es el valor o estado inicial que requiere un algoritmo para empezar a generar una secuencia de números pseudoaleatorios. Si se usa la misma semilla, el algoritmo generará exactamente la misma secuencia de números.  
* **Módulo / Resto:** Es el residuo de una división. En programación, funciones como mod(m) o el operador % devuelven este valor. Es fundamental en los algoritmos generadores para asegurar que los números se mantengan dentro de un rango específico.  
* **Período (o Ciclo de vida):** Es la cantidad de números pseudoaleatorios que un algoritmo puede generar antes de que la secuencia comience a repetirse irremediablemente.

## **Desarrollo de la clase**

### **1\. Tipos de Simulación**

La materia se divide principalmente en dos grandes paradigmas de simulación:

* **La vereda Discreta:** Hablamos de "discretizar" cuando simulamos cosas en base a *eventos*. El sistema tiene "tiempos muertos" donde no pasa nada hasta que un evento dispara una acción.  
* **La vereda Continua:** Se diferencia radicalmente porque el paso del tiempo es constante y las variables cambian con él sin saltos bruscos. En la programación de esta simulación, se establecen parámetros iniciales y ecuaciones diferenciales (análisis numérico) que dictan cómo se moverá y cambiará el sistema hasta una condición de finalización.

### **2\. Generación de Números Pseudoaleatorios (RND)**

Para incluir variabilidad en un modelo de simulación, necesitamos aleatoriedad. Como las computadoras son máquinas deterministas, no pueden crear azar real. Utilizan funciones preprogramadas (como la tecla RND en la calculadora Casio, o las funciones random() en Python, C, JavaScript, Excel).  
Estos algoritmos necesitan un punto de partida llamado **Semilla**. Habitualmente, los lenguajes de programación usan la fecha y hora exacta del sistema (milisegundos) como semilla por defecto, ya que es un valor que nunca se repite.

#### **Método Congruencial Lineal**

Es el algoritmo más clásico explicado para generar estos números. Utiliza la siguiente ecuación recursiva:

$$
X_{i+1} = (a \cdot X_i + c) \pmod{m}
$$
  
Donde:

* $X_0$ \= Semilla inicial.  
* $a$ \= Constante multiplicativa.  
* $c$ \= Constante aditiva.  
* $m$ \= Módulo.  
* *Todos deben ser números enteros mayores a cero.*

**Paso a paso para obtener el número RND:**  
El algoritmo de arriba genera *números enteros*. Para pasarlos al espectro de probabilidades \[0, 1), se debe hacer la siguiente división:

$$
rnd_i = \frac{X_{i+1}}{m - 1}
$$
  
*Nota: Un número RND puede ser exactamente 0, pero por convención matemática, nunca llegará a ser exactamente 1 (es un intervalo cerrado en 0 y abierto en 1).*  
**Condiciones para un generador exitoso (Período Máximo):**  
Para que la secuencia tarde lo máximo posible en repetirse (Período máximo $N = m$), se deben cumplir reglas matemáticas precisas:

1. $m = 2^g$ (donde $g$ es un entero positivo grande, ej. $2^{64}$).  
2. $a = 1 + 4k$ (donde $k$ es un entero positivo).  
3. $c$ debe ser **relativamente primo** a $m$ (es decir, el único divisor que comparten $c$ y $m$ es el 1; no comparten ningún otro divisor común en sus listas de divisores).

*(También existe el Método Congruencial Multiplicativo, donde* $c=0$*, ahorrando una operación computacional, explicado en el PDF 02).*

### **3\. Propiedades de los generadores de números RND**

Para que consideremos "bueno" a un generador (algoritmo), debe cumplir con:

* **Uniformidad:** Todos los números en el espectro deben tener exactamente la misma probabilidad de ocurrencia (como un dado perfecto).  
* **Independencia:** Un número generado no debe tener correlación con el anterior ni con el siguiente.  
* **Ciclo largo (Período):** La secuencia debe tardar muchísimo en repetirse. Cuanto más grande sea $m$, mayor será el espacio entre repeticiones.  
* **Reproducibilidad:** Si ingresamos la misma semilla y parámetros ($a, c, m$), el algoritmo **debe** devolver la misma secuencia. Esto es crucial para poder probar y depurar modelos de simulación.  
* **Imprevisibilidad / Resistencia a la predicción:** Aunque es determinista, a simple vista (o bajo análisis simple) no debe ser evidente cuál será el próximo número de la serie.  
* **Eficiencia (Uso de recursos computacionales):** El código debe usar la menor cantidad de memoria y tiempo de CPU posible. "Menos es más".  
* **Calidad de la aleatoriedad:** Se verifica sometiendo los números generados a estrictas pruebas estadísticas.

### **4\. Pruebas de Calidad (Bondad de Ajuste)**

Si tomamos una muestra de números (el profesor usó 228 números de lotería pasados al rango 0-1), no basta con mirarlos para saber si sirven. Hay 4 métodos estadísticos para comprobarlo: Prueba de la Media, Prueba de la Varianza, Prueba de Chi-Cuadrado ($\chi^2$) y Prueba de Kolmogorov-Smirnov (KS). Todos se basan en comparar lo **Observado (Empírico)** vs. lo **Esperado (Teórico)**.  
El proceso siempre arranca definiendo dos hipótesis:

* $H_0$ **(Hipótesis Nula):** Los datos *sí* corresponden a una distribución uniforme entre 0 y 1\. (Esta es la que queremos aceptar).  
* $H_1$ **(Hipótesis Alternativa):** Los datos *no* son uniformes.  
  Se establece un Nivel de Confianza (ej. $1 - \alpha = 0.95$, o sea 95%), dejando un Nivel de Significancia o Riesgo ($\alpha = 0.05$ o 5%).

#### **A. Prueba de la Media**

* **Teoría:** La media esperada de una distribución uniforme (0,1) es **0.5**.  
* **Práctica:** Se calcula el promedio de la muestra empírica (sumar todos y dividir por $n$). Ejemplo: dio $0.51$.  
* **Cálculo:** Se calcula el estadístico de prueba $Z_0$ con la fórmula:  
  
$$
Z_0 = \frac{|\text{Media Observada} - 0.5|}{\frac{\text{Desviación Estándar}}{\sqrt{n}}}
$$
  
* **Evaluación:** Se compara el resultado con el valor de la tabla Normal Estándar para $Z_{\alpha/2}$ (que para $\alpha=0.05$ suele ser $1.96$). Si $Z_0 \le Z_{tabulado}$, se acepta $H_0$.

#### **B. Prueba de la Varianza**

* **Teoría:** La varianza esperada de una distribución uniforme (0,1) es $1/12$ (aprox. 0.0833).  
* **Práctica:** Se calcula la varianza muestral $S^2 = \frac{\sum (x_i - \bar{x})^2}{n-1}$.  
* **Evaluación:** Utiliza la distribución Chi-Cuadrado ($\chi^2$). Se compara el estadístico calculado contra los límites tabulados (usando grados de libertad $v = n-1$).

#### **C. Prueba de Chi-Cuadrado ($\chi^2$)**

*Ideal para muestras de* $n \ge 30$*.*

* **Proceso:** Se divide el rango \[0, 1\) en $k$ intervalos (se recomienda $k = \sqrt{n}$).  
* Se cuenta cuántos números cayeron en cada intervalo. Esto es la **Frecuencia Observada (**$f_o$**)**.  
* Se calcula cuántos *deberían* haber caído si fuera perfectamente uniforme ($f_e = n / k$). Esta es la **Frecuencia Esperada (**$f_e$**)**. *Ojo:* $f_e$ *debe ser* $\ge 5$ *por intervalo, sino hay que agruparlos.*  
* **Fórmula:** Por cada intervalo se hace el siguiente cálculo y se suma todo al final:  
  
$$
\chi^2_{calculado} = \sum_{i=1}^{k} \frac{(f_{o_i} - f_{e_i})^2}{f_{e_i}}
$$
  
* **Evaluación:** Se compara contra el valor de la tabla Chi-Cuadrado usando $\alpha$ y los grados de libertad $v = k - 1$. Si $\chi^2_{calculado} \le \chi^2_{tabulado}$, se acepta $H_0$.

*(Nota: La prueba KS funciona de forma similar pero evaluando probabilidades acumuladas, ideal para muestras chicas de 10 a 30\. Ver PDF 03).*

## **Ejemplos y casos mencionados**

1. **Peaje / Guardia de seguridad (Simulación Discreta):** El empleado está ocioso esperando. No hace nada hasta que llega un auto. Ese es el evento que dispara el cambio de estado en el sistema (el tipo empieza a trabajar, la cola de autos crece).  
2. **Impresora 3D (Simulación Discreta):** La máquina está apagada. Empieza a imprimir (evento de inicio). Termina y ocurre el "evento de fin de impresión", que dispara otra acción (revisar la pieza).  
3. **Fábrica de autopartes (Simulación Continua):** Se prende a las 8 AM y el tiempo corre ininterrumpidamente. Las variables (producción, desgaste, insumos) cambian continuamente a lo largo del tiempo de operación.  
4. **Generación de Semillas reales:** Para lograr cosas "más aleatorias", la naturaleza es mejor. El profesor mencionó el caso real de *Cloudflare*, que utiliza una pared llena de "lámparas de lava" y una cámara web grabando sus movimientos impredecibles para crear claves criptográficas de altísima seguridad. *(¡Tu idea de la webcam/micrófono aplica exactamente a esto\!)*.  
5. **Criptografía y el algoritmo Diffie-Hellman:** Ejemplo de uso crítico de los RND. Dos computadoras generan números aleatorios enormes para crear y compartir claves de seguridad en la web sin ser interceptadas.  
6. **Juegos (Space Invaders vs. Juegos actuales):** En juegos viejos, el alien siempre salía por el mismo lado y en el mismo momento (no había aleatoriedad). En los juegos modernos (como Counter-Strike o FIFA), se usan RND para que los eventos, apariciones y colisiones sean impredecibles (uso práctico en videojuegos).  
7. **Duración de la carrera universitaria:** Ejemplo para explicar "Esperado vs. Observado". Lo esperado (Teórico) es recibirse en 5 años. Lo observado (Empírico) es que a la mayoría de los estudiantes les toma más tiempo.

## **Puntos que el docente remarcó**

* **¡LA PRÁCTICA ES TODO\!** Repitió múltiples veces que la materia es 80% práctica. Subrayó que *no se aprende simulación mirando videos en YouTube* ("por más que mires videos de asados, si no cortás la carne y prendés el fuego, no sabés"). Hay que sentarse a programar y hacer los cálculos.  
* **Uso eficiente de recursos:** Al programar los algoritmos, enfatizó que deben ser eficientes. "Un código de 200 líneas es mejor que uno de 1000 que consume toda la RAM". Evaluará la eficiencia de la programación.  
* **Dominio de los números aleatorios:** Es tan crítico este tema que los *dos primeros TPs enteros* y el primer parcial se basan exclusivamente en esto. Si no se entiende RND, no se puede avanzar.  
* **Módulo / Resto:** Insistió en asegurarse de que todos recuerden matemáticamente qué es el resto de una división, ya que es el corazón matemático del generador de números RND.  
* **Validación oral en los TPs:** Hizo una advertencia severa. En los trabajos grupales, si a un miembro del grupo se le pregunta por una parte del código o del análisis y no sabe responder, reprobará la instancia (independientemente del resto del grupo) y deberá ir a una instancia de recuperación ("lo van a tener que codear con sus manos en su máquina").

## **Para el trabajo práctico / evaluación**

* **Modalidad de los TPs:**  
  * **TP 1 y TP 2:** Individuales. Tema: Aleatorización de números (Generación y Pruebas).  
  * **TP 3, 4 y 5:** Grupales (máximo 8 personas). El TP 3 incluirá simulación discreta por método de Montecarlo.  
  * La presentación de los TPs grupales será sorteada (por tercios del curso).  
* **Fechas clave:**  
  * Parcial 1: 2 de mayo.  
  * Parcial 2: 13 de junio.  
  * Recuperatorio: 27 de junio.  
* **Condiciones de Aprobación/Promoción:**  
  * Deben estar aprobados los 5 TPs. Los TPs no llevan nota numérica, sino "Aprobado" o "No aprobado".  
  * Para promover la materia (no rendir final), se requiere sacar **7 o más** en ambos parciales. Quienes saquen menos, quedarán regulares y se les tomará examen teórico final (conceptos dictados por el profesor Daniel en las clases virtuales).  
* **Uso de Excel en TPs/Parciales:** El profesor utilizó Excel en clase para buscar valores de tablas estadísticas complicadas. Recomendó usar funciones como \=DISTR.NORM.ESTAND.INV() para $Z$ y \=INV.CHICUAD.CD(alfa, grados\_libertad) para la prueba Chi-Cuadrado (Ej: \=INV.CHICUAD.CD(0.05, 227)).

## **Dudas y cosas para revisar**

* **Idea de programación personal:** Evaluá implementar en el TP1 o TP2 tu idea de utilizar el micrófono/webcam para generar la semilla de tu algoritmo. Podés capturar el nivel de ruido ambiental de un instante específico o el color de un píxel aleatorio de la cámara web, convertirlo a un número entero y pasarlo como $X_0$. Es un gran plus.  
* **Cálculos manuales vs. Excel:** Asegurate de saber cómo leer las tablas impresas de Chi-Cuadrado y Normal Estándar, por si en el parcial no dejan usar Excel para la función INV.CHICUAD.CD. Las tablas en los PDFs tienen límites (la del PDF llega a 29 grados de libertad nomás), revisar si los profes subirán tablas más completas o permitirán software.  
* **Diferencia terminológica:** Revisar la diferencia exacta entre "impredecible" y "resistencia a la predicción". El docente admitió dudar un poco en la terminología técnica aunque en la práctica significan casi lo mismo (no poder adivinar el número $X_{i+1}$ incluso conociendo parte de la serie).