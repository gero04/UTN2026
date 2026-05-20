# **Redes de Datos: Práctica de Wireshark, Ethernet (IEEE 802.3) y Dispositivos de Interconexión**

**Materia:** Redes de Datos (Ingeniería en Sistemas / Informática)  
**Resumen en una oración:** La clase comenzó con una fuerte corrección sobre la entrega y resolución del Trabajo Práctico de Wireshark, para luego profundizar en la teoría de la evolución de Ethernet, el formato de las tramas, los procesos de encapsulamiento/desencapsulamiento y el funcionamiento interno de los switches.

## **Conceptos clave**

* **Ethernet Conmutada**: Evolución de la red Ethernet clásica que reemplaza el uso de Hubs por Switches. Esto reduce el dominio de colisión a cada puerto específico del switch, permite operar en modo Full-Duplex y hace que el protocolo CSMA/CD ya no sea necesario, mejorando el rendimiento.  
* **Encapsulamiento / Desencapsulamiento**: Es el proceso mediante el cual los datos originados por un host transitan por el modelo OSI.  
  * *Encapsulamiento*: Los datos bajan de capa sumando encabezados (Datos \-\> Segmento en Capa 4 \-\> Paquete en Capa 3 \-\> Trama en Capa 2). Ocurre en el origen de la información.  
  * *Desencapsulamiento*: El proceso inverso; los datos se desglosan subiendo de capa y retirando encabezados al llegar a destino.  
* **Window Size (Tamaño de ventana TCP)**: En la capa de transporte, es un mecanismo de control de flujo. Representa una "charla" o negociación entre origen y destino sobre la cantidad de bytes que se pueden transmitir antes de saturar al receptor, permitiendo ajustar o bajar el flujo de datos dinámicamente si es necesario.  
* **Direcciones MAC (Media Access Control Address)**: Direcciones físicas planas de 48 bits de longitud (6 bytes), expresadas en 12 dígitos hexadecimales. Son únicas a nivel mundial. Los primeros 24 bits (3 bytes) son el OUI (Identificador de Organización) asignado por la IEEE al fabricante, y los restantes son el identificador específico de la interfaz.  
* **Tabla CAM**: Tablas dinámicas en la memoria RAM de un switch. Guardan el mapeo entre una dirección MAC de origen y el puerto físico por el cual ingresó la trama. Tienen un tiempo de vida (Time To Live), se borran si se apaga el equipo, y sirven para evitar enviar datos por todos los puertos (broadcast) cuando ya se conoce al destino.  
* **Atenuación**: Pérdida de potencia y calidad (amplitud) de una señal analógica o digital a medida que viaja por un medio físico (como el cable UTP). Esto es lo que limita el alcance de los cables de red.

## **Desarrollo de la clase**

### **1\. Retroalimentación sobre el Práctico de Wireshark**

La primera parte de la clase se centró en analizar los resultados del TP. Muchos estudiantes entregaron tarde y con respuestas superficiales ("lo justo y necesario"). Se observaron errores conceptuales graves que se remarcaron fuertemente:

* **Confusión de Capas:** Muchos estudiantes mezclaron protocolos de distintas capas. Por ejemplo, al leer el campo Type en la cabecera Ethernet que indicaba "IPv4", concluían erróneamente que Ethernet "era un paquete IPv4". El docente aclaró de forma tajante: **Ethernet pertenece a la capa de enlace (Capa 2), mientras que IPv4 pertenece a la capa de red (Capa 3).** El campo Type simplemente indica qué protocolo viene *encapsulado* en la carga útil desde la capa superior.  
* **La Visualización en Wireshark:** El software muestra la captura al revés del modelo teórico "Top-Down". Arranca desde la Capa 1/2 (Frame/Ethernet II) hacia arriba, pasando por Capa 3 (Internet Protocol IPv4/IPv6) y finalmente Capa 4 (TCP/UDP) o la aplicación.  
* **Conceptos de Capa 4 (Puertos y Protocolos):** TCP y UDP son protocolos de la capa de transporte. TCP está orientado a la conexión y UDP no. Los **Puertos (origen y destino)** son fundamentales en esta capa porque permiten identificar y diferenciar las aplicaciones o servicios finales que se están comunicando entre los hosts, así como la MAC identifica el hardware en la LAN y la IP identifica la ruta en la red.

### **2\. Estándares IEEE 802.3 y Evolución de Ethernet**

