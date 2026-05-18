# **Simulación de Sistemas Discretos y Teoría de Colas**

**Materia:** Simulación
**Resumen en una oración:** La clase introdujo el modelado de sistemas discretos mediante diagramas de eventos y vectores de estado, explicando cómo gestionar llegadas, colas y atenciones, y culminó con una breve introducción a la resolución analítica (Teoría de Colas).

## **Conceptos clave**

* **Sistemas Discretos:** Sistemas dinámicos que evolucionan a lo largo del tiempo, pero donde los cambios ocurren únicamente en instantes específicos marcados por "eventos". Entre un evento y el siguiente (ej. entre $T_1$ y $T_2$), el sistema permanece estático y medirlo arrojaría los mismos resultados.  
* **Objetos del Sistema:** Son las entidades que interactúan.  
  * *Temporales:* Entran y salen del sistema (típicamente los clientes).  
  * *Permanentes:* Están desde el inicio hasta el final de la simulación (típicamente los servidores). Tienen capacidad finita.  
* **Eventos:** Sucesos que alteran el estado del sistema y nos indican cuándo hacer las mediciones.  
* **Colas:** Líneas de espera que se forman cuando la capacidad del servidor está colmada porque los clientes llegan más rápido de lo que pueden ser atendidos.  
* **Estados:** Es un atributo fundamental que poseen tanto clientes como servidores que determina su situación actual (ej. servidor "libre" u "ocupado", cliente "en cola" o "siendo atendido"). Toman valores limitados.  
* **Atributos:** Características específicas de un objeto que pueden variar (ej. cantidad de artículos que compra un cliente, hora de llegada a la cola).  
* **Medidas de Desempeño:** Valores estadísticos de interés que resultan de la simulación y sirven para evaluar cómo funciona el sistema (ej. tiempo promedio en cola, porcentaje de ocupación).  
* **Vector de Estado:** Estructura tabular que permite trazar la evolución del sistema paso a paso (evento a evento), registrando el reloj, variables aleatorias, estado de servidores, colas y acumuladores.

## **Desarrollo de la clase**

### **1\. Identificación de Eventos**

En la simulación discreta, no todo lo que pasa es un evento. Los eventos principales a considerar son:

1. **Llegadas:** Un objeto (generalmente un cliente) ingresa al sistema.  
2. **Fin de atención:** El servidor termina de dar el servicio al cliente.  
3. **Eventos Temporizados:** Eventos preestablecidos por un reloj ("es la hora de..."). Ej: fin de la simulación, hora de descanso del cajero.  
4. **Interrupciones:** Cuando el servidor debe cortar la atención por una urgencia o mantenimiento.

*Aclaración fundamental:* **No existen los "inicios de atención" como eventos independientes.** El comienzo de una atención es una *consecuencia* de otro evento (ya sea porque llegó un cliente y el servidor estaba libre, o porque hubo un "fin de atención" y había alguien esperando en la cola).

### **2\. Características y Tipos de Colas**

Al modelar un sistema, hay que definir cómo se comportan las colas:

* **Longitud máxima:** Si la cola tiene un límite físico. Si está colmada, el cliente que llega no ingresa al sistema y se va.  
* **Disciplina de salida:** Orden en que son atendidos (generalmente FIFO \- First In, First Out).  
* **Impaciencia:** Define si el cliente está dispuesto a esperar tiempo infinito o no. Algunos clientes esperan un tiempo determinado (ej. 2 minutos) y si no son atendidos, abandonan la cola.  
* **Prioridades:** Algunos clientes pueden requerir servicios distintos o tener pase prioritario.

### **3\. Disposición de los Servidores**

* **En serie:** El cliente debe pasar obligatoriamente por el Servidor A y luego por el Servidor B (uno detrás de otro).  
* **En paralelo:** Hay varios servidores (A1, A2) y una única cola. El cliente es atendido por el primero que se libere.  
* **Combinaciones y excepciones:** Hay clientes que pueden saltear partes del sistema si no necesitan ese servicio en particular.

### **4\. Lógica de los Eventos (El "Diagrama de Burbujas")**

El profesor hizo mucho hincapié en cómo debe pensar lógicamente el programa al ocurrir un evento. Todo esto ocurre instantáneamente con el reloj principal del sistema "congelado" en ese milisegundo:  
**A. ¿Qué pasa cuando hay una LLEGADA al sistema?**

