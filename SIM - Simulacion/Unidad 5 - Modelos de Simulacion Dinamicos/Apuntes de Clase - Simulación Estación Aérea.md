# **Modelado y Simulación: Análisis del Ejercicio de la Estación Aérea y Pautas del Parcial**

**Materia:** Modelado y Simulación de Sistemas  
**Resumen en una oración:** La clase se centró en repasar la gestión de eventos consecutivos (ejercicio del ascensor), modelar paso a paso un sistema de colas con prioridades (ejercicio del aeropuerto) definiendo objetos, estados y eventos, y finalmente se detalló la modalidad práctica del próximo examen parcial.

## **Conceptos clave**

* **Generación de tiempos para eventos simultáneos/múltiples:** Cuando múltiples entidades realizan una misma acción consecutivamente (ej. 3 personas bajando de un ascensor), **NO se debe** generar un solo tiempo aleatorio y multiplicarlo por 3, ya que eso asumiría que todas tardan exactamente lo mismo (rompiendo la aleatoriedad). Se deben generar tres tiempos independientes y sumarlos.  
* **Agrupación de eventos (Evento Único vs. Múltiples):** Se puede agrupar la salida de varias entidades en un solo evento ("Fin de salida general") **únicamente si se tiene la certeza absoluta (100%)** de que ese proceso no va a ser interrumpido por ningún otro evento del sistema (ej. un corte de luz, falla de puertas). Si hay riesgo de interrupción, los eventos deben programarse de a uno.  
* **Entidades efímeras (Entidades que rebotan):** Si una entidad llega al sistema pero es rechazada inmediatamente por falta de capacidad (ej. un avión derivado porque la estación está llena), **no se le asigna un estado**. Simplemente se la cuenta (si el problema lo pide) y se elimina el objeto del sistema. Crear un estado "Derivado" es un error conceptual porque llenaría la simulación de objetos inactivos que nunca saldrán de ese estado.  
* **Continuidad de ocupación del servidor:** Si un servidor (ej. la pista) termina de atender a una entidad y hay otra entidad en la cola esperando, el servidor **nunca pasa al estado "Libre"**. Permanece "Ocupado", pasando inmediatamente a atender a la siguiente entidad.

## **Desarrollo de la clase**

### **1\. Repaso inicial: Ejercicio del Ascensor**

El profesor comenzó revisando un ejercicio anterior sobre un ascensor en el piso 15 donde bajaban y subían personas. La duda principal era cómo modelar la salida de, por ejemplo, 3 personas que bajan juntas.  
Se plantearon dos formas:

1. Generar un evento "Fin de salida" por cada pasajero de forma secuencial.  
2. Generar un único evento "Fin de salida" que englobe a los 3 pasajeros, sumando sus tiempos de salida.  
   El profesor explicó que la opción 2 es válida y optimiza la simulación, pero solo si estamos seguros de que nada interrumpirá ese proceso (como que se cierren las puertas por un desperfecto). Además, recalcó que los tiempos se suman, nunca se genera un random y se multiplica por la cantidad de personas, ya que cada persona tiene un comportamiento aleatorio diferente.

### **2\. Análisis del Problema 26: La Estación Aérea**

Se leyó el enunciado del problema donde aviones llegan (exponencial, media 10 min), aterrizan si la pista está libre (uniforme 3 a 5 min), permanecen estacionados (normal, media 80 min, desvío 30 min) y luego despegan (uniforme 2 a 4 min). Hay prioridad para aterrizar sobre despegar, y una capacidad máxima de 30 lugares en la estación.

### **3\. Definición de Objetos y Estados**

Se realizó un debate exhaustivo para definir qué elementos deben rastrearse en la simulación:  
**Objeto: Aeronave (Avión)**

* *En vuelo (o Esperando aterrizaje):* El avión llegó al sistema, pero la pista está ocupada.  
* *Aterrizando:* Usando la pista para llegar.  
* *Estacionado (o En tierra):* Terminó de aterrizar y está pasando su tiempo de permanencia. No requiere pista ni atención.  
* *Esperando despegue:* Terminó su tiempo de permanencia, quiere irse, pero la pista está ocupada.  
* *Despegando:* Usando la pista para irse.  
  *(Nota: Hubo debate sobre si unificar "Aterrizando" y "Despegando" en un solo estado "Usando pista". El docente indicó que ambas formas son válidas siempre que se asigne el tiempo correcto, pero separarlos suele dar más claridad al programar).*

**Objeto: Pista**

* *Libre* / *Ocupada*.

**Objeto: Estación Aérea**

* *Con espacio* / *Llena* (Capacidad máxima: 30 unidades). El docente hizo una analogía con el estacionamiento de un shopping: no importan los lugares específicos, sino si hay capacidad global o no.

### **4\. Definición de Eventos**

Los eventos son los instantes donde cambia el estado del sistema. El profesor remarcó que las "solicitudes" (de aterrizaje o despegue) no son eventos por sí mismos, sino acciones que ocurren *dentro* de otros eventos.  
Los eventos definidos fueron:

1. **Llegada de aeronave:** Aquí se genera la próxima llegada y se evalúa si el avión entra a la pista, va a la cola de aterrizaje, o es derivado (si hay 30 aviones en el sistema).  
2. **Fin de aterrizaje:** Libera la pista temporalmente. Revisa la cola de prioridad (primero los que quieren aterrizar, luego los que quieren despegar). Genera el "Fin de permanencia" para el avión que acaba de llegar.  
3. **Fin de despegue:** Libera la pista. Revisa nuevamente las colas (prioridad a aterrizajes). El avión desaparece del sistema.  
4. **Fin de permanencia:** El avión termina su estadía. Si la pista está libre, empieza a despegar (se genera el Fin de despegue). Si está ocupada, pasa a la cola de "Esperando despegue".