* **Ethernet Clásico (3 a 10 Mbps):** Surgió en 1973\. Utilizaba codificación Manchester. Funcionaba sobre cables coaxiales gruesos y finos (10Base5, 10Base2) en una **topología de bus física**, lo que generaba un gran número de colisiones y mucha dificultad al sumar nuevos equipos. Luego migró a cable UTP (10BaseT) con concentradores (Hubs) operando en Half-duplex y compartiendo el ancho de banda bajo las reglas CSMA/CD.  
* **Fast Ethernet (100 Mbps \- 802.3u):** Aprobado en 1995\. Mantuvo compatibilidad con los sistemas anteriores pero redujo drásticamente el tiempo de bit de 100 ns a 10 ns. Se usa típicamente en cables UTP Cat 5 (100Base-TX) o fibra óptica (100Base-FX) usando codificación 4B/5B \+ NRZI. Introduce firmemente los **switches** y la **autonegociación** (detectar si operar en 10 o 100 Mbps, en Half o Full-Duplex, ganando siempre el modo del dispositivo más lento para evitar pérdidas).  
* **Gigabit Ethernet (1000 Mbps \- 802.3ab/z):** Aprobado en 1999\. Transmite a 1000 Mbps sobre cobre (1000Base-T, 4 pares UTP, hasta 100m) o Fibra Óptica (1000Base-SX multimodo, 1000Base-LX monomodo). Exige mejores drivers y topologías jerárquicas en la conmutación para no generar cuellos de botella (ej. bajando troncales de Gigabit a repartos de Fast Ethernet).  
* **10 Gigabit Ethernet (802.3ae/an/ak):** Funciona **exclusivamente en Full-Duplex** y se expande más allá de la red LAN, implementándose para unir redes MAN o WAN, interconectando routers pesados o servidores de gama alta. En fibra monomodo puede llegar a grandes distancias como 10 km (10GBase-LR) o hasta 40 km (10GBase-ER).

### **3\. Formato de las Tramas (Ethernet II vs IEEE 802.3)**

Aunque son casi idénticas, hay sutiles diferencias de formato que dependen del estándar (usualmente prevalece Ethernet II, pero conviven).

* **Preámbulo y Delimitador de Inicio (SoF):** En Ethernet II hay un preámbulo de 8 bytes de patrón 10101010\. En el 802.3, son 7 bytes de preámbulo más 1 byte de Start of Frame (10101011). Esto le avisa al destino de que viene una trama y sincroniza los relojes.  
* **Direcciones:** MAC de Destino (6 bytes) seguido de MAC de Origen (6 bytes). Se envían en ese orden para acelerar la toma de decisiones del dispositivo receptor/switch.  
* **Tipo / Longitud:** 2 bytes. En Ethernet, indica el protocolo de la capa superior (ej. IPv4, ARP). En 802.3, indica la longitud de la carga útil.  
* **Datos / Carga Útil:** El tamaño mínimo es de 46 bytes y el máximo general es de 1500 bytes.  
* **CRC o FCS (Secuencia de Verificación de Trama):** Algoritmo de 4 bytes ubicado al final de la trama. El dispositivo receptor hace una cuenta con todos los bytes desde la dirección MAC destino hasta los datos. Si su resultado es igual a este campo, la trama es válida. **Si difiere siquiera por un bit (por atenuación o error), la trama se descarta entera.**

### **4\. Técnicas de Conmutación de Switches**

A diferencia de los hubs antiguos, un switch toma decisiones sobre cómo y cuándo enviar las tramas. Existen dos técnicas principales:

1. **Almacenamiento y Reenvío (Store-and-Forward):** La más utilizada en la actualidad. El switch recibe la trama completa, evalúa el CRC para asegurarse de que no tiene errores, analiza la MAC destino y recién ahí la reenvía por el puerto correspondiente. Tiene una latencia un poco más alta, pero evita propagar tráfico corrupto.  
2. **Método de Corte (Cut-Through):**  
   * *Fast-Forward (Capturado):* Lee los primerísimos bytes hasta encontrar la dirección MAC de destino y reenvía la trama inmediatamente sin verificar el CRC. Bajísima latencia, pero puede propagar tramas rotas.  
   * *Fragment Free (Libre de fragmentos):* Método híbrido. Espera a leer los primeros 64 bytes de la trama (la parte donde suelen ocurrir la mayoría de los errores lógicos y de red) y luego reenvía. Detección parcial de errores con latencia media.

## **Ejemplos y casos mencionados**

