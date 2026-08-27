## Miercoles 26 de Agosto: SCM Y Trabajo practico 4
**Materia:** Ingeniería y Calidad de Software 
**Resumen en una oración:** La clase detalló los fundamentos de la Gestión de Configuración de Software para mantener la integridad del trabajo en equipo, explicó conceptos como línea base, auditorías y comités de cambios, y estableció los lineamientos para el Trabajo Práctico 4.
### Conceptos clave
- **Ítem de Configuración (IC):** Cualquier pieza o artefacto utilizado para construir un producto (código, casos de prueba, requerimientos, diagramas, base de datos, cronogramas, planes de proyecto).
- **Configuración:** Una "foto" o situación específica que se le saca al conjunto de ítems de configuración con sus versiones correspondientes en un momento dado (ej. "el 26 de agosto tenía estas cosas terminadas").
- **Versión:** Cada iteración de un mismo ítem de configuración a medida que se le van agregando cambios o mejoras (ej. Resumen ISW versión 1, versión 2).
- **Repositorio:** Lugar donde se almacenan todos los ítems de configuración con sus respectivas versiones.
- **Variante:** Ramas separadas sobre un mismo ítem de configuración para hacer pruebas y evaluar si funcionan antes de pasar a producción, con la idea de luego volver a unirlas en un solo ítem.
- **Línea Base:** Etiqueta o marca que se le pone a una configuración (conjunto de ítems) para establecer que hasta ese punto el producto es estable, fue probado, tiene calidad y cumple con lo prometido. Permite hacer un "rollback" a un punto seguro si los desarrollos futuros fallan.
- **Verificación (Física):** Evalúa si se están haciendo las cosas correctamente (ej. cumplir con la ley, nombrar el ítem como indica el plan).
- **Validación (Funcional):** Evalúa si se está haciendo la cosa correcta, es decir, si se cumple con lo que el cliente realmente pidió.
### Desarrollo de la clase
**Propósito de la Gestión de Configuración** La gestión de configuración permite trabajar en equipo garantizando que siempre se use la última versión, evitando pisar cambios, duplicarlos o generar errores al unir distintas partes del software. El objetivo fundamental de esta disciplina es cuidar la integridad del producto que se está construyendo.
**Actividades de la Gestión de Configuración** La disciplina se divide en cuatro actividades principales:
1. **Identificación** de los ítems de configuración.
2. **Control de Cambios:** Un comité evalúa si una línea base tiene defectos o requiere mejoras, analizando y aprobando modificaciones para crear una variante o una nueva línea base.
3. **Informes de Estado (Reportes):** Generación de reportes para llevar el control del proyecto.
4. **Auditorías:** Pueden ser físicas (verificación de nombres y formas documentadas) o funcionales (validación de la trazabilidad entre requerimiento, diseño, código y pruebas para asegurar que se construye lo que pidió el cliente).
**Gestión de Configuración en Procesos Definidos vs. Empíricos** Existe una diferencia clave en cómo se aplica esta disciplina según el enfoque del proyecto. En los **procesos definidos**, existe un plan documentado contra el cual auditar. Aquí cobra relevancia el **Comité de Control de Cambios**, encargado de aprobar modificaciones manuales. Nota: A diferencia de lo que apuntaste en tus notas rápidas, la profesora aclaró explícitamente que el comité de cambios es un concepto propio de procesos definidos, y generalmente no existe en procesos empíricos. En los procesos definidos, el comité se divide en:
- **Mínimo:** Para cambios menores. Conformado por roles del equipo de proyecto (líder de proyecto, arquitecto, líderes técnicos, gestor de configuración). Nunca puede ser una sola persona.
- **Ampliado:** Para cambios mayores. Es el comité mínimo más roles organizacionales (gestor de configuración de la organización, responsable de calidad, gerente de proyecto).
En los **procesos empíricos (ágiles)**, no hay una plantilla rígida contra la cual auditar de forma tradicional, ya que el proceso se define "haciendo camino al andar" mediante acuerdos del equipo, los cuales suelen ser muy estrictos. Además, se busca no gastar tiempo en actividades manuales de control que no aportan valor directo al cliente. Por ello, el control se automatiza casi por completo mediante **Prácticas Continuas (CI/CD)**. Se configuran "pipelines" (herramientas de automatización) que obligan a que el código compile y pase pruebas unitarias/integración antes de permitir un _merge_ en el repositorio común, cuidando así la integridad sin necesidad de un comité humano.
### Ejemplos y casos mencionados
- **Drive/Word:** La profesora usó el historial de versiones de Google Drive o Word como analogía de una línea base: si terminás el resumen de la Unidad 2, lo marcás; si luego la Unidad 3 sale mal, podés borrarla y volver exactamente a la configuración estable de la Unidad 2.
- **Nomenclatura de ítems:** Ejemplificó reglas de nombrado para ítems. En lugar de poner "Ejercicio práctico número 5 Charlie la fábrica de chocolate", se debe usar una lógica genérica acordada, como `ISW_Numero_TituloEjercicio` (ej. `NombreProducto_CasosDeUso_2026`).
- **Error común de repositorios:** Mencionó el caso de alumnos que subieron un repositorio de desarrollo de software (ej. un sistema de estacionamientos para la facultad) en lugar de armar un repositorio exclusivamente estructurado para gestionar los documentos de la materia.
### Puntos que el docente remarcó
- **Uso de Inteligencia Artificial:** Está permitido usar IA, pero es obligatorio revisar críticamente lo que genera. Enfatizó fuertemente que si entregan un TP con texto sin leer (ej. "reemplace el nombre de la materia aquí" o links a Wikipedia al pasar el mouse), se califica automáticamente con un 2 sin derecho a reclamo.
- **Comunicación por correo:** Se debe incluir la materia y el curso en el "Asunto" (ej. Ingeniería y Calidad de Software), usar correctamente el campo "CC" (Con Copia) y evitar los correos los viernes a la noche o con dudas que puedan resolverse en clase.
- **Diferencia entre Commit y Línea Base:** Recalcó que un _commit_ no es una línea base. El commit sube un cambio parcial de ciertos ítems, y un rollback de commit deshace todo lo modificado en él. La línea base es una "foto" integral de todos los ítems en un momento de estabilidad, y permite hacer un _tag_ (etiqueta) para volver solo a lo que se marcó como estable.
### Para el trabajo práctico / evaluación
- **Trabajo Práctico 4 (Gestión de Configuración):**
    - Se debe armar un repositorio público (o con accesos habilitados para las profesoras) en una herramienta de gestión a elección.
    - El repositorio es para gestionar los ítems de **la materia** (teórico, práctico, resoluciones), no para un proyecto de desarrollo de software.
    - Se evaluará mediante una "auditoría" donde se revisará el Plan de Gestión de Configuración de Software creado.
    - **Estructura:** Debe incluir un árbol de carpetas lógicas (ej. Teórico, Práctico).
    - **Reglas de Nombrado:** Deben definirse en una tabla que incluya: Identificación genérica del IC, Regla de nombrado (ej. `ISW_TP[N]`), Ubicación en el repositorio (directorio), y Tipo de ítem (ej. práctico, teórico). La clasificación de tipos debe ser útil (2 a 4 tipos, no 35).
    - **Líneas Base:** Se debe definir explícitamente cuándo se marcarán las líneas base, ya sea por periodicidad (ej. fines de mes) o por hitos (ej. fin de la planificación). Lo que definan, deberán cumplirlo para la entrega final del TP5.
- **Condiciones de cursada:**
    - Para regularizar: Nota 4 en los parciales y entregar todos los trabajos prácticos. Si falta entregar uno, se pierde la regularidad y no hay recuperatorio de TPs.
    - Para promocionar: 70% de los trabajos prácticos con nota 7 o superior.
    - El TP4 y TP5 se evalúan en conjunto a fin de año revisando que hayan mantenido el repositorio activo, sin subir todo a último momento ("spike").
    - **Parciales:** Son en el horario de 9 a 12 horas. No se reprograman por superposiciones, para eso está la instancia de recuperatorio.
### Dudas y cosas para revisar
- **Marcado de Línea Base en la herramienta:** Quedó de tarea para los alumnos investigar técnicamente cómo se aplica una línea base (tag) en la herramienta de repositorio que elijan (ej. Git/GitHub). La profesora aclaró que no se hace simplemente copiando carpetas ni haciendo un "commit", sino usando la funcionalidad de etiquetado/tagging de la plataforma.