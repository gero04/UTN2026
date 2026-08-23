## Viernes 21 de Agosto: Introducción a la Agilidad y Requerimientos Ágiles (User Stories) 
**Resumen en una oración:** La clase abordó la fundamentación conceptual de la filosofía ágil frente a los procesos definidos tradicionales, la estructura de la gestión de proyectos (personas, procesos, producto y proyecto), los tres pilares del empirismo y la técnica de Historias de Usuario (User Stories) para la especificación Just-In-Time de requerimientos.

---
### Conceptos clave
* **Filosofía Ágil (Agilismo):** Enfoque filosófico y marco mental basado en un conjunto de valores y principios centrados principalmente en las personas y el cambio cultural. No es una metodología ni un proceso de software.
* **Procesos Empíricos:** Procesos basados en la experiencia directa y en el aprendizaje adaptativo dentro del contexto de cada proyecto. Sostienen que la experiencia es única e intransferible (no se puede extrapolar a otros proyectos).
* **Procesos Definidos:** Procesos estructurados (como el PUD o RUP) que buscan la repetibilidad mediante una planificación detallada y la estandarización previa de actividades, asumiendo que la experiencia acumulada se puede extrapolar.
* **Los 3 Pilares del Empirismo:** **Inspección** (puntos de realimentación temprana y frecuente), **Adaptación** (capacidad de modificar producto, proceso o conducta a partir del feedback) y **Transparencia** (visibilidad y honestidad total sobre el estado real del proyecto).
* **Product Backlog:** Lista dinámicamente priorizada de características y necesidades de negocio que representa el contenedor de requerimientos del producto. Es gestionado exclusivamente por el Product Owner.
* **User Story (Historia de Usuario):** Técnica de especificación de requerimientos en ambientes ágiles que describe una necesidad desde la perspectiva del usuario final.
* **Modelo INVEST:** Criterio de calidad para evaluar la redacción de una Historia de Usuario (*Independent, Negotiable, Valuable, Estimatable, Small, Testable*).
* **Spike:** Historia de usuario con un nivel de incertidumbre tan elevado (por falta de definición funcional o técnica) que no permite su estimación ni su implementación directa, requiriendo investigación previa.
---
### Desarrollo de la clase
#### 1. Encuadre de la materia y disciplinas de la Ingeniería de Software
El docente comenzó repasando el mapa general de la asignatura y sus diferentes unidades. Dentro de la Ingeniería de Software conviven tres grandes grupos de disciplinas:
1. **Disciplinas Técnicas:** Incluyen requerimientos, análisis, diseño, pruebas (*testing*) y despliegue. Las dos últimas son el foco técnico de la materia.
2. **Disciplinas de Gestión:** Se concentran en la planificación, seguimiento y control del proyecto (Unidad 2).
3. **Disciplinas de Soporte o Protectoras:** Abarcan la Gestión de Configuración de Software (SCM), prácticas continuas (*Continuous Integration, Delivery, Deployment*), aseguramiento de calidad (SQA) y métricas (Unidades 3 y 4).
#### 2. Las dimensiones del desarrollo: El esquema de las 4 P
Apoyándose en el esquema conceptual del Proceso Unificado (PUD), se explicaron las dimensiones que interactúan en la ingeniería de software:
* **Personas:** El recurso más valioso y determinante. El software es una actividad "humano-intensiva". Sin un equipo capacitado y motivado, los mejores procesos o herramientas fracasan.
* **Proceso:** La definición teórica y estructurada de tareas para construir software.
* **Proyecto:** La unidad de gestión del trabajo con recursos y tiempo acotado. Instancia el proceso para generar el producto.
* **Producto:** El software en sus distintas versiones e ítems de configuración.
Un **Proyecto** posee cuatro características fundamentales:

1. **Resultados únicos:** Genera un producto o versión única.


2. **Duración limitada:** Posee fecha explícita de inicio y de fin.


3. **Elaboración gradual:** Cumplimiento parcializado de objetivos.


4. **Tareas interrelacionadas:** Actividades coordinadas entre sí.



#### 3. Procesos Definidos vs. Procesos Empíricos

Se contrapusieron los dos grandes enfoques para la creación y gestión de software:

* **Procesos Definidos (Tradicionales):** Buscan definir el 100% de los requerimientos y del proceso por adelantado (*upfront decision*). La organización o los ingenieros de proceso establecen actividades estrictas. Asumen que la experiencia es **extrapolable** y buscan la repetibilidad (pretenden que un proyecto rinda igual que otro similar).


