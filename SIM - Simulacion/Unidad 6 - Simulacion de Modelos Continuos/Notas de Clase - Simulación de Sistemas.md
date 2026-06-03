# **Sistemas Discretos y Continuos: Simulación y Métodos Numéricos**

**Materia:** Simulación de Sistemas / Modelos Numéricos  
**Resumen en una oración:** La clase comenzó con la resolución detallada de un modelo de simulación discreta de un puerto marítimo y la gestión dinámica de sus recursos (grúas), para luego introducir los sistemas continuos, la resolución analítica de ecuaciones diferenciales (crecimiento poblacional y decaimiento radiactivo) y la aplicación de métodos de integración numérica (Euler, Runge-Kutta, Predictor-Corrector) junto con el análisis de los errores relativos y absolutos.

## **Conceptos clave**

* **Sistema Discreto:** Un sistema donde las variables de estado cambian instantáneamente en puntos separados en el tiempo (eventos). En la clase se ejemplifica con la llegada o partida de barcos.  
* **Vector de Estado:** Conjunto de variables necesarias para describir el sistema en cualquier instante. En el problema del puerto, incluye el estado de la bahía (cola), los muelles (libre/ocupado) y las grúas (libre/ocupada).  
* **Sistema Continuo:** Un sistema donde las variables de estado cambian de forma continua a lo largo del tiempo. Suelen modelarse utilizando ecuaciones diferenciales ordinarias (EDO) o ecuaciones de diferencia, requiriendo medir variaciones en intervalos de tiempo minúsculos.  
* **Constante de crecimiento / decaimiento ($k$):** Parámetro de proporcionalidad que define a qué ritmo crece (si es positiva) o decae (si es negativa) una población o cantidad respecto a su tamaño actual a lo largo del tiempo.  
* **Vida Media (Half-life):** El tiempo necesario para que la mitad de los átomos de un material radiactivo en particular se desintegre a su estado base u otro isótopo. Es el tiempo $t$ tal que la cantidad restante es exactamente la mitad de la inicial $\left(\frac{C_0}{2}\right)$.  
* **Integración Numérica:** Métodos matemáticos (como Euler o Runge-Kutta) que se utilizan para encontrar aproximaciones numéricas a las soluciones de ecuaciones diferenciales, especialmente cuando la solución analítica es inviable. Funcionan calculando pendientes sucesivas y avanzando en pasos definidos ($h$).  
* **Error Absoluto:** La diferencia directa entre el valor obtenido mediante la aproximación numérica (ej. integración con Euler) y el valor analítico o real. Fórmula: $|Valor_{Aproximado} - Valor_{Real}|$.  
* **Error Relativo:** La división del Error Absoluto sobre el Valor Real. Se suele expresar en porcentajes y permite comprender si el error absoluto es significativo respecto a la magnitud de lo que se está midiendo.

## **Desarrollo de la clase**

### **1\. Simulación Discreta: El caso del Puerto**

La clase inicia analizando el modelo de un puerto donde arriban barcos.

* **Dinámica del sistema:** Los barcos llegan según una distribución exponencial (1 cada 25 días). El puerto tiene 1 dique con 2 muelles y 2 grúas. El tiempo de descarga usando 1 grúa es uniforme \[0,5; 1,5\] días.  
* **La complejidad de los recursos (Grúas y Muelles):** Si hay un solo barco en el puerto, las 2 grúas lo descargan simultáneamente, reduciendo el tiempo de descarga a la mitad. Si llega un segundo barco y ocupa el otro muelle, una de las grúas se desplaza al nuevo barco. En ese instante, el barco que estaba siendo descargado por dos grúas pierde una, por lo que *su tiempo restante de descarga se duplica*. A la inversa, cuando un barco finaliza, la grúa que queda libre se une a la que está trabajando en el muelle ocupado, dividiendo el tiempo restante a la mitad.  
* **Definición de Entidades y Estado:** No basta con tener la entidad "puerto". Es imperativo definir "Muelles" (Muelle 1 y Muelle 2), ya que determinan el cupo del sistema, y la "Bahía" (cola) donde los barcos esperan si ambos muelles están ocupados.  
* **Eventos:**  
  1. Llegada de barco.  
  2. Fin de descarga Muelle 1\.  
  3. Fin de descarga Muelle 2\. (Deben modelarse por separado, es un error agruparlos como un solo "Fin de descarga").  
* **Recálculo de tiempos en la Tabla de Eventos:** El profesor explica operativamente cómo recalcular en la tabla:  
  1. Si a un barco le quedaba un Tiempo de Descarga (TD) estipulado para $0.935$ días y el reloj actual es $0.43$: Tiempo faltante \= $0.935 - 0.43 - 0.505$.  
  2. Como se le retiró una grúa, venía a doble ritmo, por lo tanto el tiempo efectivo restante se duplica: $0.505 * 2$.  
  3. El nuevo Fin de Descarga se programa sumando el reloj actual más este nuevo tiempo efectivo.

