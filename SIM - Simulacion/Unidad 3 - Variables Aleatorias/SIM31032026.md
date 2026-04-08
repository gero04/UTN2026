# **Apuntes de Clase: Método de la Transformada Inversa**

**Materia:** Simulación
**Resumen en una oración:** La clase detalla el Método de la Transformada Inversa, un procedimiento matemático fundamentado en integrales que permite convertir números pseudoaleatorios uniformes (0,1) en variables aleatorias que sigan cualquier distribución específica (continua o por partes) requerida por un problema.

## **Conceptos clave**

* **Método de la Transformada Inversa:** Procedimiento utilizado para fabricar un generador de variables aleatorias con una distribución específica (custom). Transforma una serie de números uniformes entre 0 y 1 provenientes de un generador estándar (como RND o el congruente) en números que siguen la probabilidad de la distribución deseada.  
* **Función de Densidad (**$f(x)$**):** Representa la probabilidad matemática de un punto o la curva que queremos modelar. El área total bajo esta curva en todo su dominio siempre debe ser igual a 1\.  
* **Función de Distribución Acumulada (**$F(x)$**):** Es la integral definida de la función de densidad. Mientras $f(x)$ da la probabilidad en un punto, $F(x)$ da la probabilidad de un área (probabilidad acumulada hasta un valor $x$).  
* **Valor de Corte:** En funciones definidas por partes, es el valor del área total (superficie acumulada) de la porción anterior de la función. Define el límite probabilístico (entre 0 y 1\) para decidir qué ecuación de generación ($x_1$, $x_2$, etc.) se debe usar para un número aleatorio dado.  
* **Variable Uniforme (0,1):** Denominada en clase como RND, ri o U(0,1). Es el número pseudoaleatorio puro que entra como parámetro. Teóricamente va de 0 a 0.9999..., el 1 puro nunca se genera.

## **Desarrollo de la clase**

### **El objetivo del método**

Normalmente existen fórmulas directas para distribuciones conocidas (Uniforme, Exponencial Negativa, Poisson, Normal). Sin embargo, cuando nos enfrentamos a problemas de la realidad cuyas probabilidades no responden a estas distribuciones clásicas, necesitamos fabricar un "generador a medida". Esto requiere obtener la función inversa de la distribución acumulada.  
*Nota del docente:* Hay que saber integrar, pero el foco de la materia no está en resolver integrales complejísimas (tema de Análisis Matemático), sino en saber aplicar el método correctamente.

### **Los 4 pasos del Método**

El docente remarcó estos 4 pasos fundamentales que siempre hay que seguir:

1. **Definir la función** $f(x)$**:** Obtener la función de densidad que represente la variable. A veces el ejercicio la da servida, otras veces hay que deducirla de un gráfico.  
2. **Calcular la función de distribución acumulada** $F(x)$**:** Se logra calculando la integral definida de la $f(x)$ obtenida en el paso 1\.  
3. **Determinar la función inversa:** Se equipara el resultado de la integral $F(x)$ a una variable aleatoria uniforme (que simbolizamos como RND). Queda la ecuación $RND = F(x)$. Luego, hay que despejar matemáticamente la variable $x$.  
4. **Generar las variables aleatorias:** Utilizar la fórmula final obtenida alimentándola con números RND (entre 0 y 1\) para obtener valores de la variable en el rango y con la distribución deseada.

### **Demostración 1: Distribución Uniforme entre A y B**

Para entender de dónde salen las fórmulas pre-hechas. Queremos generar valores uniformes entre un mínimo $A$ y un máximo $B$.

* **Paso 1:** La función de densidad para una distribución uniforme $A, B$ es una constante:  
  
$$
f(x) = \frac{1}{B - A}
$$
  
* **Paso 2:** Calculamos la integral definida entre el extremo inferior $A$ y $x$.  
  
$$
F(x) = \int_{A}^{x} \frac{1}{B - A} \\, dx
$$
  
  Como $\frac{1}{B - A}$ es constante, sale de la integral:  
  
$$
F(x) = \frac{1}{B - A} \int_{A}^{x} 1 \\, dx
$$
  
  La integral indefinida de $1 \\, dx$ es $x$. Aplicando regla de Barrow (extremo superior menos inferior):  
  
$$
F(x) = \frac{1}{B - A} (x - A) = \frac{x - A}{B - A}
$$
  
* **Paso 3:** Igualamos a RND y despejamos $x$.  
  
