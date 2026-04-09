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

- Para la primera restriccion ($4 M_1 + 8 M_2 \leq\ 480$) nos quedan [120, 0] y [0, 60]
- Para la segunda restriccion ($5\ M_1\ +\ 6\ M_2 \leq\ 600$) nos quedan [120, 0] y []