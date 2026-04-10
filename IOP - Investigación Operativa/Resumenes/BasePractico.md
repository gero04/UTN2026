# Practico IOP

## Planteo del problema

En un primer momento, vamos a tener que desarrollar un modelo matematico que represente el problema enunciado. Para modelizar un problema debemos identificar el objetivo, definir las variables y enunciar las restricciones. Por ejemplo:

- Objetivo: Maximizar la contribucion total a las utilidades semanales de la produccion y venta de los motores M1 y M2

> [Tip]
> Para definir un objetivo, debemos tener en cuenta que buscamos maximizar o minimizar algo en un periodo de tiempo haciendo un proceso

- Variables:

  - $M_1$ : Unidades del motor tipo M1 a producir y vender semanalmente

  - $M_2$ : Unidades del motor tipo M2 a producir y vender semanalmente

> [Tip]
> Definimos una variable como "Unidad de medida/Unidad" + Verbo + Franja de tiempo

- Restricciones:

  - La cantidad de horas de proceso de maquinado a utilizar semanalmente no debe superar las 480
  - La cantidad de horas de proceso de armado a utilizar semanalmente no debe superar las 600
  - La cantidad de horas de proceso de montaje a utilizar semanalmente no debe superar las 540

En base a esto el modelo nos queda de la siguiente manera:

$$ MAX(Z) = 100 * M_1 + 120 * M_2 $$
$$ s.a. $$
$$4\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 480\ [Horas]$$
$$5\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 6\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 600\ [Horas]$$
$$12\ \frac{[Horas]}{[Unidad]}\ M_1\ [Unidad]\ +\ 8\ \frac{[Horas]}{[Unidad]}\ M_2\ [Unidad]\ \leq\ 540\ [Horas]$$
$$M_1,\ M_2\ \geq\ 0$$

> [Tip]
> La ultima restriccion se conoce como Restriccion de no negatividad y VA SIEMPRE

Ahora vamos a plantear dos maneras de resolver el problema: el metodo grafico y el metodo simplex

## Metodo Grafico

> [OJOTA]
> Este metodo solo se usa con dos variables de decision por ende te limita muchisimo, pero bueno que se le va a hacer

Vamos a graficar todas las restricciones, para esto lo mas facil es plantear a una variable como $x$ y a la otra como $y$, y luego hacerlas valer 0 alternativamente, esto nos va a dar dos conjuntos de puntos: [x, 0] ó [x1, 0] e [0, y] ó [0, x2]. Es decir

- Para la primera restriccion ($4 M_1 + 8 M_2 \leq\ 480$) nos quedan $[120, 0]$ y $[0, 60]$
- Para la segunda restriccion ($5\ M_1\ +\ 6\ M_2 \leq\ 600$) nos quedan $[120, 0]$ y $[0, 100]$
- Para la tercera restriccion ($12\ M_1\ +\ 8\ M_2\ \leq\ 540$) nos quedan $[45, 0]$ y $[0, 67.5]$

> [TIP]
> El calculo de una recta dada por dos puntos se realiza calculando primero la pendiente $m = \frac{y_2 - y_1}{x_2 - x_1}$ y luego la ecuacion punto pendiente $y - y_1 = m * (x - x_1)$. Con estas dos terminamos despejando para obtener la forma $y = m*x + b$ 

Con estos puntos podemos trazar rectas que representan las restricciones, y teniendo en cuenta que vamos a trabajar tambien con la restriccion de no nulidad (lo cual nos ubica el campo de trabajo en el primer cuadrante), graficamente tenemos lo siguiente

![[Pasted image 20260410101959.png]]

Aca nos encontramos con la *region factible*, que es el conjunto de puntos que es solucion a todas las inecuaciones del sistema de restricciones del PL. En este caso, es el poligono formado por los puntos A, B, C y D. Estos puntos van a conformar los posibles puntos optimos de nuestra funcion, entonces evaluamos la funcion en ellos y la que de un Z mas grande es el punto optimo

- Para $A= [0, 0]$: $\longrightarrow Z = 100 * 0 + 120 * 0 \longrightarrow Z = 0$ 
- Para $B = [50, 0] : \longrightarrow Z = 100 * 50 + 120 * 0 \longrightarrow Z = 5000$
- Para $C = [15, 53] : \longrightarrow Z = 100 * 15 + 120 * 53 \longrightarrow Z = 7860$
- Para $D = [0, 60] : \longrightarrow Z = 100 * 0 + 120 * 60 \longrightarrow Z = 7200$
Entonces comprobamos que el punto optimo de Z es $C = [15, 53]$ 
  