* **Procesos Empíricos (Ágiles / Lean):** Asumen que el desarrollo de software involucra alta incertidumbre. Afirman que la experiencia **no es extrapolable**: cada proyecto tiene su propia dinámica y el conocimiento surge de la marcha (camino al andar).



El empirismo requiere **ciclos de vida iterativos e incrementales** y se sostiene sobre tres pilares:

* **Inspección:** Evaluación rápida del trabajo mediante iteraciones cortas para obtener realimentación frecuente del cliente.


* **Adaptación:** Acción directa derivante de la inspección. Permite corregir desvíos en el producto, ajustar actividades del proceso o ajustar conductas del equipo.


* **Transparencia:** Condición ética e informacional donde todo el equipo blanquea riesgos, problemas o demoras de forma honesta. Sin transparencia, la inspección falla y la adaptación es errónea.



#### 4. El Manifiesto Ágil: Valores y Principios

Surgido en 2001, el Manifiesto Ágil es un acuerdo fundacional estructurado en 4 valores y 12 principios.
La lectura correcta de los valores es: *"Valoramos más lo primero (izquierda/arriba) que lo segundo (derecha/abajo), sin anular esto último"*:

1. **Individuos e interacciones** por sobre procesos y herramientas.


2. **Software funcionando** por sobre documentación excesiva y detallada.


3. **Colaboración con el cliente** por sobre negociación contractual.


4. **Respuesta ante el cambio** por sobre seguir un plan.



**Aclaración sobre la documentación:** El agilismo NO prohíbe documentar. Propone posponer la documentación detallada e innecesaria hasta el momento en que aporte verdadero valor y el requerimiento esté consolidado.

Entre los principios remarcados durante la clase destacan:

* **Trabajo conjunto (Principio 4):** Técnicos y responsables de negocio deben trabajar juntos diariamente a lo largo de todo el proyecto. De la figura utópica del cliente *on-site* de XP se evolucionó al rol disponible del *Product Owner*.


* **Comunicación cara a cara:** El desarrollo es un problema socio-comunicacional. Más del 80% de la eficacia comunicativa reside en la gestualidad, el tono y la presencia cara a cara.


* **Requerimientos Emergentes:** Históricamente, el 50% de los requerimientos de un software surgen **después** de iniciado el proyecto. El equipo debe estar preparado para absorber el cambio sin forzar al cliente a congelar ideas.


* **Filosofía Just-In-Time:** Diferir las especificaciones detalladas al momento exacto en que van a ser implementadas para evitar el desperdicio.



#### 5. Requerimientos Ágiles y Product Backlog

En un entorno ágil, el contenedor de requerimientos es el **Product Backlog**:

* Es una lista priorizada de ítems/características del producto.


* El **Product Owner (PO)** es su único dueño y responsable: establece y modifica la prioridad de los ítems.


* No contiene el 100% de los requerimientos desde el día uno y jamás está "completo", ya que los ítems implementados salen del backlog y no vuelven.



#### 6. Técnica de Historias de Usuario (User Stories)

Las Historias de Usuario describen necesidades funcionales al nivel del usuario. Se componen operacionalmente de **3 partes (Las 3 C)**:

1. **Card (Tarjeta):** El soporte físico o digital con la sintaxis principal.


2. **Conversation (Conversación):** La parte más importante. El intercambio cara a cara entre el equipo técnico y el Product Owner para aclarar dudas.


3. **Confirmation (Confirmación):** Los criterios de aceptación y escenarios de prueba especificados al dorso o como parte de la tarjeta.



##### Sintaxis Estándar de la Card:

> **Como** [Rol de usuario]
> **Quiero** [Actividad / Qué debe hacer el software]
> **Para poder** [Valor de negocio / Beneficio obtenido]
> 
> 

*Nota:* No debe confundirse la historia de usuario con la **frase verbal** (ej. *"Buscar destino por dirección"*), la cual es únicamente una etiqueta corta para referenciarla informalmente.

##### Estructura completa exigida por la cátedra:

Una Historia de Usuario completa debe contar obligatoriamente con:

* Frase verbal.


* Declaración completa (Sintaxis Como / Quiero / Para poder).


* Criterios de aceptación (reglas de negocio y atributos de calidad/no funcionales específicos).


* Pruebas de usuario (escenarios de prueba que **pasan** y escenarios que **fallan**).



##### Modelo de Calidad INVEST:

Para asegurar que una Historia de Usuario está bien construida debe evaluarse bajo el acrónimo INVEST:

* **I - Independent (Independiente):** Se puede seleccionar e implementar en cualquier orden sin dependencias rígidas.


* **N - Negotiable (Negociable):** El PO define el *qué* y el valor; el equipo técnico negocia el *cómo*.


