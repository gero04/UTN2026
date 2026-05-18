# **Ejercicios Prácticos de Simulación: Monte Carlo General y Modelos de Inventario**

**Materia:** Simulación
**Resumen en una oración:** La clase se enfocó en la resolución práctica de ejercicios de simulación por Monte Carlo con eventos dependientes (juego de guerra) y la optimización de simulaciones de inventario y transporte mediante árboles de probabilidad y manejo eficiente de la memoria (acumuladores).

## **Conceptos clave**

* **Simulación de Inventario vs. Simulación General (Monte Carlo):** Los problemas de inventario suelen resolverse mediante una "plantilla" de columnas que casi siempre es la misma (stock inicial, demanda, pedido, etc.). En cambio, los problemas generales por Monte Carlo carecen de una fórmula fija; las columnas y la estructura dependen completamente de la narrativa y lógica del problema, cómo se suceden los eventos y qué variables se pide rastrear.  
* **Experimentos Independientes vs. Dependientes:** En simulaciones puras, cada fila (experimento) no tiene relación con la anterior. Sin embargo, en ejercicios complejos, ciertas variables de "estado" se arrastran de un experimento a otro (por ejemplo, el nivel de combustible de un tanque que sobrevive o la posición de un elemento).  
* **Consumo de Números Aleatorios (Randoms):** Regla inquebrantable de la simulación: un número aleatorio de una serie predefinida solo se consume/gasta cuando *efectivamente ocurre y se necesita simular* el evento asociado. No se puede "saltar" un número si una condición previa impidió que llegáramos a ese cálculo.  
* **Contadores vs. Acumuladores:** \* *Contador:* Incrementa su valor de a 1 (ej. cantidad de unidades destruidas o días de lluvia).  
  * *Acumulador:* Suma magnitudes variables fila a fila (ej. litros de combustible gastados o costo total en pesos).  
* **Inmediatez Superior (Regla de optimización en memoria):** Principio de diseño para algoritmos de simulación. Consiste en mantener en memoria únicamente la "fila actual" y la "fila anterior". Cualquier totalización (ej. gasto total) debe hacerse llevando una columna acumuladora fila a fila. Nunca se debe salir a leer toda una columna hacia atrás al finalizar la simulación, ya que esto saturaría el hardware en simulaciones de millones de registros.  
* **Eventos mutuamente excluyentes y simultáneos (Árboles de Probabilidad):** Al simular demoras secuenciales, la probabilidad de que ocurran dos eventos sucesivos se calcula multiplicando sus probabilidades (Regla del Y \= Producto). Las alternativas para un mismo resultado se suman (Regla del O \= Suma). Esto permite consolidar varios eventos aleatorios en una única tabla de probabilidad y ahorrar números aleatorios.

## **Desarrollo de la clase**

### **1\. Resolución del Ejercicio: Simulación de Juego de Guerra (PDF 7, Ejercicio 4\)**

La primera mitad de la clase analizó un problema de enfrentamiento bélico entre tanques A y B, donde se debían rastrear condiciones específicas de estado.

* **Contexto:** Los tanques del bando A salen de uno en uno a buscar a los del bando B.  
* **Reglas de combustible:** \* A gasta 20% de combustible para ir hasta la zona B y 20% para volver a su base.  
  * B tiene autonomía infinita y no gasta en desplazarse.  
* **Enfrentamiento:** Al encontrarse, se simula el combate. Hay 80% de chances de que B sea destruido y 20% de que A sea destruido. Si el tanque A resulta victorioso, gasta combustible extra de acuerdo a una tabla de probabilidades (20%, 30%, 40% o 50% de gasto).  
* **Condición de retorno:** Si luego de ganar, A queda con 30% de combustible o menos, se retira a la base. Si queda con más, permanece en la zona para el siguiente experimento (ahorrando el 20% de viaje en la siguiente fila). Si A queda inmovilizado sin nafta para volver, es destruido. Cada vez que A es destruido o vuelve, sale un nuevo tanque A con 100% de nafta en la fila siguiente.

#### **Diseño de la Tabla de Simulación**

El profesor estructuró la simulación de la siguiente manera:

1. **Fila 0 (Inicialización):** Optativa. Sirve para setear el nivel inicial del tanque (100%).  
2. **Combustible inicial de A:** Toma el valor del tanque al iniciar el experimento (puede ser 100% si es nuevo, o lo que le sobró si se quedó en la zona de combate).  
3. **Desplazamiento:** Se anota si gasta "20" (viaja) o "0" (si ya estaba en la zona).  
4. **Random de enfrentamiento:** Determina si gana A o gana B.  
5. **Resultado de enfrentamiento:** Se anota "B destruido" o "A destruido". *Importante:* El orden de las probabilidades no altera el resultado final en simulaciones muy largas, siempre que se respete el ancho del espectro (ej. 80% del espectro para B y 20% para A).  
6. **Random de Consumo:** *Nota crucial:* Solo debería sacarse si A no fue destruido, pero debido a que el inciso B pedía calcular el *consumo promedio total por combate*, se decidió calcular el consumo de A incluso en los casos donde luego resultara destruido.  
7. **Consumo de Combate:** Valor obtenido según la tabla de probabilidad asociada al gasto.  
8. **Nivel final de combustible:** El saldo de nafta.  
9. **Retorna a la base:** Se anota "20" (si el saldo es \<=30% y le alcanza para volver) o "0".  
10. **Consumo Total:** Sumatoria del Desplazamiento \+ Consumo de Combate \+ Retorno a Base.  
11. **Contadores:** Columnas separadas para "Tanques A destruidos" y "Tanques B destruidos".  
12. **Acumulador de consumo de combustible:** Columna crítica para ir sumando fila a fila el "Consumo Total" de todos los combates, a fin de dividirlo al final por el N de experimentos (10) y obtener el promedio sin recorrer la columna hacia atrás.

### **2\. Dudas sobre la unidad de tiempo (Ejercicio de inventarios)**

Un alumno consultó cómo gestionar los inventarios si las ventas ocurren al inicio de la semana y el pedido llega a la mitad.  
**Explicación del profesor:** Si la simulación está planteada en *semanas* o *días*, se asume que **todo ocurre de forma simultánea al final de esa unidad de tiempo**. No se discrimina qué pasa dentro del día/semana. Si un problema del mundo real exige distinguir entre mañana o tarde (ej. los camiones llegan a la tarde, las ventas son a la mañana), el modelo está mal planteado y hay que "bajar la granularidad" (cambiar la unidad de tiempo a horas).

### **3\. Tratamiento de Frecuencias Históricas (PDF 8, Ejercicio "Moreno Insumos")**

El problema entregaba datos de demanda como frecuencia bruta: en una muestra de 14 días (del 1 al 14 de marzo), se vendió 1 unidad (2 ocasiones), 2 unidades (3 ocasiones), 3 unidades (3 ocasiones), etc.

* **Procedimiento:** Para pasar esto a una tabla utilizable en simulación, se suma el total de frecuencias (muestra total \= 10 días útiles de venta reportados) y se divide la frecuencia individual sobre el total para obtener la *Probabilidad simple*. Luego se genera la *Probabilidad Acumulada* y finalmente se asignan los rangos para los randoms (0.00 a 0.99).  
* **Importancia del tamaño muestral:** El profesor recalcó que armar esta tabla tomando la demanda de solo dos semanas o un mes es peligroso en la vida real debido a la estacionalidad (ej. no usar datos de enero para inferir la venta de abrigos). A mayor volumen de facturación histórica usada (ej. 6 meses), más precisa la simulación.

### **4\. Simulación de Demoras Compuestas y Árboles de Probabilidad**

En el tramo Buenos Aires \-\> Rosario \-\> Córdoba, existen demoras base (1 día por tramo, 1 día en depósito). Pero hay probabilidades de retrasos adicionales:

* Buenos Aires \- Rosario: 15% de probabilidad de demorar 1 día extra. (Por tanto, 85% de que no haya demora).  
* Rosario \- Córdoba: 30% de probabilidad de demorar 1 día extra. (Por tanto, 70% de que no haya demora).

**El abordaje ineficiente:** Usar un número aleatorio para ver qué pasa en el Tramo 1, y luego sacar otro número aleatorio para ver qué pasa en el Tramo 2\.  
**El abordaje óptimo:** Armar un árbol de probabilidades para calcular los caminos posibles y simular toda la demora total del viaje con *un solo* número aleatorio.