$$
RND = \frac{x - A}{B - A}
$$
$$RND \cdot (B - A) = x - A
$$
$$x = A + RND \cdot (B - A)
$$
  
  *(Este es el generador oficial para distribuciones uniformes no estandarizadas).*

### **Demostración 2: Distribución Exponencial Negativa**

* **Paso 1:** $f(x) = \lambda e^{-\lambda x}$ para $x \ge 0$.  
* **Paso 2:** Integral definida entre 0 y $x$.  
  
$$
F(x) = \int_{0}^{x} \lambda e^{-\lambda x} \\, dx
$$
  
  El docente resolvió esto por sustitución: $u = -\lambda x \implies du = -\lambda \\, dx \implies dx = \frac{du}{-\lambda}$.  
  La integral indefinida resulta en $-e^{-\lambda x}$.  
  Aplicando Barrow entre 0 y $x$:  
  
$$
F(x) = (-e^{-\lambda x}) - (-e^{-\lambda \cdot 0})
$$
  
  Como $e^0 = 1$, nos queda:  
  
$$
F(x) = 1 - e^{-\lambda x}
$$
  
* **Paso 3:** Igualar y despejar.  
  
$$
RND = 1 - e^{-\lambda x}
$$
$$e^{-\lambda x} = 1 - RND
$$
  
  Aplicando logaritmo natural ($\ln$) a ambos lados:  
  
$$
-\lambda x = \ln(1 - RND)
$$
$$x = -\frac{1}{\lambda} \ln(1 - RND)
$$
  
  *Nota importante del docente:* Dado que estadísticamente generar 1 \- RND es exactamente lo mismo que generar RND (si el generador funciona bien y usamos una muestra suficiente), es muy común ver y usar la fórmula simplificada:  
  
$$
x = -\frac{1}{\lambda} \ln(RND)
$$
  
  Además, recordando que $\lambda = \frac{1}{Media}$, la fórmula también puede expresarse como: $x = -Media \cdot \ln(RND)$.

### **Caso Complejo 1: Funciones de densidad por partes**

Este es un error común que el docente enfatizó repetidas veces en clase.  
**Ejercicio:**  
$f_1(x) = \frac{\sqrt{x}}{16}$ para $x$ entre $0$ y $1$  
$f_2(x) = \frac{1}{6}$ para $x$ entre $1$ y $6$  
Cuando se tienen dos tramos, hay que crear **dos generadores** ($x_1$ y $x_2$), pero el cálculo del segundo depende crucialmente del área del primero.  
**Para el primer tramo (**$x_1$**):**

1. Integral de $f_1(x)$ entre 0 y $x$:  
   
$$
F_1(x) = \int_{0}^{x} \frac{x^{1/2}}{4} \\, dx = \frac{1}{4} \cdot \frac{x^{3/2}}{3/2} = \frac{x^{3/2}}{6}
$$
  
2. Igualando a RND y despejando:  
   
$$
RND = \frac{x^{3/2}}{6} \implies x_1 = (RND \cdot 6)^{2/3}
$$

**CÁLCULO DEL VALOR DE CORTE (¡CRÍTICO\!):**  
Antes de hacer el tramo 2, necesitamos saber el "valor de corte", es decir, cuánta área (probabilidad acumulada) ocupó el tramo 1\. Para esto, tomamos la $F_1(x)$ (antes de igualar a RND) y **la evaluamos en el límite superior de su intervalo (en** $x=1$**)**:

$$
F_1(1) = \frac{1^{3/2}}{6} = \frac{1}{6}
$$
  
Este $1/6$ es el valor de corte. Si generamos un RND $< 1/6$, usamos la fórmula $x_1$. Si RND $\ge 1/6$, usamos la fórmula $x_2$.  
**Para el segundo tramo (**$x_2$**):**  
El docente remarcó un error que cometió en vivo para enseñar la lección: **Al plantear la integral del tramo 2, HAY QUE SUMARLE EL ÁREA ACUMULADA DEL TRAMO 1 (el valor de corte).**

$$
F_2(x) = \frac{1}{6} + \int_{1}^{x} \frac{1}{6} \\, dx
$$
  
Integrando:

$$
F_2(x) = \frac{1}{6} + \left[ \frac{1}{6}x \right]_1^x = \frac{1}{6} + \left( \frac{1}{6}x - \frac{1}{6} \right) = \frac{1}{6}x
$$
  
