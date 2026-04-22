# **Práctico de Direccionamiento Básico IPv4 y Diagnóstico**

**Materia:** Redes de Datos
**Resumen en una oración:** La clase práctica se centró en la configuración de interfaces de red IPv4 mediante la terminal (ifconfig), la comprobación de conectividad interpretando los mensajes del comando ping (ICMP) y la observación básica de la tabla ARP.

## **Conceptos clave**

* **Interfaz lógica (lo / loopback):** Es una interfaz virtual que todas las PCs tienen (ya sea en Windows o Linux). El sistema operativo levanta la pila de protocolos por defecto para esta interfaz y sirve únicamente para testeos a nivel local. No es configurable, no se le puede asignar una IP para que pertenezca a una red, y no registra tráfico real (paquetes transmitidos/recibidos, errores).  
* **Interfaz física (ej. eth0):** Es la representación en el sistema de la placa de red física (NIC, ya sea Ethernet, Wi-Fi, etc.) a través de la cual enviamos y recibimos paquetes reales. A esta interfaz sí se le configura la IP y la máscara de subred.  
* **Dirección MAC (HWaddr / Physical Address):** Es la dirección física de capa 2 de la placa de red. Está en formato hexadecimal y es única e irrepetible para cada interfaz en el mundo (viene de fábrica). Los primeros 3 octetos identifican al fabricante y los últimos 3 son asignados aleatoriamente en la fabricación.  
* **Máscara de subred:** Es un parámetro inseparable de la dirección IP que sirve para identificar a qué red pertenece el equipo. Determina qué porción de la IP corresponde a la red y qué porción corresponde al host (identificando la red con los "1" lógicos).  
* **Protocolo ICMP (Internet Control Message Protocol):** Protocolo de capa 3 que sirve para controlar la conectividad. Es el protocolo subyacente que utiliza el comando ping para devolvernos las respuestas.  
* **Tabla ARP (Address Resolution Protocol):** Es una tabla (caché) que se arma internamente en el buffer de la placa de red de la computadora. Vincula (mapea) la dirección IP de destino (capa 3\) con su correspondiente dirección MAC (capa 2\) para permitir la comunicación.

## **Desarrollo de la clase**

### **Análisis de Topologías y Redes**

Al observar una topología en el simulador, es crucial identificar correctamente la cantidad de redes. Si en el medio de la topología hay un switch y ningún router, estamos hablando de **una sola red**. El switch es un dispositivo de capa 2 que no divide redes.  
En la práctica se utilizó la red 192.168.1.0/24. Al ser /24, utiliza la máscara por defecto de una red Clase C (255.255.255.0). Esto significa que todos los equipos en esa topología mantendrán los tres primeros octetos (192.168.1) iguales, y solo variará el último octeto (el host).

### **Análisis de interfaces con ifconfig**

Para conocer el estado de las interfaces en Linux se utiliza el comando ifconfig. Si la interfaz está dada de baja, no aparecerá al ejecutar el comando sin parámetros. Para ver interfaces físicas que existen pero no están habilitadas, se usa ifconfig \-a.  
Para levantar (habilitar) una interfaz apagada se usa: ifconfig eth0 up.  
Parámetros importantes que devuelve la salida de ifconfig:

* **Link encap:** Indica el protocolo de encapsulamiento a nivel de capa 2 (por ejemplo, *Ethernet*).  
* **HWaddr:** Muestra la dirección MAC de la interfaz.  
* **Bcast (Broadcast) / Multicast:** Configuración de direcciones de difusión (no estaban configuradas en este paso específico).  
* **MTU (Maximum Transmission Unit):** Generalmente configurado en 1500 bytes. Define el tamaño máximo de la unidad de transmisión para que en el destino los paquetes se puedan reordenar y desencapsular correctamente de forma estandarizada.

### **Configuración de la Dirección IP**

Para asignar una dirección IP a una interfaz en caliente (en vivo), se utiliza la siguiente sintaxis:  
ifconfig \<nombre\_interfaz\> \<direccion\_IP\> netmask \<mascara\_subred\>  
*Ejemplo:* ifconfig eth0 192.168.1.10 netmask 255.255.255.0  
**Regla de oro:** Nunca se puede configurar un equipo solo con una IP; siempre debe ir acompañada de su máscara de subred (netmask). La IP y la máscara son un conjunto indivisible para que el equipo entienda en qué red se encuentra.

### **Comprobación de conectividad: Comando ping**

El comando ping sirve para verificar la conectividad entre equipos. En Linux, por defecto, el ping envía un flujo continuo de paquetes de forma indefinida hasta que el usuario lo detiene manualmente (con Ctrl \+ C). En Windows, el comportamiento por defecto es enviar solo 4 paquetes, requiriendo el parámetro \-t si se desea un ping indefinido.  
Dejar el ping corriendo es útil en la vida real para monitorear enlaces, evaluar tiempos de respuesta, ver variaciones y detectar pérdida temporal de paquetes.  
La salida del ping devuelve:

* Secuencia del paquete (icmp\_seq).  
* Dirección IP de destino.  
* Tiempo de respuesta (Time \= X ms).  
* Al cortarlo, muestra una estadística: paquetes transmitidos, recibidos, porcentaje de pérdida y tiempos promedio.

### **Errores comunes al usar ping**

Interpretar el error que arroja el ping es vital para el diagnóstico:

1. **Network is unreachable (Red inalcanzable):** Ocurre cuando se hace ping a una dirección IP que pertenece a una red completamente distinta a la configurada, y el equipo no sabe cómo llegar a ella (no hay ruta/gateway). El comando se corta inmediatamente sin intentar enviar más paquetes.  
2. **Destination host unreachable (Host de destino inalcanzable):** Ocurre cuando se intenta llegar a un equipo que teóricamente está en la *misma red* (ej. 192.168.1.10 a 192.168.1.100), pero ese equipo destino no existe, está apagado, tiene el cable desconectado o no tiene la IP configurada. El equipo origen se queda enviando los paquetes y reintentando (ej. envía 6, pierde 6\) porque asume que el host debería estar ahí.

### **La tabla ARP**

Cuando hacemos un ping, la PC necesita saber la dirección MAC del destino para armar la trama de capa 2\. Si no la conoce, pregunta a la red y luego guarda esa relación (IP \-\> MAC) en la tabla ARP (arp \-a para visualizarla).

* Si el ping es exitoso, la tabla guarda la IP junto con la MAC real (ej. HWaddress 00:xx:xx...).  
* Si se hace ping a un equipo de la misma red que no existe (ej. la .40), el ping falla y la tabla ARP puede mostrar la IP con una MAC en ceros (00:00:00:00:00:00) o incompleta, ya que nadie respondió con su dirección física.  
* Esta caché se vacía automáticamente (aprox. cada 30 segundos en algunos sistemas) si no hay comunicación continua, aunque se puede configurar estáticamente (no recomendado por cuestiones de administración, salvo casos estrictos de seguridad).

### **Persistencia de la Configuración**

Todo lo configurado con ifconfig se borra si la máquina se reinicia (reboot).  
Para hacer que la configuración IP sea permanente, se debe modificar el archivo de interfaces: /etc/network/interfaces.  
En este archivo se pueden cargar los parámetros de la interfaz estática (iface eth0 ... address ... netmask ...) para que al arrancar el sistema operativo asigne automáticamente los valores. Aunque a veces en los simuladores puede fallar la carga automática, es la manera correcta de garantizar la persistencia.

## **Ejemplos y casos mencionados**

* **Caso del Switch y las Redes:** Un switch interconectando 3 PCs es 1 sola red, no 3\.  
* **Ejemplo de ping a otra red (Error humano):** El profesor escribió por error ping 182.x.x.x en lugar de 192.x.x.x. El resultado fue rápido y tajante: *Network is unreachable*. Cortó el envío ahí mismo.  
* **Ejemplo de ping a un host no configurado:** Se hizo ping desde la PC2 (ya configurada) al Servidor (192.168.1.100, sin configurar aún). El ping no se cortó, siguió enviando paquetes intentando encontrarlo, devolviendo el error *Destination host unreachable*. Al levantar la interfaz del servidor y ponerle la IP, el ping inmediatamente empezó a recibir respuesta.  
* **Ejemplo de ping a host inexistente en la misma red:** Hacer ping a la 192.168.1.30 o 1.40 (que no existían en la topología). El sistema envió los paquetes y devolvió *Host inaccesible*.

## **Puntos que el docente remarcó (¡Muy Importante\!)**

* **¡Hacer el práctico uno mismo\!** No basta con copiarse los comandos de un compañero. En los parciales y finales van a incluir **capturas de pantalla de la terminal**, y se evaluará la capacidad de interpretarlas (entender por qué tiró un error, o qué nos dice una tabla ARP). Hay que familiarizarse con la experiencia visual del simulador.  
* **La máscara es obligatoria:** Nunca configurar una IP sin su máscara de red. "Es una unión, van las dos juntas".  
* **Diferencia de errores de Ping:** Hizo muchísimo énfasis en distinguir "Network is unreachable" (tratando de llegar a otra red) vs "Destination host unreachable" (tratando de llegar a la misma red pero el equipo no responde). Dijo textualmente que *eso se toma en parciales y finales*.

## **Para el trabajo práctico / evaluación**

* **Plataforma:** Se usa el Simulador de Redes (basado en Linux/VirtualBox).  
* **Actividad actual:** Abrir la plantilla de "Direccionamiento básico IPv4".  
* **Documentación:** Tienen que armar un documento PDF con los comandos que tiran y las devoluciones de pantalla que da el simulador, a modo de bitácora, para poder estudiar de ahí después sin tener que levantar la simulación de cero.  
* **Entregas:** Aunque trabajen en equipo o usen la misma PC, **todas las entregas de reportes son individuales**.  
* **Actividad 2:** Está habilitada pero en espera hasta que se terminen de definir bien los grupos de la Actividad 1\.

## **Dudas y cosas para revisar**

* **Subnetting (Subredes):** Se mencionó brevemente cómo prestando bits (ej. usando máscara /24 o 255.255.255.0 en una IP de Clase A como la 10.x.x.x) se pueden hacer subredes, acortando la porción de host. Esto lo verán a profundidad en el teórico, pero es clave tener muy en claro cómo la máscara dicta el límite red/host.  
* **Fijar la tabla ARP:** Se mencionó que es posible fijar estáticamente una dirección MAC con una IP para que no se borre de la caché, pero se profundizará más adelante si aplica a temas de seguridad de la materia.  
* **Guardar todo para la próxima clase:** El profesor indicó al final de la grabación que iban a ver "cómo guardar toda la configuración", lo cual quedó pendiente para el final/próxima clase.