* **V - Valuable (Valiosa):** Explicita el valor de negocio real para el usuario.


* **E - Estimatable (Estimable):** Existe suficiente claridad para calcular su tamaño/esfuerzo. Si no es estimable, se transforma en un *Spike*.


* **S - Small (Pequeña):** Su tamaño permite que empiece y termine completamente dentro de una sola iteración.


* **T - Testable (Comprobable/Probable):** Cuenta con criterios que permiten verificar objetivamente si fue implementada con éxito.



---

### Ejemplos y casos mencionados

* **Evolución del software Word (Microsoft):** Usado para ilustrar cómo un producto evoluciona a lo largo de 50 años a través de múltiples proyectos y versiones (Word para DOS, versiones para Windows, paquete Office, Office 365 en la nube).


* **Metáfora deportiva (Final Argentina vs. España):** Demostración de que la experiencia previa de un equipo no garantiza resultados idénticos en situaciones futuras; la experiencia no se extrapola directamente.


* **Nomenclaturas informales de versionado:** El hábito del estudiante de nombrar archivos como *"TP_final_ultimo_v2_este_si_es_el_bueno.doc"*, usado como contraejemplo de una disciplina profesional de Gestión de Configuración (SCM).


* **Sintaxis de una User Story real:**
* *Frase verbal:* Buscar destino por dirección.


* *Card:* **Como** conductor, **quiero** buscar un destino a partir de una calle y altura, **para poder** llegar al lugar deseado sin perderme.


* *Criterios de aceptación:* La altura debe ser numérico positivo; la búsqueda no debe demorar más de 30 segundos.




* **AFIP / ARCA:** Ejemplo real de un *Spike funcional*: un ente regulador emite una resolución exigiendo cambios operativos urgentes pero sin dar detalles de implementación, generando máxima incertidumbre que impide estimar plazos o compromisos de forma inmediata.



---

### Puntos que el docente remarcó

* **El agilismo NO es una metodología ni un proceso:** Es una filosofía y un marco de pensamiento enfocado en el cambio cultural de las personas.


* **No se puede mezclar Scrum con Cascada:** Scrum es un proceso empírico iterativo; Cascada es un ciclo secuencial donde el feedback llega al final. Mezlarlos rompe los pilares del empirismo.


* **Cero de avance en el empirismo:** La gestión en agilismo es binaria ($0$ o $1$). Una historia no está "al 80%"; o está 100% terminada (probada y aprobada) o vale 0.


* **El error de omitir el "Para poder":** Eliminar la cláusula de valor de negocio transforma la User Story en un simple requerimiento técnico redactado por un analista tradicional, perdiendo la esencia de la técnica.


* **Frase verbal vs. User Story:** Decir *"Buscar destino"* es solo el nombre corto/frase verbal. La User Story es la estructura completa con el *Como / Quiero / Para poder*.


* **El problema de la comunicación:** El fracaso del 60% de los proyectos de software se debe a deficiencias en el relevamiento y comunicación de requerimientos, no a limitaciones tecnológicas.



---

### Para el trabajo práctico / evaluación

* **Evaluación parcial:** Se solicitará redactar una **User Story completa**.


* **Criterio de corrección explícito:**
* Debe incluir la **Frase Verbal**.


* Debe incluir la **Sintaxis completa** (*Como [rol], quiero [actividad], para poder [valor de negocio]*).


* Debe incluir **Criterios de Aceptación** coherentes.


* Debe incluir **Pruebas de Usuario / Escenarios de confirmación**, asegurando incluir casos felices (*pasa*) y casos de falla (*falla*).


* Si una historia presenta 5 criterios de aceptación, no se puede presentar solo 2 pruebas de usuario; todos los criterios deben poder probarse.




* **Evaluación del modelo INVEST:** Se usará el modelo INVEST para auditar si la historia escrita en el examen está bien construida.



---

### Dudas y cosas para revisar

* **Spikes:** Profundizar la lectura en la presentación (PPT) sobre los tipos de Spikes (técnicos vs. funcionales) y cómo se redactan formalmente en la práctica.


* **Criterio de elección de procesos:** La respuesta a la pregunta *"¿Cuándo conviene usar Scrum/Ágil y cuándo un proceso definido tradicional?"* quedó pendiente para ser desarrollada con mayor profundidad a medida que se avance en la materia.


* **Lectura obligatoria:** Revisar el paper de Fred Brooks (*"No Silver Bullet"*) citado en la PPT 1 y el libro *User Stories Applied* de Mike Cohn (disponible en el aula virtual).