Igualando a RND y despejando:

$$
RND = \frac{1}{6}x \implies x_2 = RND \cdot 6
$$

### **Caso Complejo 2: Obtener la f(x) a partir de un gráfico**

**Ejercicio:** Generar variables a partir de un gráfico de probabilidad que muestra una línea recta ascendente que arranca en $x=170$ con probabilidad $0$, y termina en $x=210$ con probabilidad $1/20$.  
Aquí el paso 1 no está resuelto. No tenemos $f(x)$, tenemos un gráfico con dos puntos coordenados:  
Punto 1: $(170, 0)$  
Punto 2: $(210, \frac{1}{20})$  
**Cómo deducir la función (Ecuación de la recta** $y = mx + b$**):**

1. **Calcular la pendiente (**$m$**):**  
   
$$
m = \frac{y_2 - y_1}{x_2 - x_1} = \frac{\frac{1}{20} - 0}{210 - 170} = \frac{1/20}{40} = \frac{1}{800}
$$
  
2. **Calcular la ordenada al origen (**$b$**):**  
   Tomamos cualquier punto, por ejemplo $(170, 0)$, y despejamos $b$:  
   
$$
y = mx + b \implies 0 = \frac{1}{800}(170) + b \implies b = -\frac{170}{800}
$$
  
3. **Armar la función de densidad:**  
   
$$
f(x) = \frac{1}{800}x - \frac{170}{800} = \frac{x - 170}{800}
$$
  
   A partir de aquí, se aplica el método normalmente: se integra entre $170$ y $x$, y el resultado se iguala a RND para despejar $x$.

## **Ejemplos y casos mencionados**

* **Temperatura de una estufa:** Caso de Distribución Uniforme entre 80 y 95 grados. Explicó que ingresando esos valores como $A$ y $B$ en la fórmula transformada, transformamos la distribución $U(0,1)$ en una que siempre arrojará valores entre 80 y 95\. El 95 nunca sale de forma exacta porque el generador nunca arroja 1 puro.  
* **Gráfico ascendente de probabilidad (170 a 210):** Se usó para mostrar cómo afecta la probabilidad visual. Al estar la curva ascendiendo hacia el 210, el docente hizo razonar que nuestro generador tirará muchos más números cercanos a 210 que a 170\. Si hiciéramos un histograma de los números generados, se vería una escalera ascendente.

## **Puntos que el docente remarcó**

* **¡El valor de corte en funciones por partes va sumado a la siguiente integral\!** Fue el punto de mayor fricción geométrica y analítica de la clase. Hay que sumar la superficie de la integral anterior antes de integrar el nuevo tramo.  
* **¿A quién le corresponde el "Valor de Corte"?** Si el número aleatorio generado es **exactamente igual** al valor de corte, se debe utilizar el generador de la función *siguiente* (Ej: si corte es $0.5$ y RND \= $0.5$, se usa el generador $x_2$, porque el primero suele incluir hasta el límite sin tocarlo estricto matemáticamente).  
* **Simplificación Exponencial:** Es matemáticamente correcto en la práctica usar RND en lugar de 1 \- RND al despejar la función exponencial inversa.  
* **Error en el PDF provisto:** El documento original de la cátedra tiene intercambiados los subíndices de los generadores ($x_1$ y $x_2$) en la tabla de resolución del ejercicio de dos tramos. Todo lo que dice $x_1$ debería decir $x_2$ en la resolución de la serie y viceversa.

## **Para el trabajo práctico / evaluación**

* **Precisión de los aleatorios en TPs y Ejercicios:** El enunciado o el docente siempre definirá con cuántos decimales de precisión se trabaja (generalmente 2 para clase por simplicidad temporal, y más decimales en TPs).  

## **Dudas y cosas para revisar por el alumno (Tareas)**

* **Ejercicio 3 del PDF:** Función simétrica ascendente y descendente dividida en $x=18$ (tramos $14$ a $18$ y $18$ a $22$). El estudiante debe resolverlo aplicando la lógica de cálculo de corte vista en el Ejemplo Complejo 1\. El valor de corte deducido en clase mentalmente fue $1/2$.  
* **Completar la integral del Ejercicio 4:** Se obtuvo la ecuación de la recta ($f(x) = \frac{x - 170}{800}$). Falta integrar entre $170$ y $x$, igualar a RND y despejar para obtener la ecuación del generador final.