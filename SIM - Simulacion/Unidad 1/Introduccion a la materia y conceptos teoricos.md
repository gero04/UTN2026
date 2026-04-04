# **Introducción a la Simulación de Sistemas y Modelos Matemáticos**

**Materia:** Simulación (Comisión 4K2)  
**Resumen en una oración:** Introducción a los conceptos fundamentales de simulación, la clasificación de sistemas, las ventajas y peligros de modelar, y las etapas detalladas del proceso de construcción y validación de un modelo de simulación.

## **Conceptos clave**

* **Modelo:** Es una representación de la realidad o de un sistema. No es el sistema en sí, lo que implica que inherentemente posee un grado de inexactitud que dependerá del expertise de quien lo construya. En esta materia se trabajará específicamente con modelos matemáticos.  
* **Simulación:** Es el proceso de construir un programa de computadora que describa el comportamiento de un sistema (o refleje el modelo que lo representa) y hacer evolucionar ese modelo a lo largo del tiempo para experimentar con él. Su objetivo es estimar características, sacar conclusiones y apoyar la toma de decisiones. *Aclaración crucial:* La simulación estima, no da valores exactos; da un valor estadístico entre miles de posibilidades.  
* **Sistemas Estáticos:** Son aquellos modelos discretos donde, ante una entrada al sistema, se genera una salida y sus componentes internos no sufren ningún cambio. Típicamente, ante la misma entrada, la salida será idéntica.  
* **Sistemas Dinámicos:** Modelos discretos donde una entrada genera una salida, pero como consecuencia, alguna variable interna cambia. Si se vuelve a ingresar la misma entrada exacta, la salida será diferente porque el estado interno del sistema ya se modificó.  
* **Estado Transitorio (Warm-up):** Es una fase inicial de inestabilidad en las variables estadísticas del modelo que se da justo al arrancar la simulación (porque arranca "en frío" o desde el reposo). Durante este período, los promedios fluctúan muchísimo antes de estabilizarse.  
* **Análisis de Sensibilidad:** Técnica de validación donde se genera una leve variación en una entrada o variable interna del sistema para observar cómo reacciona la salida. En un sistema validado, cambios suaves en la entrada deberían reflejarse como cambios suaves en la salida (no abruptos).

## **Desarrollo de la clase**

### **1\. ¿Por qué hacemos simulaciones?**

El profesor explicó que existen múltiples motivos por los cuales se prefiere simular un sistema en lugar de trabajar con el sistema real:

* **Complejidad y disponibilidad:** A veces el sistema real es demasiado complejo, muy grande, o está en plena producción y no existe posibilidad de cambiar su configuración para ver qué pasa con variables de interés (ej. cuántos productos se fabrican, demoras en atención) sin interrumpir el negocio.  
* **Costo:** Suele ser mucho más barato (e inofensivo) experimentar en un entorno simulado que usar equipos reales, probar rendimientos o algoritmos en la vida real.  
* **Inexistencia del sistema:** En muchas ocasiones, el sistema que se quiere estudiar simplemente no existe todavía. Se construye un modelo idealizado para prever su comportamiento antes de invertir en su creación física.

### **2\. Clasificación de Sistemas y Modelos**

Se detallaron múltiples clasificaciones (abiertos/cerrados, estables/inestables, naturales/artificiales, estocásticos/determinísticos, lineales/no lineales). Para la materia, la clasificación principal se divide en:

* **Modelos Discretos:**  
  * *Sistemas Estáticos:* Análisis de riesgo, costos, ganancias, modelos de inventario.  
  * *Sistemas Dinámicos:* Modelos de líneas de espera o sistemas de colas.  