* **Camino Feliz (3 días en total):** No hay demoras extras. Probabilidad: 0.85 \* 0.70 \= 0.595 (59.5%)  
* **Camino Demora 1 (4 días en total):** Demora solo en el primer tramo. Probabilidad: 0.15 \* 0.70 \= 0.105 (10.5%)  
* **Camino Demora 2 (4 días en total):** Demora solo en el segundo tramo. Probabilidad: 0.85 \* 0.30 \= 0.255 (25.5%)  
* **Camino Desastre (5 días en total):** Demoras extras en ambos tramos. Probabilidad: 0.15 \* 0.30 \= 0.045 (4.5%)  
  *(Nota: la sumatoria de estas probabilidades da exactamente 1).* De esta forma, se arma una tabla agrupando los escenarios de 4 días (10.5% \+ 25.5% \= 36% de prob.), usando la mitad de procesamiento computacional.

## **Ejemplos y casos mencionados**

* **Depredador y la Presa (Ejercicio Previo):** Usado para explicar qué hacer con los randoms durante un empate en combate. Si hay empate, la presa no se escapa pero tampoco se la caza. Si se tenía preparado un random para ver si la cazaba, *no se debe utilizar ni descartar*; se guarda estrictamente para el próximo momento de la simulación en que realmente haya una cacería ganada.  
* **Venta de Abrigos en Enero:** Analogía para explicar los sesgos por estacionalidad al tomar muestras muy cortas de demanda.  
* **El tren Buenos Aires \- Rosario \- Córdoba:** Caso de ruteo para enseñar el concepto estadístico de multiplicación de probabilidades en eventos independientes para consolidar un simulador de demoras logísticas.

## **Puntos que el docente remarcó explícitamente**

* **Estricto consumo de Randoms:** *Reiterado enfáticamente*. Si un número se extrae (mentalmente) pero no se usa porque la condición no se cumplió, el número se guarda para la próxima. "Saltar un número aleatorio de una serie porque 'no correspondía aplicarlo' está mal".  
* **Estabilidad de Promedios en fila:** Calcular promedios en cada fila demanda más procesamiento, pero en simulaciones reales es útil. Se pone un "listener" (escuchador); si durante 100 o 1000 filas el promedio no cambia sustancialmente, la simulación se estabilizó y se puede cortar la ejecución para no gastar cómputo innecesariamente.  
* **Diseño con inmediatez superior:** Si van a programar una simulación (TPs 3, 4 y 5), diseñen variables acumuladoras. Un script que intenta guardar toda una tabla de millones de registros para sumar al final causará "Out of Memory".  
* **Ajuste manual de decimales:** Cuando una probabilidad calculada (ej. 0.595) excede la cantidad de decimales de la tabla de randoms impresa que se lleva al examen (usualmente 2 decimales, del 00 al 99), es válido redistribuir centésimas entre las opciones para redondear artificialmente a dos decimales y que sumen 1.00. (A nivel software, la solución correcta es simplemente pedirle al generador que trabaje con 3 decimales).

## **Para el trabajo práctico / evaluación**

* **Sobre el parcial:** El ejercicio del "Juego de Guerra 2" se considera de una dificultad mayor/más rebuscada que lo que suele tomarse en los parciales. En el parcial entrará un ejercicio Genérico de Monte Carlo u otro de Inventario puro y duro.  
* **Ambigüedades en parciales:** Toda duda interpretativa del enunciado se debe consultar en voz alta levantando la mano en el examen (Ej: ¿Tomo en cuenta o no lo que sobra de nafta en tal caso?). El profesor tomará un criterio y lo dictará para todo el curso para unificar la corrección. Las tablas y el orden de los datos en el examen vienen cerradas (prearmadas) para asegurar que a todos les dé exactamente el mismo número final.  
* **Tener en cuenta para los Trabajos Prácticos Programados (TP 3, 4 y 5):** Aplicar estrictamente el concepto de usar Acumuladores fila por fila para no saturar la memoria del lenguaje de programación utilizado.

## **Dudas y cosas para revisar**

* **Consumo y retorno en el Juego de Guerra:** Hubo un fuerte debate sobre qué pasaba matemáticamente con el tanque que intentaba volver con menos de 20% de combustible y era destruido (ej. si le quedaban 10%). El consenso final fue que *se consume todo lo que le queda* en el intento, quedando el nivel final en cero, pero que el texto era ligeramente ambiguo en cómo se lo cobraba estadísticamente.  
* **Demoras Asimétricas / Condicionadas:** Al final de la clase se introdujo rápidamente el problema de "Maquinaria Agrícola", el cual plantea una dificultad mayor: Si se demora el primer tramo, la probabilidad del segundo tramo *cambia* (ej. baja al 15%). Aquí ya no se pueden unificar probabilidades tan directamente sin contemplar las probabilidades condicionales asimétricas. Se recomienda revisar cómo estructurar ese árbol de probabilidad.