### **2\. Introducción a Sistemas Continuos y Modelos Poblacionales**

El docente transiciona a los sistemas continuos, donde las variables (ej. población $P$) varían continuamente con el tiempo $t$.

* El modelo poblacional simple dice que la variación de la población $\left(\frac{dP}{dt}\right)$ es directamente proporcional a la población misma ($P$) multiplicada por una constante ($k$).  
* **Solución Analítica por Separación de Variables:**  
  1. Ecuación: $\frac{dP}{dt} - k * P$  
  2. Separación de variables: $\frac{dP}{P} - k * dt$  
  3. Se aplica la integral a ambos lados usando la condición inicial (tiempo $t_0$ y población inicial $P_0$):  
     $\displaystyle\int_{P_0}^{P}{\frac{1}{P}dP}-\int_{t_0}^{t}kdt$
  4. La primitiva de $\frac{1}{P}$ es $ln(P)$. Resultando en: $ln(P)-ln(P_0)-k(t-t_0)$.  
  5. Por propiedades de logaritmos: $ln\left(\frac{P}{P_0}\right)=k(t-t_0)$.  
  6. Aplicando la exponencial ($e$) a ambos lados: $\frac{P}{P_0}=e^{k(t-t_0)}$.  
  7. **Ecuación final:** $P(t)-P_0*e^{k(t-t_0)}$.  
* Por conveniencia matemática, casi siempre se puede asumir arbitrariamente que el instante inicial es $t_0-0$.

### **3\. Decaimiento Radiactivo (Aplicación del modelo)**

A diferencia del crecimiento, en el decaimiento la constante es negativa, modelando una reducción exponencial de la cantidad del material.

* **Carbono 14 (C-14):** Se da el dato de que la vida media es de 5230 años. Se evalúa el modelo: $C(5230)-\frac{C_0}{2}$.  
  Se plantea: $\frac{C_0}{2}-C_0*e^{-k*5230}$.  
  Se simplifica $C_0$ y se aplica logaritmo natural: $ln(0.5)-(-k)*5230$.  
  Se despeja $k$: $k=\frac{-ln(0.5)}{5230}$.  
* **Iodo 131 (I-131):** Misma lógica, pero la vida media es de 8 días. $k=\frac{-ln(0.5)}{8}\approx 0.08664$.

### **4\. Integración Numérica**

Cuando una ecuación diferencial no se puede resolver analíticamente, se recurre a aproximaciones paso a paso, iterando mediante un incremento fijo de tiempo llamado $h$.

* **Método de Euler:** El más simple. Usa el primer término de la serie de Taylor (una sola recta tangente por paso). Acumula bastante error rápidamente comparado con la curva real.  
* **Método de Runge-Kutta (4to orden):** Realiza cuatro evaluaciones intermedias (pendientes ponderadas) dentro de cada paso $h$, logrando asimilar hasta 4 términos de Taylor. Es mucho más exacto que Euler.  
* **Método Predictor-Corrector:** \* No es "autoiniciante"; requiere arrancar con 4 puntos iniciales calculados previamente (generalmente calculados con Runge-Kutta).  
  * *Fase Predictora:* Usa una fórmula que toma los últimos 4 puntos conocidos ($y_i,y_{i-1},y_{i-2},y_{i-3}$) para predecir el próximo valor ($y_{i-1}^p$).  
  * *Fase Correctora:* Reevalúa el punto tomando los últimos 3 puntos conocidos más el nuevo punto recién predecido. Esta fórmula correctora se puede iterar sobre sí misma 2 o 3 veces sin avanzar el $h$, hasta que el error converge (se minimiza la diferencia entre iteraciones de corrección). Recién ahí se acepta el punto y se avanza el $h$.

### **5\. Análisis de Errores Numéricos**

Al comparar los métodos en planillas tabuladas frente a la solución analítica, el docente enfatizó la interpretación del error.

* **Euler vs Runge-Kutta:** Para un mismo ejercicio, Euler llegó a tener un Error Relativo del 69%, mientras que el método Predictor-Corrector apenas un 2.66% y Runge-Kutta se mantenía en escalas bajísimas.  
* **El estallido del Error Relativo:** La fórmula del Error Relativo implica dividir sobre el valor real. El docente advirtió un fenómeno matemático fundamental: cuando el valor de la curva que estamos simulando se acerca a cero (cruza el eje $x$), el error relativo explota hacia valores altísimos (debido a la división por valores infinitesimales tendientes a cero). Aclaró que este pico de error es transitorio y se vuelve a normalizar cuando la curva se aleja de cero.

## **Ejemplos y casos mencionados**