* **Modelos Continuos:**  
  * *Basados en leyes de la naturaleza:* Sistemas técnicos, mecánicos, químicos (usualmente representados por ecuaciones diferenciales).  
  * *Basados en la observación:* Sistemas económicos, políticos, sociales. Aquí interviene la voluntad humana, por lo que se conoce poco matemáticamente y es difícil representarlos con ecuaciones exactas. Suelen ser tratados como modelos de "caja negra" (totalmente opacos respecto a sus relaciones internas) o "caja gris".

### **3\. Ventajas, Desventajas y Peligros de la Simulación**

**Ventajas:**

* Permite estimar el desempeño bajo distintos escenarios y otorgar control sobre las condiciones experimentales (modificar variables a voluntad).  
* Manejo arbitrario del tiempo: permite ralentizar sistemas que en la vida real son rapidísimos para ver sus subsistemas en detalle, o acelerar sistemas que tardan meses para obtener resultados instantáneos.  
* Permite estudiar sistemas estocásticos (con variables estadísticas).  
* Se puede usar para capacitar personal (entrenar a empleados en cómo interactuar con el sistema sin romper nada real).  
* Ayuda a anticipar problemas antes de que la empresa sufra las consecuencias.

**Desventajas:**

* **Costo y tiempo:** Construir un buen modelo no es inmediato ni fácil; requiere personal altamente capacitado, tiempo y dinero.  
* **Falsa precisión:** El modelo puede aparentar reflejar con exactitud un sistema real cuando en verdad no lo hace (imposibilidad de medir exactamente el grado de imprecisión).  
* **No optimiza:** La simulación no encuentra mágicamente la "solución óptima"; solo evalúa las alternativas y configuraciones que nosotros le damos para probar.  
* Es difícil convencer al management de invertir en la creación de un modelo para simular.

**Peligros al simular (¡Muy importante\!):**

* **El error de la corrida única:** Asumir que el resultado de una sola corrida es el definitivo. Si la simulación dice "ganarás $2000", es falso casarse con ese número. Al haber variables estadísticas, otra corrida dará otro resultado. Hay que hacer estudios estadísticos de múltiples corridas.  
* **Mal uso de distribuciones:** Asignar una distribución incorrecta (ej. decir que los clientes llegan de forma exponencial, cuando en la realidad no es así). Si la entrada está mal, todo el modelo está mal.  
* **Ignorar factores humanos/tecnológicos:** En la simulación podés obligar a una máquina a trabajar al 200% o a los empleados a hacer turnos imposibles y los números darán bien, pero en la realidad los sindicatos o las limitaciones físicas de las máquinas lo impedirán.  
* **Ignorar ciclos:** Promediar resultados anuales cuando el producto tiene comportamiento estacional (un pico enorme y luego un valle). Promediar eso da un valor falso que no sirve para ningún cuatrimestre específico.

### **4\. Sistemas Terminantes vs. No Terminantes**

* **Sistemas Terminantes:** No alcanzan nunca un "estado estable" o de régimen. Existe un evento natural o condición que determina el fin de la simulación. El sistema se "vacía" o se reinicia.  
* **Sistemas No Terminantes:** Su vida se prolonga indefinidamente. Alcanzan un estado estable (las variables fluctúan, pero dentro de un rango acotado de valores).  
  * *El problema del estado transitorio (Warm-up):* Al iniciar una simulación no terminante desde el reposo (máquinas frías, empleados parados sin hacer nada), los primeros datos producidos fluctúan caóticamente. Por ejemplo, el primer producto sale carísimo, el segundo muy barato. Esto contamina el promedio final.  
  * *Cómo suprimir este error:*  
    1. Corridas muy prolongadas (para que los datos del inicio se diluyan en un mar de datos estables). No sirve si necesitamos evaluar datos hora por hora.  
    2. Inicialización adecuada: Arrancar la simulación "en movimiento", pre-cargando variables como si fuera la foto de un sistema que ya venía funcionando.  
    3. Eliminación de datos iniciales: Correr el sistema, pero borrar deliberadamente los primeros *L* resultados y promediar solo con los datos posteriores a la estabilización.