* **El rol del Ingeniero en Sistemas / Informático:** El docente usó la analogía laboral para quejarse del TP ("Ustedes no van a ir a una reunión con un jefe a hablar sin saber de qué; hay que leer la consigna, hacer una introducción, exponer un desarrollo y dar una conclusión sólida."). El cliente (en este caso el docente) debe ser convencido del conocimiento del alumno.  
* **¿Encapsulando o Desencapsulando?:** Viendo el Wireshark, el docente propuso un escenario práctico: "Si la IP de mi PC es la IP Origen, estoy originando la información, por ende mi host está encapsulando. Si la IP de mi PC es la Destino, estoy recibiendo los datos, por ende estoy desencapsulando."  
* **El hardware "todo en uno" de los ISP locales (módems hogareños):** Para ilustrar un switch físicamente, se puso de ejemplo el router que todos tienen en su casa. Es un dispositivo *integrado*: por donde entra la fibra óptica es el módulo del *Router*; las salidas RJ45 amarillas son el *Switch*; las antenas forman el *Access Point* y adentro habita el módem. Físicamente todo parece uno, pero son dominios separados internamente.  
* **Atenuación en el cableado estructurado:** El límite de Ethernet UTP son 100 metros. El docente dio el caso real del diseño de red (Norma 568): 90 metros fijos desde el patch-panel en la pared hasta el rack del switch, y se dejan 10 metros máximos como holgura para los *patch-cords* en los dos extremos. ¿Qué pasa si armás un cable de 120 metros y conectas una PC? *Va a conectar*, pero la atenuación de la señal generará errores de bits. El FCS fallará y el switch descartará tantas tramas que la red pasará todo su tiempo retransmitiendo datos basura y no habrá rendimiento real.

## **Puntos que el docente remarcó**

* **¡No dejar las cosas para último momento\!** Se notó estadísticamente por Moodle que el 50% de la clase hizo el TP horas antes y las entregas evidenciaron falta de investigación y de entendimiento profundo de los campos que mostraba Wireshark.  
* **Separación de Capas OSI:** Remarcó enfáticamente no cometer el error de nombrar la tecnología Ethernet como contenedora o creadora de IP. "Ethernet es capa 2\. IP es capa 3".  
* **Curiosidad Técnica:** Aconsejó a los alumnos no ignorar conceptos extraños como *Window Size*, *Flags TCP (PSH, ACK)*, puertos desconocidos o un *Multicast DNS (mDNS)*. Deben buscar la información y proponer hipótesis lógicas para complementar los reportes, no esquivarlos porque "no lo vimos aún en clase".  
* **Tipos de Direcciones MAC:** Hay que saber diferenciar claramente Unicast (uno a uno), Multicast (a un grupo, por ejemplo usando el primer bit del OUI en 1\) y Broadcast (a todos, todo en uno lógico, FF-FF-FF-FF-FF-FF).

## **Para el trabajo práctico / evaluación (EL PARCIAL)**

* **Modalidad y Entorno:** El parcial va a ser a través de Moodle y no será nada fácil ("no subestimen la materia"). Será extenso.  
* **Componente Práctico (Muy Importante):** En el parcial aparecerán **imágenes o ventanas de capturas de Wireshark**. Tienen que saber identificar qué proceso se está dando (encapsulamiento/desencapsulamiento), leer las direcciones MAC, IP, comprender los campos y los puertos.  
* **Consola OS:** Podrá aparecer la ventana de una consola de comandos con los resultados de algún ping/tracert o configuración de red, y ustedes deben deducir el problema o qué comando se aplicó *sin ver el comando en sí*.  
* **Componente Teórico:** Temas IP (público vs privado, rangos) y Subredes que ya se vieron (repasarlos bien porque detectó falencias), la evolución de Ethernet, cableados, y lógica de conmutación.  
* **NO ENTRA EN ESTE PARCIAL:** El tema "STP" (Spanning Tree Protocol, que atiende la prevención de bucles) **NO VA**. Se verá después del parcial debido a falta de tiempo.

## **Dudas y cosas para revisar**

* **Clasificación de IPs (Públicas vs Privadas):** Un alumno se confundió con el rango 172.x.x.x. El docente tuvo que aclarar la diferencia entre lo que asigna un proveedor (pública en tránsito) y la privada (dentro del rango 172.16.0.0 a 172.31.255.255). Es clave repasar los espacios de memoria asignados.  
* **Puertos Específicos:** Aunque en la clase no se ahondó en la clasificación de los puertos (Capa 4), se notó que los alumnos se sintieron desafiados por el Wireshark al no saber qué significaban. Convendrá revisar qué es un puerto lógico, los rangos de puertos bien conocidos (0-1023) y cómo se estructuran TCP y UDP en el estudio posterior.  
* **WiMAX (802.16):** Se mencionó brevemente un intercambio de dudas sobre si era lo mismo que Wi-Fi (802.11). El docente aclaró que es otra tecnología para conexiones inalámbricas Punto a Punto de gran distancia (hasta 100km). Revisar su concepto si hace falta.