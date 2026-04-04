# **Introducción a la Investigación Operativa**

**Materia:** Investigación Operativa (IO) / Ingeniería en Sistemas  
**Resumen en una oración:** Clase introductoria sobre el rol de la investigación operativa en la toma de decisiones mediante modelos matemáticos, su historia, conceptos básicos de modelización y las reglas de cursado para regularizar o alcanzar la aprobación directa.

## **Conceptos clave**

* **Investigación Operativa (IO):** Es la disciplina que transforma problemas que tienen las organizaciones en modelos matemáticos (cuantitativos) para poder tomar mejores decisiones. En lugar de ser solo una "matemática abstracta", es ingeniería aplicada a decisiones.  
* **Problema de Decisión:** Se presenta frente a una situación problemática *solo* cuando existe más de un curso de acción o alternativa para afrontarla. Si hay una sola opción, no hay un problema de decisión. La meta en IO es encontrar la alternativa o solución óptima para estos problemas.  
* **Modelo:** Es una representación simplificada de la realidad. Al ser "simplificada", implica que no contempla el 100% de las variables del mundo real, sino las necesarias para resolver el problema. En IO se trabaja específicamente con *modelos cuantitativos* (matemáticos).  
* **Modelos de Optimización:** Son aquellos modelos que devuelven la *mejor decisión posible* (solución óptima). Buscan maximizar (ej. ganancias) o minimizar (ej. costos) una función.  
* **Modelos de Descripción:** Son modelos que no optimizan directamente, sino que describen cómo funciona un sistema bajo ciertos parámetros y de acuerdo a la información disponible. Para mejorar el sistema en estos casos, el usuario debe modificar los parámetros manualmente e iterar.  
* **Solución Óptima:** El término "óptimo" es absoluto. Significa que es la mejor solución posible y no existe otra superadora bajo las condiciones dadas. No se debe decir "la solución más óptima".  
* **Parámetro vs. Dato:** El parámetro es una parte del modelo que está matemáticamente indeterminada en su forma general (como una variable conceptual, ej. coeficiente de costo). Cuando se aplica a un caso particular y se le asigna un valor numérico específico (ej. 150 pesos), deja de ser un parámetro general y se transforma en un "dato" o constante.  
* **Restricciones:** Son todas aquellas limitaciones físicas, de recursos o de negocio que el sistema debe cumplir obligatoriamente para que la solución sea válida.  
* **Hipótesis / Supuestos:** Dado que el modelo es una simplificación de la realidad, requiere formular supuestos o hipótesis que limiten el alcance y permitan la resolución matemática del problema.

## **Desarrollo de la clase**

### **¿Qué hace un Ingeniero en Sistemas y qué aporta la IO?**

La clase comenzó debatiendo el verdadero rol del ingeniero en sistemas. Lejos de limitarse a "desarrollar software", el ingeniero diseña soluciones para los problemas de las organizaciones. Un sistema de información procesa datos para solucionar problemas, y en el núcleo de esas soluciones, operando de fondo, existen modelos matemáticos.  
La Investigación Operativa aporta al ingeniero el **pensamiento estructurado**. Enseña a definir correctamente los problemas, formular hipótesis y, sobre todo, a **pensar en términos de optimización bajo restricciones**. Esta forma de pensar es una competencia profesional clave, ya que en la vida real todos los sistemas y organizaciones tienen restricciones (tiempo, dinero, recursos). Además, facilita la interacción con otros profesionales (gerentes, administradores, contadores), dándoles a los ingenieros un vocabulario y una lógica común para la toma de decisiones basada en datos.

### **Historia de la Investigación Operativa**

La disciplina nace formalmente durante la Segunda Guerra Mundial, impulsada por la Armada Inglesa. En ese entonces, reunieron a un equipo interdisciplinario de científicos (matemáticos, físicos, estadísticos) para investigar las operaciones tácticas y estratégicas de la guerra. El objetivo era asignar de la manera más eficiente posible recursos sumamente escasos: hombres, armamento y comida. De allí deriva el nombre "Investigación de Operaciones".  
En la posguerra, los científicos notaron que las industrias y organizaciones se enfrentaban exactamente a los mismos problemas logísticos y de asignación de recursos. A partir de 1947, con el desarrollo de algoritmos fundamentales como el Método Simplex (creado por George Dantzig para resolver problemas de programación lineal) y el posterior auge de las computadoras, la IO se integró masivamente en el sector empresarial. Hoy en día es la base algorítmica de software de gestión masivos y de logística.