### **5\. Lenguajes de Programación en la Simulación**

Se comparó programar en lenguajes de propósito general (Python, Java, C) versus lenguajes específicos de simulación:

* **Propósito general (los que se usarán en los TP):** Permiten total libertad en el formato de salida, no hay que pagar costosas licencias, son súper flexibles y suelen tener tiempos de ejecución más rápidos. Sin embargo, hay que programar todo desde cero (recolección de datos, estadísticas). *Peligro asociado:* El manejo de memoria; en corridas largas el sistema se puede colgar o quedar sin RAM si no se gestiona bien.  
* **Lenguajes de simulación:** Ya traen componentes prearmados (arrastrar un "cajero", darle atributos). Automáticamente gestionan estadísticas, recolección de datos y administran la memoria a la perfección, evitando que se cuelgue. Son menos propensos a errores de código y ahorran muchísimo tiempo de desarrollo, compensando el costo de la licencia de software.

### **6\. Etapas del Proceso de Simulación**

1. **Definición del problema:** Saber exactamente qué queremos estudiar.  
2. **Formulación o modelo conceptual:** Decidir qué entidades entran en el modelo y cuáles se descartan por no afectar el funcionamiento.  
3. **Adquisición y preparación de datos:** Definir distribuciones estadísticas reales.  
4. **Programación del modelo.**  
5. **Validación:** Asegurarse de que el modelo armado realmente representa el sistema. (Si falla, se vuelve atrás).  
6. **Planeación táctica y estratégica:** Definir qué corridas y escenarios se van a probar.  
7. **Experimentación:** Ejecución de las múltiples corridas.  
8. **Análisis de resultados.**  
9. **Implantación:** Aplicar la recomendación en el sistema real del cliente.  
10. **Documentación:** Crucial para cuando haya que hacer modificaciones años después. "Da fiaca, pero es importantísimo".

### **7\. Técnicas de Validación**

Se deben validar los supuestos, los valores de entrada y los valores de salida. ¿Cómo?

* **Intuición del experto:** Trabajar codo a codo con el cliente o dueño del sistema, que es quien realmente sabe si los números que le mostramos tienen sentido en la práctica.  
* **Comparación:** Cruzar resultados del modelo con mediciones tomadas en el sistema real actual (o con bases teóricas si el sistema no existe).  
* **Análisis de sensibilidad** (ver sección "Conceptos clave").

## **Ejemplos y casos mencionados por el docente**

* **Máquina dispenser (Linealidad):** Si pones billetes en un dispenser, obtenés 1 paquete. Si pones el doble, obtenés 2\. Ejemplo de sistema lineal.  
* **Cajero de supermercado:** Ejemplo para explicar que la simulación no da la solución "óptima" automática. Uno prueba configuraciones ("¿qué pasa si pongo 5 repositores y 3 cajeros?") y evalúa cuál da menor tiempo de espera, pero la opción ideal matemáticamente podría estar fuera de los parámetros probados.  
* **Banco (Sistema Terminante vs. Supuestos):**  
  * *Como sistema terminante:* El banco abre, atiende, cierra, y atiende a los que quedaron adentro hasta que se vacía por completo de clientes. Hay un evento de fin diario.  
  * *Como validación de supuestos:* ¿Incluyo al policía en el modelo? Si solo vigila, se ignora porque no afecta la fila. Si lo obligan a hacer tareas de empleado (derivar gente, dar números), sí debe incluirse en la simulación.  
* **Batalla militar (Sistema Terminante):** Inicia la simulación de combate y termina cuando uno de los bandos pierde un porcentaje específico de fuerza.  
* **Fábrica (Estado transitorio):** Si se simula el costo medio por producto, los primeros artículos producidos muestran costos fluctuantes muy extremos (ej. el primero cuesta 30, el segundo 15, el promedio salta). Luego de un rato, la línea se estabiliza cerca del valor real (ej. 20).