1. Se determina cuándo va a llegar el *próximo* cliente (se genera un número random, se calcula el tiempo entre llegadas según su distribución y se le suma al reloj actual).  
2. El cliente que acaba de llegar **NO pregunta por la cola**. Pregunta directamente por el servidor.  
3. *Si el servidor está Ocupado:* El cliente no puede ser atendido. Se va a la cola, cambia su estado a "en espera" y se le registra en un atributo la "hora de ingreso a la cola".  
4. *Si el servidor está Libre:* El cliente pasa a estado "siendo atendido". El servidor pasa a estado "ocupado". Como inicia una atención, se debe generar (con un RND) el tiempo que durará esa atención para saber en qué momento del futuro programar el evento "Fin de atención".

**B. ¿Qué pasa cuando hay un FIN DE ATENCIÓN?**

1. El cliente actual abandona el sistema (o esa parte de él).  
2. El servidor **SÍ pregunta por la cola** (pregunta si hay clientes esperando).  
3. *Si hay clientes en cola:* Sale el primero de la cola. Empieza a ser atendido instantáneamente. Se calcula su tiempo en cola (Reloj actual \- su hora de ingreso registrada) y se acumula. Se genera el evento de fin de atención para este nuevo cliente. **El servidor nunca pasa a estado "libre" en este proceso, permanece ocupado.**  
4. *Si NO hay clientes en cola:* El servidor pasa a estar "Libre" y termina el proceso del evento.

### **5\. Medidas de Desempeño y sus Cálculos**

Para evaluar el sistema, al final de la simulación se calculan estos valores:

* **Tiempo promedio de permanencia en cola:** Se suman todos los tiempos que los objetos pasaron en la cola y **se divide por la cantidad TOTAL de clientes que pasaron por el sistema**, no solo por los que hicieron fila. Si alguien no hizo cola, su tiempo es 0, lo cual mejora el promedio.  
* **Cantidad promedio de clientes en cola:** Se calcula sumando el tiempo que la cola tuvo $N$ cantidad de personas. (Ejemplo dado: Si hubo 3 clientes esperando durante 2 minutos, acumulan 6 minutos-cliente. Si luego llega un 4to cliente y están 3 minutos más, acumulan 12 minutos-cliente. Se suma todo eso y se divide por el tiempo total de la simulación).  
* **Porcentaje de ocupación del servidor:** Se registran los momentos en que pasa de "Libre" a "Ocupado" y viceversa. Se acumulan esos tiempos, se divide por el tiempo total de la simulación y se multiplica por 100\.

### **6\. Ejecución del Vector de Estado**

Es una tabla donde cada fila representa el procesamiento de un evento. Columnas principales recomendadas:

* **Evento:** Qué suceso disparó esta fila (Llegada o Fin de Atención).  
* **Reloj:** El tiempo actual de la simulación.  
* **Llegadas:** RND, Tiempo entre llegadas, Próxima Llegada (Hora de reloj).  
* **Cola:** Cantidad actual.  
* **Servidor:** Estado (Libre/Ocupado), RND, Tiempo Atención, Fin de Atención (Hora de reloj).  
* **Atributos y Acumuladores:** Contador de clientes, Hora inicio ocupación, Acumulador de tiempo ocupado, Acumulador tiempo en cola, atributos individuales por cliente para guardar a qué hora llegaron a la cola.

*Mecánica:* Siempre se mira la fila anterior. Se comparan los tiempos de "Próxima Llegada" y "Fin de Atención". El menor de ellos será el "Reloj" de la fila siguiente y dictará qué "Evento" se procesa.

### **7\. Resolución Analítica (Teoría de Colas \- Ley de Little)**

Es un enfoque matemático para sistemas simples que evita hacer la simulación por eventos.

* $\lambda$ (Lambda): Tasa de llegadas (ej. 40 personas por hora).  
* $\mu$ (Mu): Tasa de servicio por servidor (ej. 20 personas por hora).  
* $\rho$ (Ro): Porcentaje de ocupación o factor de utilización. $\rho = \lambda / (s \cdot \mu)$ donde $s$ es la cantidad de servidores. Debe ser menor a 1 para que el sistema sea estable.  
* $W$: Tiempo de permanencia.  
* $L$: Cantidad de clientes.

## **Ejemplos y casos mencionados**