### **El proceso de un Problema de Decisión**

El objeto de estudio central de la materia son los "problemas de decisión". El ciclo para resolverlos tiene cuatro pasos:

1. **Analizar el problema:** Comprender la situación y la necesidad.  
2. **Modelizar:** Convertir el problema del mundo real en un modelo matemático (identificar variables, función objetivo, parámetros y restricciones).  
3. **Resolver:** Aplicar un algoritmo (ej. Simplex) mediante software para encontrar la solución óptima.  
4. **Comunicar:** La profesora remarcó fuertemente este paso. Si la solución se calcula de forma excelente pero no se sabe comunicar de manera clara al decisor (el gerente, el cliente), este no la va a aceptar ni implementar.

### **Planificación Anual de la Materia**

* **Primer Semestre (Programación Matemática):** El enfoque estará en la "Programación Lineal". Se verá el algoritmo Simplex, análisis de dualidad, análisis de sensibilidad (qué pasa si cambian las condiciones del problema) y algo de optimización no lineal. Esto se aplica a asignación de recursos, optimización de costos y planificación de producción.  
* **Segundo Semestre (Modelos avanzados de IO):** Se trabajará con Modelos de Redes (árbol de expansión, ruta más corta), modelos de Pronósticos (esenciales para cualquier tipo de planificación) y Modelos de Inventarios.

### **Metodología de Trabajo**

La cátedra adopta un enfoque de "Aprendizaje basado en problemas" y un rol activo por parte del estudiante, trabajando colaborativamente en pequeños grupos (hasta 7 personas). Se utilizará una modalidad híbrida, apoyándose mucho en el Aula Virtual (Moodle) para tareas y material, lo cual es vital, especialmente frente a paros docentes o feriados.

## **Ejemplos y casos mencionados**

* **El GPS (ej. Google Maps):** Es un sistema cotidiano que contiene un modelo interno de IO. No "adivina" el camino; utiliza un algoritmo de la ruta más corta/eficiente/barata para optimizar el trayecto basándose en datos del tráfico y distancia.  
* **Sistema SAP:** Este famoso ERP empresarial contiene embebidos en su código múltiples modelos de IO, como por ejemplo los modelos clásicos de gestión de inventarios, aunque el usuario final no sepa que está usando "Investigación Operativa".  
* **Ir al cine o al teatro:** Un ejemplo básico para ilustrar qué es un "problema de decisión". Solo es un problema porque hay *más de una alternativa*. Si la única opción es quedarse en casa, el problema de decisión desaparece.  
* **Fenómeno de espera en fila (colas):** Se usó para explicar los "Modelos de Descripción" (ej. en simulación). Modela la llegada de clientes a un servidor (ej. estación de servicio o caja de banco). No te da la solución óptima, pero te predice el futuro: te describe, dada la configuración actual, cuánto tiempo esperará un cliente en la cola. Para optimizarlo, el humano debe cambiar los parámetros (ej. poner más servidores).  
* **Cálculo de contribución total a las utilidades:** Para ilustrar la diferencia entre "parámetro" y "dato/constante". La fórmula genérica *Beneficio \= (a \* x1) \+ (b \* x2)* usa parámetros (*a* y *b*). Cuando a ese producto particular se le asigna un valor (ej. 150 y 350 pesos), esos parámetros se convierten en datos constantes para el sistema.  
* **La ruta de la profesora al trabajo:** Un ejemplo de cómo la materia "enseña a pensar en términos de optimización". Ella explicó que mentalmente y de forma automática calcula su ruta analizando embotellamientos buscando la ruta más corta bajo la restricción del "horario pico".

## **Puntos que el docente remarcó**