### **5\. Manejo de Colas y Contadores**

* **Cola de aterrizaje:** Aviones en vuelo esperando.  
* **Cola de despegue:** Aviones en tierra esperando irse. El docente sugirió manejar colas separadas por prioridad es más fácil que una sola cola compleja.  
* **Contador de lugares ocupados:** Fundamental. Debe contemplar los aviones estacionados, los que esperan despegue, ¡y también los que están en la cola de aterrizaje\! Porque el que está en vuelo ya tiene garantizado su lugar abajo.  
* **Acumuladores:** Se necesitarán para sumar tiempos de espera en vuelo y en tierra para los promedios solicitados en el enunciado.  
* **Vectores individuales:** Como cada avión estacionado tiene su propio tiempo de "Fin de permanencia", el vector estado debe tener múltiples columnas (hasta 30, idealmente) para rastrear cuándo se quiere ir cada avión específico.

### **6\. Simulación paso a paso (Inicio)**

El docente modeló las primeras filas del vector estado basándose en las condiciones iniciales:

* *Minuto 0:* Próxima llegada al min 12\. Pista libre. 3 aviones estacionados con fin de permanencia en min 15, 17 y 20\. Lugares ocupados: 3\.  
* *Minuto 12 (Llegada):* Se genera la próxima llegada. Como la pista está libre, el avión ocupa la pista (empieza a aterrizar). Se genera el fin de aterrizaje. Lugares ocupados: 4\.  
* *Minuto 15 (Fin permanencia):* El avión que se quería ir despierta. Pero la pista está ocupada (aterrizando el del min 12). Pasa a la "Cola de despegue". Se inicia su tiempo de espera en tierra.

## **Ejemplos y casos mencionados**

* **Personas en el ascensor:** Usado para explicar por qué no se debe multiplicar un único número aleatorio por la cantidad de personas (rompe la variabilidad estadística).  
* **Bomba / Corte de luz en el ascensor:** Ejemplo extremo para ilustrar qué significa un "evento que interrumpe" un proceso continuo, lo que obliga a modelar las salidas de a una en lugar de en bloque.  
* **Estacionamiento del shopping:** Analogía para el estado de la estación aérea ("Llena" o "Con espacio"). No interesa qué lugar exacto ocupa el avión, solo si la capacidad de 30 fue alcanzada.  
* **Cola médica de urgencias:** Usada para explicar el manejo de prioridades. Los aviones en vuelo (aterrizaje) son como las urgencias médicas; tienen prioridad sobre los pacientes generales (aviones despegando). Se recomendó usar colas físicas separadas para simplificar la lógica.

## **Puntos que el docente remarcó reiteradas veces**

* **NO multiplicar randoms:** Si 3 entidades hacen lo mismo, se generan 3 randoms distintos y se calculan 3 tiempos distintos, luego se suman.  
* **Eliminación de entidades:** Si un avión es derivado porque la estación está llena, desaparece. **No se crea un estado ni un evento para él.**  
* **La pista nunca queda libre si hay cola:** Al ocurrir un evento de "Fin de...", si hay alguien esperando (ya sea para aterrizar o despegar), la pista sigue en estado "Ocupada" automáticamente.  
* **Atención al límite de capacidad (30):** Al evaluar si se acepta a un nuevo avión, el contador debe sumar a los aviones estacionados, a los que esperan despegar, Y a los que están en la cola de aterrizaje esperando tocar tierra.

## **Para el trabajo práctico / evaluación (Parcial)**

* **Fecha de cierre/Parcial:** Mencionado para el viernes 29 de mayo (aproximadamente, revisar calendario oficial).  
* **Modalidad de examen:** Se rendirá en Moodle y requerirá el uso de LibreOffice Calc (no Excel, aunque la lógica es la misma).  
* **Formato del vector:** Los docentes entregarán el archivo con la cabecera (columnas) y la primera fila ya armadas, incluyendo la condición inicial.  
* **Mecánica de resolución:** No se hará el ejercicio desde cero. Se pedirá simular, por ejemplo, de la fila 2 a la 5\. Luego habrá preguntas en Moodle del estilo *"¿Qué valor tiene el acumulador de esperas en el evento N?"*.  
* **Números Aleatorios a demanda:** No se entregará una tabla genérica de números aleatorios. En el mismo archivo provisto, debajo de la columna donde se necesite un random, aparecerá la lista específica de randoms a utilizar para esa columna/cálculo.  
* **Hojas de fórmulas:** El docente confirmó explícitamente: **"Sí, llevá la fórmula"**. Los estudiantes pueden llevar anotadas las fórmulas de las distribuciones (Exponencial, Normal, Uniforme) ya que el examen requerirá hacer el cálculo manual/en planilla insertando el random dado.

## **Dudas y cosas para revisar por tu cuenta**

* **Contador complejo:** Quedó planteado pero sin resolver numéricamente a fondo cómo rastrear el punto que pide: *"porcentaje de aeronaves que aterrizan y parten ni bien lo solicitan"*. Esto implica crear contadores separados para llegadas totales y para "llegadas con pista libre \+ salidas con pista libre", lo cual requerirá mucha atención en las condiciones IF de la planilla.  
* **Tiempos de espera:** Revisar bien cómo acumular el tiempo de inicio de espera vs. la hora de fin de espera para calcular promedios. (Hora actual del evento menos la Hora en que entró a la cola).