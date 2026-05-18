# **Comandos de Red, Gateways y Topologías Básicas**

**Materia:** Redes de Datos 
**Resumen en una oración:** La clase se centró en la práctica de configuración, visualización y diagnóstico de interfaces de red en Linux y Windows, abarcando comandos clave (ifconfig, ip, ping, ipconfig), y profundizando en conceptos como Puerta de Enlace (Gateway), cálculo de direcciones de red/broadcast, DHCP, DNS y la diferencia entre Dominios y Grupos de Trabajo.

## **Conceptos clave**

* **MAC Address (Dirección Física):** Identificador único de la placa de red. En Linux se puede encontrar listada como HWaddr (Hardware address) o ether, dependiendo de la versión del sistema.  
* **MTU (Maximum Transmission Unit):** Tamaño máximo del paquete de datos que puede ser transmitido a través de la interfaz de red.  
* **Dirección de Red:** Es la dirección que identifica a la red en sí. Se obtiene aplicando una operación matemática de "AND lógico" entre la dirección IP y la Máscara de Subred (esto deja todos los bits de la porción de host en 0).  
* **Dirección de Broadcast (Difusión):** Es la dirección utilizada para transmitir mensajes a todos los hosts dentro de la misma red local. Se calcula tomando la dirección de red y cambiando todos los bits de la porción de host a 1\.  
* **Gateway (Puerta de Enlace):** Es la dirección IP del dispositivo (generalmente un router) que permite a una computadora salir de su red local (LAN) para comunicarse con otras redes o con Internet. Se encarga de enrutar o encaminar los paquetes hacia su destino.  
* **ICMP (Internet Control Message Protocol):** Protocolo de mensajes de control en Internet. Es el protocolo subyacente que utiliza el comando ping para realizar pruebas de conectividad.  
* **APIPA (Automatic Private IP Addressing):** Rango de direcciones IP (169.254.x.x) que un sistema operativo Windows se autoasigna aleatoriamente cuando está configurado para recibir una IP automáticamente (DHCP) pero el servidor falla o no está disponible. Permite, al menos, la comunicación en red local.  
* **DNS (Domain Name System):** Servicio encargado de traducir y resolver nombres de dominio comprensibles para humanos (ej. google.com.ar) a direcciones IP (ej. 142.250.78.35).  
* **DHCP:** Servidor o servicio que asigna dinámicamente configuraciones de red (IP, Máscara, DNS, Gateway) a los equipos que se conectan.

## **Desarrollo de la clase**

### **Práctica en Linux: Visualización de interfaces**

Para trabajar en Linux, el docente indicó levantar una máquina virtual (LIT o Debian/Wheezy) ingresando con el usuario root.

* Se repasó el comando ifconfig. Aunque en versiones más nuevas de Linux este comando está en desuso (deprecado) y cambia ligeramente su formato visual, la información que aporta sigue siendo la misma. La interfaz física principal se identifica usualmente como eth0.  
* El comando muestra estadísticas de la placa de red a través de RX packets (paquetes recibidos) y TX packets (paquetes transmitidos).  
* **El reemplazo moderno de ifconfig:** Actualmente se utiliza el comando ip. Ejecutando ip address show o simplemente ip a, se puede obtener la misma información. Si ifconfig no viene instalado, el alumno debe saber usar la alternativa ip o instalar net-tools.

### **Diagnóstico de red: El comando Ping**

El comando ping utiliza paquetes "ICMP Echo" y recibe "ICMP Echo Reply". Al lanzar un ping, la consola devuelve información específica en cada respuesta:

* **64 bytes:** Es el tamaño del paquete enviado por defecto (este valor se puede modificar mediante opciones del comando).  
* **from (desde):** Indica la dirección IP de quien está respondiendo a la petición.  
* **seq (secuencia):** Un contador de los paquetes enviados (ej. empieza en 0 y sube sucesivamente).  
* **ttl (Time to Live):** Tiempo de vida del paquete, para evitar que quede dando vueltas infinitamente por la red si hay un bucle de ruteo.  
* **time:** El tiempo en milisegundos que tardó el paquete en ir y volver.  
* Al final de la ejecución, el sistema arroja una estadística: paquetes enviados, recibidos, perdidos, y los tiempos mínimo, máximo y promedio.

### **Topologías de red y Gateways**

Se analizó una topología que contenía dos routers conectados entre sí por un enlace serial, y cada router conectado a una PC a través de una LAN.

* **Redes de Difusión (Broadcast):** Las redes LAN son redes "punto a muchos" o de difusión. En estas redes todos "hablan con todos", por lo que para salir de esa red es obligatorio conocer y configurar un Gateway.  
* **Redes Punto a Punto:** La conexión serial entre dos routers es de punto a punto. Se conectan directamente y se terminó la red ahí, por lo que su comportamiento y necesidad de "puerta de enlace" es distinta a la de una LAN.  
* **¿Dónde está el Gateway físicamente y lógicamente?** \- Físicamente, el Gateway es la interfaz LAN del router (el punto de red que da a las computadoras locales).  
  * Lógicamente (en configuración), esa dirección IP de la interfaz del router es la que debe ser informada (configurada) dentro de los parámetros de red de cada computadora para que sepan a quién entregarle los paquetes destinados al exterior.