* **Uso del celular en clase:** La profesora fue sumamente estricta con esto. Prohibido chatear o usar el teléfono mientras da la clase. La asistencia no es obligatoria, por lo que asume que el que va, va a prestar atención.  
* **Comunicación de resultados:** Subrayó que el trabajo matemático no sirve de nada si el ingeniero no es capaz de comunicar la solución de forma clara al cliente o gerente ("si no lo sé comunicar, el decisor no lo va a aceptar").  
* **"Óptimo" es absoluto:** Fue muy enfática en que no existe "la más óptima" o "mejor óptima". Óptimo significa que es la mejor solución matemáticamente posible y no hay otra que la supere.  
* **Los modelos en el código:** Repitió varias veces la frase *"Detrás de cada decisión tecnológica o solución que programen, hay un modelo"*.  
* **Ausencias a clase:** Como no se toma asistencia, no estar presente en una clase no es excusa para no saber un tema para el parcial. El alumno es responsable de mantenerse al día mediante el Aula Virtual.

## **Para el trabajo práctico / evaluación**

### **Condiciones de Regularidad**

* Tener **2 parciales aprobados**. Se aprueban con el 60% (Nota \= 6). IMPORTANTE: El parcial debe tener un 60% correctamente desarrollado de *cada tema individual evaluado* (ej. no sirve tener todo excelente en programación lineal y dejar en blanco análisis de sensibilidad; se evalúa conocimiento integral).  
* Tener **3 Trabajos Prácticos (TPs) grupales aprobados**.  
* **Recuperatorios:** Se puede recuperar **1 solo parcial** (reemplaza la nota si es mayor) y **1 Trabajo Práctico** (la nota reemplaza al 4to TP).

### **Condiciones de Aprobación Directa (AD)**

* **2 parciales aprobados con nota 7 o superior** (implica tener un 70% o más). Mismas reglas de distribución de conocimiento.  
* **3 TPs grupales aprobados con nota 8 o superior**.  
* **Evaluaciones virtuales en Moodle:** Hay que aprobar **5 de 6** cuestionarios teóricos/prácticos estructurados en el Aula Virtual. Estos cuestionarios NO tienen recuperatorio, aunque permiten 2 intentos cada uno (cuidado, las preguntas/números pueden cambiar entre intentos).  
* **Recuperatorios en AD:** Se puede recuperar 1 parcial o 1 TP para alcanzar la condición. *Atención:* El recuperatorio NO se puede usar para "levantar promedio" si ya se sacaron un 7\. Solo es para cambiar la condición si se sacaron menos de 7\.

### **Herramientas de Software a utilizar**

* **LINDO:** Software comercial pero con versión de prueba gratuita muy útil. Se descarga desde lindo.com. Es muy fácil de usar porque se carga el problema tal cual se escribe en papel.  
* **Solver (Excel):** Es un complemento de Excel (o software de hojas de cálculo equivalente) utilizado para programación lineal y no lineal. Hay que habilitarlo en *Archivos \> Complementos*.  
* *(Nota: Existe LINGO, pero a la profesora no le gusta para la cursada).*

### **Tareas y Próxima Clase**

* **Libro:** Descargar o conseguir el libro de la cátedra (está gratis en PDF en el aula virtual en su edición anterior, la cual sirve perfecto).  
* **Lectura obligatoria:** Leer el **Capítulo 3 (Programación Lineal)** *hasta* llegar al subtítulo "Resolución Gráfica" (no incluir este último tema).  
* **Próxima clase (Viernes):** La dará la profesora "Andrea" (Claudia Andrea). Van a comenzar fuertemente con la **modelización matemática** de problemas, por eso es indispensable llevar la lectura hecha.  
* **Foros:** Toda duda (sobre ejercicios, software o fechas) debe publicarse en el Foro del Aula Virtual, no por mail privado, para fomentar el aprendizaje colaborativo.

## **Dudas y cosas para revisar**

* **Habilitar Solver:** Revisar en casa cómo habilitar el complemento Solver en Excel / LibreOffice / Google Sheets.  
* **Descargar LINDO:** Entrar a lindo.com e instalar el software para familiarizarse con la interfaz antes de los prácticos.  
* **Verificar fechas en el Excel:** La profesora mencionó que subirá un archivo Excel actualizable al Aula Virtual con el cronograma detallado de fechas de parciales y TPs. Hay que revisarlo esta semana.