## **Puntos que el docente remarcó explícitamente**

1. **"No hay nada más inútil que la solución correcta al problema equivocado"**: Frase citada de un antiguo profesor para enfatizar que la etapa 1 (Definición del problema) es la más crítica.  
2. **Nunca casarse con el resultado de una sola corrida:** Repitió varias veces que una sola corrida estadística no sirve para nada; es mandatorio hacer análisis de múltiples corridas.  
3. **Documentar da "fiaca" pero salva vidas:** Aclaró que la etapa final de documentación suele esquivarse, pero es el 90% del trabajo resuelto para mantenimientos futuros.  
4. **Cuidado con la memoria en los TPs:** Avisó que al usar lenguajes de propósito general, los estudiantes enfrentarán bloqueos o que los programas "se claven" si hacen corridas muy largas sin limpiar memoria. (Prometió enseñar trucos para mitigar esto).

## **Para el Trabajo Práctico / Evaluación (Administrativo)**

* **Regularidad:**  
  * Aprobación de 2 Parciales (con nota \>= 4).  
  * Aprobación de 5 Trabajos Prácticos.  
  * 80% de asistencia (teoría y práctica).  
* **Parciales:**  
  * *Modalidad:* Sábados a la mañana. Parte Teórica a libro cerrado; Parte Práctica a libro abierto.  
  * *Contenidos:* Parcial 1 (Unidades 1 a 4 completas); Parcial 2 (Unidades 5 y 6).  
  * *Recuperatorio:* Hay un solo recuperatorio que permite levantar un único parcial. Queda la nota más alta.  
  * *Aclaración:* No hay parcial anual ni integrador.  
* **Trabajos Prácticos (TPs):**  
  * Son 5 en total: 3 grupales y 2 individuales.  
  * Se aprueban con formato "Aprobado / No Aprobado".  
  * Hay instancias de "parcialito" (pequeñas evaluaciones en clase sobre el TP).  
  * Las entregas (sobre todo TP 4 y 5\) son instancias de evaluación individual y grupal.  
  * Hay una instancia de entrega y máximo una instancia de recuperación por TP.  
  * *Nota TPs:* Si los 5 están aprobados \= Nota 10\. Si están aprobados pero entregados fuera de tiempo o con baja participación \= Nota 4 (se pierde aprobación directa). Si alguien no trabajó \= Nota 2 (pierde la regularidad de la materia).  
  * *Grupos:* Serán grandes, probablemente de 8 integrantes (curso muy numeroso de \+215 alumnos).  
* **Aprobación Directa (Promoción):**  
  * Notas de Parciales \>= 7 (cuenta la mayor del recuperatorio).  
  * Nota de TPs \= 10\.  
* **Examen Final (Para alumnos regulares):**  
  * Misma modalidad que los parciales (Teoría libro cerrado, Práctica abierto).  
  * *Detalle clave:* Al inscribirse al final, el sistema les asigna individualmente un enunciado de un trabajo práctico de simulación para programar. Conviene inscribirse con mucha anticipación para tener tiempo de desarrollarlo y llevarlo a la mesa.  
* **Comunicaciones y Plataforma:**  
  * Todo se centralizará a través de **Autogestión** (mensajes, filminas), ya que la UV (Universidad Virtual) actualmente no funciona/no está visible para los estudiantes.  
  * *Clave de matriculación (cuando la UV ande):* sim-2026-4k2 (Todo minúscula y con guiones).

## **Dudas y cosas para revisar (Pendientes de la clase)**

* **Clase del viernes:** Quedó pendiente confirmar si la próxima clase (del día viernes) será en formato presencial o virtual. El profesor avisará a la brevedad por Autogestión.  
* **Estado de la UV:** Revisar periódicamente si Cómputos ya habilitó el Aula Virtual (UV) para poder matricularse usando la clave provista. Mientras tanto, descargar las filminas de Autogestión.