* **Ejemplos generales de sistemas discretos:** Supermercado, pistas de aterrizaje y despegue de un aeropuerto, mostradores de check-in, seguridad de aduanas, plantas fabriles, pacientes llegando a una guardia médica.  
* **Ejemplo de atributos/recorridos:** Un cliente en un supermercado que pasa por panadería, luego góndola 4\. Otro que solo va por vinos y directo a la caja (no hace la cola de la balanza de verduras).  
* **El cliente que llega al supermercado (Comportamiento del sistema):** Al llegar a las cajas, un humano miraría la cola para ver a dónde ir. Pero en programación, el objeto "cliente" debe preguntar si el servidor (cajero) está libre u ocupado. Buscar en una lista de miles de clientes quién está siendo atendido es ineficiente; consultar la variable de estado del servidor es inmediato.  
* **El tiempo de atención del cajero:** El evento "Fin de atención" no solo cuenta pasar los artículos por el escáner. Incluye todo el proceso humano: el saludo ("¿Cómo le va José?"), contar los billetes, pasar la tarjeta. Todo eso debe estimarse dentro de la distribución estadística del tiempo de servicio.  
* **Interrupción telefónica:** Si el cajero/librero debe atender un teléfono, eso es un evento que puede poner al cliente actual en pausa (el cliente queda "siendo atendido" pero se le suma el tiempo de la llamada al fin de atención) o en "espera".  
* **Vector de Estado paso a paso \- La Librería:** Un empleado (servidor permanente), todos los clientes iguales (temporales). Se simuló el ingreso del Cliente 1, cómo cambia el estado del empleado, y cómo el Cliente 2 debe ir a la cola guardando su atributo de tiempo.  
* **Análisis Servidores Rápidos vs. Lentos:** ¿Qué es mejor? ¿3 servidores que demoran 3 segundos por petición, o 1 servidor que demora 1 segundo? La matemática demuestra que aunque el tiempo *en cola* es apenas mayor con el servidor único y rápido, el tiempo de permanencia total en el sistema es **menor**.  
* **Análisis de Costos (Supermercado):** Se analizó un caso donde abrir una caja cuesta $700/h, pero tener a un cliente esperando cuesta $5400/h. Aumentar servidores sube el costo de cajas pero desploma el costo total de espera de clientes.

## **Puntos que el docente remarcó con énfasis**

* **REGLA DE ORO:** **No existen los inicios de atención como eventos.** Son solo la consecuencia de una llegada o de un fin de atención.  
* **REGLA DE PROGRAMACIÓN:** **El cliente NUNCA pregunta por la cola.** Siempre pregunta si el servidor está libre u ocupado.  
* **CONTINUIDAD DEL SERVIDOR:** Cuando un servidor termina de atender a alguien y hay gente en la cola, el servidor **NO pasa por el estado "libre"** ni por un segundo. Pasa directamente a atender al siguiente y sigue "ocupado".  
* **CÁLCULO DE PROMEDIO EN COLA:** Al calcular el promedio de espera en la cola, el divisor es la **totalidad de la población de clientes atendidos**. Los que no esperaron nada suman 0 al acumulador de tiempo, lo que mejora el promedio general.

## **Para el trabajo práctico / evaluación**

### **Sobre el Parcial 1**

* **Fecha:** Sábado 2 por la mañana (hay que anotarse en el selector que publicarán pronto. ¡No demorar\!).  
* **Temas:** Lo visto en esta clase (Teoría de colas y vector de estado) **NO ENTRA** en el primer parcial.  
* **Modalidad Teórico:** Opciones múltiples (Multiple choice). No habrá preguntas a desarrollar porque son 700 alumnos. Es sin material.  
* **Modalidad Práctico:** Se permite llevar material en perfil A o B, y llevar archivos previos de Excel/Planillas. No se permiten pendrives.

### **Sobre el Trabajo Práctico 2 (TP2)**

* **Restricción de software:** A diferencia del parcial, para el TP2 **NO** se pueden llevar archivos previamente confeccionados. Hay que hacerlo todo a mano o usar la planilla en blanco en el momento.  
* **Histogramas (Dato clave):** Cuando armen distribuciones (Normal o Exponencial), **NO agrupen los intervalos de los extremos** (los intervalos chiquitos que suelen dar 2, 0, 1, 1). Déjenlos como están y calculen el estadístico de esa forma, ya que los valores de cálculo están configurados sin agrupar para dar un resultado exacto.

## **Dudas y cosas para revisar**

* **Ley de Little / Teoría Analítica:** El profesor explicó los cálculos con $\lambda$ y $\mu$, pero aclaró explícitamente: *"Esta fórmula de Little no se las vamos a pedir, no las vamos a evaluar"*. Sirve para saber que existe, pero el foco de la materia es hacer la simulación lógica por vector de estado.  
* **Eventos simultáneos:** El profesor mencionó brevemente que si hay eventos que ocurren exactamente en el mismo instante del reloj, por lo general es indistinto el orden de procesamiento, aunque a veces uno depende de la información del otro. Esto convendría repasarlo al programar la simulación.