1. **Simulación del puerto, muelles y grúas:** Usado exhaustivamente en la primera parte para enseñar a modelar recursos compartidos (grúas) y el recálculo dinámico de los tiempos (fines de descarga) en una tabla de simulación discreta.  
2. **Modelo Poblacional (Crecimiento de poblaciones):** Ejemplo matemático para resolver y derivar la ecuación general de $P_0*e^{k*t}$.  
3. **Radioactividad \- Iodo 131 para cáncer/hipertiroidismo:** Se mencionó la logística médica. Si el hospital pide I-131, dado el viaje de 72 horas (3 días), a la llegada al hospital le quedará solo el 77% del material original por el decaimiento radiactivo. Si se almacena otras 48 horas, cuando se le suministre al paciente quedará el 65%.  
4. **Pregunta trampa "Límite a infinito" del residuo radiactivo:** Cuando se pregunta "¿en qué tiempo el residuo desaparece completamente para descartarse sin precaución?". El profesor demostró que matemáticamente $t\rightarrow \infty$ y que el asintotismo exponencial implica que el material tiende a cero, pero nunca llega al 0 absoluto.  
5. **Base Marambio en la Antártida (Temperatura decreciente):** Se planteó un ejercicio donde la calefacción falla y la temperatura baja constantemente cruzando los 0°C. Sirvió para explicar dos cosas:  
   * En las tablas numéricas rara vez veremos el "0" exacto. Veremos un salto (ej: $t-2.7$ temperatura 0.8°C; $t-2.8$ temperatura \-0.3°C). Debemos responder dando el intervalo. (Reducir el $h$ achica el intervalo, pero no da un punto exacto).  
   * Este fue el ejemplo que utilizó para mostrar por qué el Error Relativo se dispara "al infinito" justo al acercarse a la temperatura de cero absoluto del problema.

## **Puntos que el docente remarcó**

* **¡Atención al modelar objetos\!** No poner objetos redundantes no es el problema mayor, el problema real es perder información por no modelar objetos clave (en el puerto, si no modelaban los "muelles" separados de las grúas, no se podía llevar correctamente el estado concurrente de 2 barcos).  
* **Interpretar el significado físico y no solo matemático:** Un modelo numérico nos puede dar números, y la matemática lo aguanta todo. (Ej: "La curva de población bajó de cero, se puso en negativos y rebotó hacia arriba"). Matemáticamente es un número, lógicamente significa que *"ya se murieron todos y no hay vuelta atrás"*. Hay que aplicar sentido común al contexto de la simulación.  
* **La aproximación numérica es solo eso, una aproximación:** Hay que ser honestos al comunicar resultados de simulación. Nunca tendremos el valor exacto donde la temperatura toca cero, solo un intervalo de confianza.

## **Para el trabajo práctico / evaluación**

* **Unificación de criterios para el parcial (Simulación Discreta):** El docente aclaró que el enunciado del parcial especificará *cuándo* se deben contar/acumular las variables estadísticas (Ej: acumular el tiempo en el ingreso a la cola, o contabilizar el tiempo solo cuando el elemento sale de la cola). Si se hace bien lógicamente cualquier enfoque funciona, pero para la evaluación exigen que todos sigan el mismo criterio para obtener los mismos números en la corrección automática.  
* **Herramientas para el parcial de integración numérica:**  
  * El parcial de la segunda etapa pedirá realizar integraciones numéricas.  
  * Principalmente pedirán el uso del método **Runge-Kutta de 4to orden**.  
  * Se permitirá usar computadoras/tablets y se aconseja tener preparada una planilla de cálculo (Excel o similar) pre-configurada con los métodos (Euler y Runge-Kutta) listos para usar y acelerar los cálculos.  
* **Trabajo Práctico N° 5:** Confirmado por el docente, este TP estará enfocado pura y exclusivamente en los sistemas continuos y la integración numérica.  
* **Paros y exposiciones:** Se mencionó que hay un gran impacto por paros docentes (28, 29 de mayo y 4 de junio). Mencionan las fechas de exposición para el 29 de junio. Afecta fuertemente el calendario.

## **Dudas y cosas para revisar**

* **Matemática de Ecuaciones Diferenciales:** Hubo confusión en el aula sobre las reglas de integración y las primitivas. **¡Revisar urgente\!** Específicamente la regla de potencias ($\int x^n dx$) y la primitiva de $\int \frac{1}{x} dx -ln(x)$. Fundamental para poder despejar variables por métodos analíticos.  
* **Método Predictor-Corrector:** El docente aclaró explícitamente: *"No les vamos a pedir este método"* (en los exámenes). Sin embargo, valió la pena la explicación teórica para entender que es un método que no avanza instantáneamente en el paso $h$, sino que itera y refina la precisión en el mismo punto antes de saltar. Conviene tener la teoría clara, aunque operativamente bastará con llevar Runge-Kutta armado al parcial.