### **Práctica en Windows: Visualización y Configuración**

Para esta práctica se levantó una VM de Windows (XP, 7, 10 o el 11 que mostró el profesor).

* El comando equivalente en Windows es ipconfig.  
* Si un equipo Windows está configurado en automático (DHCP) y no encuentra el servidor, se activa APIPA y asigna una IP del tipo 169.254.x.x para no dejar al equipo totalmente incomunicado en la red física.  
* Configuración manual (estática): Se realiza desde Panel de Control \-\> Propiedades del adaptador de red \-\> Protocolo de Internet versión 4 (TCP/IPv4). Se debe setear IP, Máscara, Puerta de Enlace (misma red que la IP) y los servidores DNS.  
* **Información detallada:** Si se necesita ver información completa de la placa (incluyendo la dirección física/MAC, si el DHCP está habilitado, los servidores DNS o el nombre del fabricante), el comando simple no basta. Se debe ejecutar ipconfig /all.

### **Estructura Organizativa: Dominio vs Grupo de Trabajo**

En Windows, los equipos pueden agruparse de dos maneras:

* **Grupo de Trabajo (Workgroup):** Sistema descentralizado. Cada computadora es independiente, el usuario es el administrador de su propia máquina y maneja su seguridad y configuraciones.  
* **Dominio (Domain):** Entorno empresarial/institucional centralizado. Un administrador maneja todo desde un equipo central. Permite enviar directivas, manejar políticas de usuarios, restringir accesos (ej. prohibir cambiar el fondo de pantalla o hacer clic derecho), y gestionar recursos compartidos de toda la red. No cualquiera puede unir su equipo a un Dominio; se requieren credenciales y permisos explícitos del Administrador del Dominio.

## **Ejemplos y casos mencionados**

* **El celular y el DHCP:** El profesor preguntó si alguna vez pusieron direcciones IP a mano en su celular. Como la respuesta fue no, lo usó para ejemplificar el trabajo invisible del servidor DHCP que nos ahorra esta tarea.  
* **Analogía del Gateway ("Frankito en la puerta"):** Para explicar cómo funciona una red de difusión (Broadcast) y la necesidad de un Gateway, el profesor usó al curso como ejemplo. Si el curso es la LAN, para mandar un mensaje afuera de la clase hay que entregárselo a "Franco" que está parado en la puerta. Franco es el Gateway. A cada alumno de la clase (PCs) se le debe configurar la dirección de Franco para que sepan por dónde salir.  
* **El Laboratorio de Sistemas (lapsis) como ejemplo de Dominio:** Usó el propio entorno físico de la facultad como ejemplo de un Dominio de Windows. Mostró que los alumnos que se loguean con el usuario "redes" tienen restricciones (no pueden hacer clic derecho, no pueden cambiar configuraciones) impuestas por políticas centralizadas.

## **Puntos que el docente remarcó**

* **Saber identificar información en parciales:** Remarcó fuertemente que si en un examen o trabajo se muestra una captura con formato de Windows (que dice "Adaptador de red inalámbrica", "Dirección física", etc.), el alumno debe saber reconocer que el comando utilizado fue ipconfig /all y NO ifconfig de Linux. Poner ifconfig en ese caso es un error grave ("cero puntos").  
* **Identificar MAC Address sin importar la etiqueta:** Enfatizó que no importa si la salida de consola dice HWaddr o ether, lo crítico es saber identificar visualmente cuál es la dirección MAC de ese equipo.  
* **Cálculo exacto del Broadcast:** Detalló y repitió paso a paso el proceso lógico: hacer un "AND lógico" de la IP y la Máscara para obtener la dirección de Red (dejando todo a cero en la parte de host), y luego pasar toda la parte de host a unos (1) para tener la de Broadcast.

## **Para el trabajo práctico / evaluación**

* **Actividad Integradora 1:** Fecha límite 5 de mayo. Es una encuesta sencilla sobre el laboratorio, pero es obligatorio hacerla.  
* **Actividad Integradora 2:** Fecha límite 22 de mayo.  
  * **Requisito previo obligatorio:** Es vital ingresar a la UV (Aula Virtual) e inscribirse en el grupo "4K2". Si no están inscriptos en ese grupo, el botón de "Agregar entrega" para ver el enunciado no se habilitará.  
  * Consiste en armar una simulación sencilla de una topología de red LAN (similar a la clase anterior) desde cero.  
  * Se puede utilizar Packet Tracer, RBL o cualquier otro software. **Aviso importante:** Si usan otro software que no sean los estándares de la materia, deben grabar un video como evidencia mostrando el funcionamiento.  
* **Para la clase práctica actual:** Loguearse siempre con el usuario "redes" y usar usuario root en los sistemas virtualizados (LIT o Debian). Completar el PDF con los comandos provistos antes de terminar.

## **Dudas y cosas para revisar**

* Queda pendiente para clases futuras ver a profundidad el "encabezado de IPv4", la "fragmentación de paquetes" al superar el MTU, y cómo funcionan de fondo los mensajes del servicio DNS.  
* Un alumno consultó sobre el "Certificado 2438", a lo cual el docente aclaró que es un servicio que corre por detrás de las páginas web pero que no será tema de estudio en esta materia.