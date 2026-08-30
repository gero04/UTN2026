## 1. Redes WLAN
### 1.1 Temario
- Características de las WLAN
- Access Point
- Router modem WiFi
- Arquitectura de IEEE 802.11
- Modos
- Servicios del sistema de distribución
- Estándares 802.11
- Seguridad
- Formato de la trama
- Bluetooth
- WiMax
### 1.2 Características de las redes WLAN
Las redes **WLAN** (**W**ireless **L**ocal **A**rea **N**etwork o Red Inalámbrica de Área Local) se componen de un conjunto de dispositivos conectados entre sí mediante ondas electromagnéticas de radio enlace. 
Esto permite mayor movilidad a los usuarios al minimizar las conexiones cableadas y, debido a ello, son más populares en los hogares para compartir el acceso a Internet entre varios dispositivos. 
Su principal **ventaja** reside en la reducción del costo, debido a que no tenemos que utilizar tantos cables como en una red LAN tradicional y tampoco tenemos que realizar mucha planificación.
Sus principales **desventajas** son en seguridad, debido a que estaremos mostrando nuestra red de manera pública, y además también estaremos ingresando en nuestro dispositivo a multitud de redes públicas, exponiendo y dejando vulnerable nuestra privacidad.
### 1.2 Access Point
El **Access Point**, o punto de acceso, es un dispositivo de red que interconecta equipos de comunicación inalámbricos para formar una red inalámbrica que interconecta dispositivos móviles o tarjetas de red inalámbricas (por ejemplo Notebooks, Tablets, Smartphones, Smart TVs).
Los estándares que utiliza la IEEE 802.11 permiten la conexión de una red cableada con una red inalámbrica, brindando mayor movilidad a los usuarios y conectando redes con protocolos de enlace diferentes, realizando una conversión de tramas en el proceso. Para esto, es necesario que cada uno de los dispositivos conectados tenga una dirección IP para poder ser configurados y comunicarse entre sí en las redes.
### 1.3 Modos de implementación de una red WLAN
1. ***Modo Ad-Hoc***: En este modo, un conjunto de computadoras están asociadas entre sí, lo cuál permite que se puedan enviar tramas entre sí. En este modo no está presente un Access Point.
2. ***Modo Infraestructura***: En este modo, cada cliente o dispositivo se asocia a un Access Point, donde este último se conecta a otra red (la cableada) y realiza las funciones de coordinación donde todo el tráfico de red pasa a través de él (es decir, el cliente envía y recibe sus tramas a través del Access Point). En este modo es posible conectar varios AP juntos mediante una red por cable para formar un "sistema de distribución", formando así una red 802.11 extendida.
### 1.4 Router módem WiFi
El router de servicios integrados (ISR) es un dispositivo comúnmente usado en redes inalámbricas hogareñas, que permiten interconectar dispositivos varios (PC, notebooks, smartphones, etcétera) debido a que brinda las siguientes funciones:
- ***Router***: Direcciona (enruta) las solicitudes internas.
- ***Switch***: Interconecta dispositivos.
- ***Access Point***: Junta las señales en un solo lugar.
- ***Módem***: Modula y le asigna una frecuencia a cada dispositivo.
- ***Conexión a Internet***: Provista e instalada por el ISP.
- ***DHCP***: Asignación dinámica de direcciones IP.
### 1.5 Arquitectura de IEEE 802.11
Esta arquitectura se compone de un sistema basada en arquitectura celular, donde usamos celdas llamadas **BSS** (**B**asic **S**ervice **S**et o Conjunto de Servicio Básicos, siendo este un conjunto de estaciones que se comunican entre ellas ya sea por modo ad-hoc o modo infraestructura) que es controlado por su propio Access Point el cual está conectado a una red troncal o DS (**D**istribution **S**ystem). A este conjunto se lo conoce como ESS (**E**xtended **S**ervice **S**et ó Conjunto de Servicio Extendido) que resulta ser la unión de todas las celdas posibles de una red. 
En esta arquitectura se reconocen los siguientes componentes:
1. Estaciones o dispositivos finales.
2. Medio inalámbrico (radio frecuencias).
3. Celda: Área geográfica en la cual una serie de dispositivos se interconectan entre sí por un medio inalámbrico.
4. Access Point: Une las redes y dispositivos funcionando como un **bridge** o puente.
5. Sistema de distribución (DS): Proporciona movilidad entre celdas.
6. BSS: Servicios basicos de comunicaciones.
7. ESS: Union de varios BSS.
### 1.6 Servicios del Sistema de Distribucion
#### 1. Asociacion
- Una estacion debe estar asociada a un AP a traves de un SSID
- El SSID (Service Set Identifier) es el nombre que identifica la red y debe estar formado por 32 caracteres como maximo. Todos los dispositivos dentro de un BSS deben compartir el mismo SSID
- Una estacion solo puede estar asociada a un AP a la vez
- El DS debe conocer en que AP se encuentra la estacion
- Las estaciones anuncian al AP su identidad y capacidad usando balizas
- Se utilizan tramas para descubrir el AP y asociarse
#### 2. Disociacion
- Utilizado por las estaciones antes de apagarse o salir de la red
- La estacion base puede usarla antes de su mantenimiento
- Cualquier de las partes (AP o estacion) pueden terminar la asociacion
#### 3. Reasociacion
- Permite que una estacion deje la asociacion de un AP para pasar a asociarse a otro AP
#### 4. Distribucion
- Servicio por el cual se trasladan los datos desde el origen al destino
- Los datos enviados al AP local fluyen por el DS hasta el AP remoto, llegando asi a la estacion destino
#### 1.6.1 Servicios Extra
- El cliente se debe asociar con un AP o router inalambrico
- Se utilizan tramas de administracion para completar los procesos de:
	- Descubrir nuevos AP inalambricos
	- Autenticar con el AP
	- Asociarse al AP
- Para permitir la negociacion de estos proceso se deben configurar los parametros en el AP y luego el cliente
### 1.7 Asociacion de un cliente inalambrico
Para asociarse, un cliente inalambrico y un AP deben acordar parametros especificos:
- SSID: El cliente debe conocer el nombre de la red a la cual se va a asociar
- Contraseña: Para que el cliente se autentique en el AP
- Modo de red: Estandar 802.11 que se este utilizando
- Modo de seguridad: Parametros de seguridad (WEP, WPA, WPA2, WPA3)
- Configuracion de canales: Las bandas de frecuencia en uso
### 1.8 Confiabilidad en IEEE 802.11
Las redes inalambricas son ruidosas e inseguras, debido a que tienen interferencias con otros dispositivos. Al alejarnos de las celdas empezara a suceder que nuestra señal se deteriora y sufre mas interferencias. Como estrategia, es bueno bajar la tasa de transmision si se pierden demasiadas tramas y cuando veamos que se empiezan a entregar tramas exitosamente, la estacion puede aumentar la tasa de transmision. Entre mas corta sea la trama, mayor va a ser la rpobabilidad de que la trama llegue correctamente a destino. Ademas, dividir la trama en fragmentos numerados individualmente permite que no se pueda transmitir el fragmento **k + 1** hasta no haber recibido exitosamente el fragmento **k**. Estas estrategias generan mayor seguridad en la transmision. 
Por ultimo, cuando nos asociamos al canal se envían multiples de estos fragmentos en ráfaga para obtener mayor fiabilidad. 
### 1.9 Ahorro de energía en IEEE 802.11
La duración de las baterías en los dispositivos móviles es importante, por ende el objetivo del ahorro de energía es que los clientes no tengan que desperdiciar energía cuando no tienen información para enviar o recibir, entrando en un modo de ahorro de energía. 
Para entrar en dicho modo, el cliente debe avisarle al Access Point que entrará en Modo de Ahorro de Energía, estando en una topología de infraestructura, y este último empezará a guardar las tramas en un buffer antes de volver a activarlo.
#### 1.9.1 Tramas Baliza
Las tramas baliza (o **beacon frames**) son difusiones periódicas realizadas por el Access Point cada 100 milisegundos. Anuncian la presencian del AP a los clientes (como hacen los routers en los hogares) y llevan parámetros del sistema como el identificador del AP, tiempo restante para la siguiente baliza y configuración de seguridad.
### 1.10 Pila de protocolos IEEE 802.11
![[PilaDeProtocolosIEE802.11.png]]
### 1.11 Consideraciones por estándar
#### 1.11.1 Estándar IEEE 802.11
- Transmite señales (sin requerir licencia) por las bandas de frecuencia de **2.4 GHz** y **5 GHz**
- Bandas de frecuencias utilizadas por portones automáticos, teléfonos inalámbricos, hornos microondas, etc.
- La banda 2.4 GHz está más saturada que la de 5 GHz
#### 1.11.2 Estándar IEEE 802.11a
- Aprobado en 1999
- Utiliza la banda de frecuencias de 5 GHz
- Las señales son absorbidas más fácilmente por paredes y objetos sólidos, debido a su longitud de onda más pequeña 
- Utiliza 52 sub-portadoras de OFDM. 48 se utilizan para datos y 4 para sincronización
- Velocidad máxima 54 Mbps. (velocidad real de 20 Mbps)
- Tiene un alcance de 20km con radios especiales
#### 1.11.3 Estándar IEEE 802.11b
- La revisión del estándar original fue ratificada en 1999
- Es un método de espectro expandido con tasas máximas de transmisión de 11 Mbps
- Utiliza la banda de frecuencia de 2,4 GHz
- Los dispositivos que utilizan 802.11b pueden experimentar interferencias con otros productos que funcionan en la misma banda de frecuencia de 2,4 GHz
- Rápida aceptación en el mercado
#### 1.11.4 Estándar IEEE 802.11g
- Aprobado en 2003. Es la evolución del 802.11b
- Este estándar copia los modelos de modulación OFDM de 802.11a
- Opera en la banda de frecuencia de los 2,4 GHz (como el “b”), pero a tasas teóricas máximas de 54 Mbps (en promedio 22 Mbps como el estándar “a”)
- Es compatible con el estándar “b” y utiliza las mismas frecuencias 
- Es común que los productos soporten 802.11a/b/g en una sola NIC
#### 1.11.5 Estándar IEEE 802.11n
- Norma ratificada en 2009
- Su objetivo es brindar una tasa de transferencia real alta
- Velocidad máxima 600 Mbps (rendimiento real percibido por el usuario de 100 Mbps)
- Puede trabajar en dos bandas de frecuencias 2,4 GHz y 5 GHz, permitiendo esto compatibilidad con dispositivos basados en todas las ediciones de tecnología de WiFi (a/b/g)
- Utiliza la tecnología MIMO (múltiples entradas, múltiples salidas), que utiliza múltiples antenas transmisoras y receptoras para mejorar el desempeño del sistema
- Utiliza hasta 4 antenas para transmitir hasta 4 flujos de información a la vez
#### 1.11.6 Estándar IEEE 802.11ac
- Norma aprobada en 2014
- Es una mejora del 802.11n
- Conocido como WiFi 5 o WiFi Gigabit
- Tasas de transferencia de hasta 1,3 Gbps con 3 antenas
- Opera en la banda de frecuencia de los 5 GHz
- Utiliza hasta 8 flujos MIMO e incluye modulación de alta densidad 256 QAM
### 1.12 Seguridad en Redes inalámbricas
#### 1.12.1 Wifi Alliance
Se trata de una organizacion que promueve la tecnologia WiFi y certifica la interoperabilidad entre los productos WiFi certificados.
#### 1.12.2 Autenticación de sistema abierto
No es necesario brindar una contraseña para acceder a la red. Se usa para brindar acceso inalámbrico gratuito.
#### 1.12.3 Autenticación de clave compartida
Permite autenticar y cifrar datos entre el cliente y el AP, la contraseña se comparte entre ambas partes. A continuación, veremos los siguientes tipos:
- WEP (Wired Equivalent Privacy)
	- Sistema de cifrado incluido en el estandar original 802.11
	- Utiliza el algoritmo de cifrado RC4 con claves de 64 o 128 bits
	- No se recomienda su uso
- WPA (WiFi Protected Access)
	- Estándar de WiFi Alliance
	- Diseñado para utilizar un servidor de autenticación RADIUS
	- Implementa el Protocolo de Integridad de Clave Temporal (TKIP) que cambia claves dinámicamente
- WPA2
	- Ratificado en 2004
	- Utiliza el algoritmo de cifrado AES
- WPA3
	- Sucesor de WPA2, anunciado en 2018- Utiliza AES+SAE (permite intercambio de claves)
#### 1.12.4 Métodos de autenticación
- Personal:
	- Utilizado en redes hogareñas o en pequeñas oficinas
	- Los dispositivos se autentican con el router inalámbrico mediante una clave precompartida (**P**re **S**hared **K**ey)
- Enterprise
	- Utilizado en empresas, requiere un servidor de autenticación RADIUS (Servicio de usuario de acceso telefónico de autenticación remota, también conocido como **R**emote                    **A**uthentication **D**ial-**I**n **U**ser **S**ervice)
	- El AP se comunica con un servidor de autenticación que tiene una Base de datos con nombres de usuario y contraseñas para controlar el acceso a la red
### 1.13 Estructura de la trama 802.11
Se definen tres clases de tramas:
- Trama de datos: transportan información entre las estaciones y los Access Point
- Trama de control: brindan asistencia a la transferencia entre estaciones inalámbricas, como por ejemplo las siguientes.
	- Trama RTS (**R**eady **T**o **S**end)
	- Trama CTS (**C**lear **T**o **S**end)
	- Trama ACK (**ACK**nowledgement)
	- Trama NACK (**N**egative **ACK**nowledgement)
- Trama de administración: permiten implementar los diferentes servicios (autenticación, asociación, re-asociación, de baliza, de prueba, etc.)
La trama se construye de la siguiente manera:
![[Trama802.11.png]]
En la cual, cada campo transporta información:
#### 1.13.1 Control de trama
- Versión de protocolo: Indica la versión del estándar utilizada para que el receptor sepa cómo interpretar los bits siguientes.
- Tipo: Determina la función general de la trama (datos, control o administración).
- Subtipo: Define la función específica dentro de cada tipo, como distinguir entre mensajes RTS o CTS en el tipo de control.
- A DS: Indica que la trama se dirige hacia el DS.
- De DS: Señala que la trama proviene desde el DS.
- Más fragmentos: Avisa al receptor que la trama actual es parte de una secuencia y que aún quedan más fragmentos por llegar.
- Reintentar: Marca la trama como una retransmisión de un envío anterior que no fue confirmado con éxito.
- Adm. de energía: Informa si el emisor entrará en modo de ahorro de batería al finalizar la transmisión.
- Más datos: Indica al receptor que el emisor tiene tramas adicionales almacenadas en el búfer.
- WEP: Indica si el cuerpo de la trama ha sido cifrado.
- Orden: Notifica que la capa superior espera que las tramas se entreguen siguiendo un orden estrictamente secuencial
#### 1.13.2 Duracion/ID
Indica el tiempo estimado en microsegundos que se utilizará el canal para la transmisión actual, la longitud de la trama y su confirmación de recepción.
#### 1.13.3 DA (Destination Address) y SA (Source Address)
Direccion MAC del emisor/origen (SA) y del receptor/destino final (DA).
#### 1.13.4 RA (Receiver Address)
Dirección MAC del destinatario inalámbrico inmediato (AP por ejemplo) que recibe la señal en el primer tramo
#### 1.13.5 Control de secuencia
- Número de fragmento: Indica la posición de un fragmento específico dentro de una trama que ha sido dividida para aumentar la probabilidad de una entrega exitosa en medios ruidosos,.
- Número de secuencia: Permite al receptor detectar tramas duplicadas y reordenarlas correctamente asignando un identificador único a cada mensaje completo enviado.
#### 1.13.6 TA (Transmitter Address)
Especifica la dirección MAC del dispositivo inalámbrico que está realizando la transmisión física inmediata de la trama en ese tramo del camino.
#### 1.13.7 Cuerpo de la trama
Transporta la carga útil de datos proveniente de las capas superiores, permitiendo un tamaño de hasta 2312 bytes. 
#### 1.13.8 FCS (Frame Check Sequence)
Contiene un código de verificación de 32 bits (CRC) que el receptor utiliza para confirmar que la trama no sufrió errores durante su transporte





## 2. Direccionamiento IPv4 - VLANs
### 2.1 Temario
- Necesidad de las VLANs
- Introducción a las VLANs
- Características de las VLANs
- Tipos de VLANs
### 2.2 VLANs (Virtual Local Area Network)
- Permiten crear redes logicas separadas sobre una misma red fisica, agrupando los empleados de una oganizacion en forma logica, independientemente de su ubicacion fisica.
- Se implementan sobre switches configurables, permitiendo implementar seguridad y reduciendo los dominios de broadcast (uno por cada VLAN)
- Se debe especificar la cantidad de VLANs que habra, el nombre de cada una y que dispositivos pertenecen a que VLAN, adaptandose así a la dinámica de una organización.
- Cada VLAN tiene asignada una dirección de red/subred diferente, y si se necesita comunicar VLANs entre sí será necesario un router entre ellas.
### 2.3 Protocolo IEEE 802.11q
- Estándar publicado en 1998. Permite implementar VLANs en switches, y que varias VLANs compartan el mismo medio físico sin interferirse unas con otras.
- Agrega una "etiqueta" en la trama Ethernet que permite identificar la VLAN a la cual pertenece.
- Un switch posee enlaces troncales y enlaces de acceso, y los VLANs se configuran en los enlaces troncales de los switches.
### 2.4 Formato de la trama IEEE 802.11q
La trama Ethernet se ve así:
![[Pasted image 20260829194828.png]]
Luego, la trama 802.11q se ve así:
![[Pasted image 20260829194911.png]]
Donde la etiqueta se construye de la siguiente manera:
![[Pasted image 20260829194940.png]]
Donde:
- Tipo: Valor fijo en **0x8100**, éste indica que la trama lleva información de VLAN para que los switches puedan reconocerla
- Prioridad: Conocida como **PCP** (**P**riority **C**ode **P**oint), ocupa 3 bits y permite definir 8 niveles de prioridad (del 0 al 7), usandose para calidad de servicio (QOS)

| Valor |      Prioridad       |
| :---: | :------------------: |
|   0   | Best Effort (normal) |
|   1   |      Background      |
|   2   |        Spare         |
|   3   |   Excellent Effort   |
|   4   |   Controlled Load    |
|   5   |        Video         |
|   6   |         Voz          |
|   7   |    Control de red    |
- CFI (Canonic Format Identifier): Indica compatibilidad (entre Ethernet y Token Ring) o elegibilidad para el descarte (en caso de congestión). Puede tomar los siguientes valores.

| Valor |   Significado    |
| :---: | :--------------: |
|   0   | Formato Ethernet |
|   1   | Formato Canónico |
En versiones modernas se usa el DEI (Drop Eligible Indicator), que indica si una trama puede descartarse en situaciones de congestión. Toma los siguientes valores:

| Valor |    Significado    |
| :---: | :---------------: |
|   0   |   No descartar    |
|   1   | Puede descartarse |
- VLAN ID (VID): Ocupa 12 bits e identifica la VLAN. Como son 12 bits, entonces $2^{12}$ = 4096, existen 4096 valores posibles (0 a 4096). Sin embargo, en la práctica solamente se van a poder crear 4094 VLANs.

| VLAN ID  |           Uso            |
| :------: | :----------------------: |
|    0     | Solo prioridad, sin VLAN |
|    1     |     VLAN por defecto     |
| 2 a 4094 |    VLANs utilizables     |
|   4095   |        Reservada         |
### 2.5 Implementacion de VLANs
A cada VLAN se le debe asignar una red o subred diferente, en consecuencia el dominio de broadcast se reduce a cada VLAN en particular y cualquier mensaje de broadcast llega solo a los puertos que pertenecen a la VLAN a la cual pertenece el dispositivo emisor.
![[Pasted image 20260829202101.png]]
### 2.6 Tipos de VLANs
#### 2.6.1 VLANs Estáticas
Son denominadas VLANs **basadas en el puerto**, creadas por el administrador de la red, mediante la asignación de los puertos de un switch a dicha VLAN. Cuando se conecta un dispositivo, automáticamente asume su pertenencia a la VLAN a la que se asignó el puerto. De esta manera, son las más usadas.
#### 2.6.2 VLANs Dinámicas
La asignación se realiza a través de un servidor de base de datos VMPS (**V**LAN **M**anagement **P**olicy **S**erver). El administrador de la red puede asignar los puertos que pertenecen a una VLAN de manera automática en función de la dirección AC del dispositivo que se conecta al puerto o el nombre de usuario utilizado para acceder al dispositivo. Cuando un dispositivo accede a la red, se hace una consulta a la base de datos de miembros de la VLAN
### 2.7 Comunicación entre VLANs (Inter-VLAN Routing)
Permite que dispositivos en diferentes redes lógicas se comuniquen usando un router o switch de capa 3.
- Necesidad de router: Debido a que cada VLAN es un dominio de broadcast diferente, los paquetes no pueden pasar de una a otra directamente, sino que necesitan un dispositivo de capa 3 que tome decisiones basadas en direcciones IP.
- Uso de subinterfaces: En la técnica conocida como **router on a stick** se utiliza una única interfaz física del router dividida en multiples subinterfaces virtuales. Cada subinterfaz se configura con una dirección IP que sirve como gateway específica para cada VLAN.
- Enlace troncal: Conocido como **trunk**, es la conexión física entre el switch y el router y usa el protocolo IEEE 802.11q.
- Flujo del paquete
	1. Una PC envía un paquete a su gateway (el router).
	2. El switch etiqueta esa trama con el ID de la VLAN de origen y la envía por el enlace troncal.
	3. El router recibe la trama, la desencapsula, consulta su tabla de encaminamiento y ve que el destino es otra VLAN.
	4. El router encapsula el paquete con la nueva etiqueta de la VLAN destino y se lo pasa al switch para su entrega final.
## 3. Agotamiento de direcciones IPv4
### 3.1 Temario
- Introducción al agotamiento de direcciones IPv4
- Direccionamiento privado
- Traducción de direcciones de red
- Administración de direcciones IP
- CIDR
- VLSM
### 3.2 Agotamiento de direcciones IPv4 y sus causas
Este suceso empieza a producirse a partir del año 2000, cuando los registros regionales empiezan a quedarse sin bloques de direcciones disponibles. Las causas de esto comprenden
- Crecimiento exponencial del Internet
- Gran cantidad de usuarios conectados al Internet
- Asignación de direcciones IPv4 por clases, lo cual implicada un uso ineficiente de las direcciones.
- Conexiones de banda ancha a Internet.
- Gran cantidad de dispositivos que requieren una dirección IP (aún más con la introducción del IotT).
#### 3.2.1 Asignación Classful, la principal causa.
La asignación **classful** (por clases) fue una de las causas principales del agotamiento IPv4 debido a su extrema ineficiencia en el uso de las direcciones. En este modelo, las direcciones se entregaban en bloques fijos (Clase A, B o C) lo que obligaba a las empresas a pedir más direcciones de las que realmente necesitaban.
- Desperdicio masivo: Si una organización necesitaba conectar 500 equipos, la jerarquía classful no permitía darle un bloque exacto, se le asignaba una clase B entera (65534 direcciones) y se perdían más de 65000 direcciones en un solo caso.
- Falta de flexibilidad: No existía un punto medio entre una clase C (254 hosts) y una clase B (65534 hosts) lo que agotó rápidamente los rangos disponibles.
### 3.3 Soluciones al agotamiento de direcciones IPv4 - Protocolo IPv6
En este modelo, a diferencia del IPv4, las direcciones se asignan a las interfaces, debido a que IPv6 usa 128 bits ($3.4 x 10^{38}$ direcciones disponibles) a diferencia de los 32 bits de IPv4 ($5 x 10^{28}$ direcciones disponibles). Con esto, ya no resulta necesario usar NAT, porque cada dispositivo tiene su propia dirección IP global pública (de hecho las interfaces "esperan" tener múltiples interfaces).
Además, las direcciones tiene alcance global, local única y local de enlace, lo cual implica un encaminamiento más eficiente, usando un direccionamiento jerárquico y geográfico que permite a los routers realizar sumarización de rutas de forma más agresiva, manteniendo las tablas de enrutamiento pequeñas y rápidas. 
Por último, las direcciones tienen tiempo de vida.
### 3.4 Soluciones al agotamiento de direcciones IPv4 - RFC 1918
Fue creado como una solución temporal, permitiendo que las redes internas crezcan sin consumir IPs públicas globales.
- Uso interno exclusivo: Estas direcciones solo funcionan dentro de LANs o Intranets, permitiendo que millones de personas usen el mismo rango (por ejemplo 192.168.0.X) sin conflictos ya que cada red está aislada de las demas.
- Invisibilidad en Internet: Los routers en Internet público están configurados para ignorar y no encaminar estas direcciones. Esto ayuda a la seguridad ya que oculta la estructura y equipos internos de una organización ante atacantes externos.
- Necesidad de NAT: Para que un equipo con IP privada pueda navegar, necesita que un router realice NAT. El router actúa como un mediador, reemplazando la IP privada del paquete por una única IP pública antes de enviarlo a la red global.
- Rangos de direcciones: Se usan estos bloques reservados según el tamaño de la organización
	- Clase A: 10.0.0.0 a 10.255.255.255 (1 sola red)
	- Clase B: 172.16.0.0 a 172.31.255.255 (16 redes)
	- Clase C: 192.168.0.0 a 192.168.255.255 (256 redes)
### 3.5 Soluciones al agotamiento de direcciones IPv4 - NAT
La traducción de direcciones de red (NAT) es un proceso usado por el router para traducir IPs privadas (internas) por públicas (Internet). Sus objetivos principales son mitigar el agotamiento de las direcciones IPv4, permitir el acceso a la red global desde redes locales y brindar seguridad al ocultar la topología interna.
Existen 3 tipos:
- NAT Estática: Asocia una dirección IP privada específica con una IP pública fija. Se usa para servidores que deben ser visibles desd eel exterior y no ahorra direcciones públicas.
- NAT Dinámica: El router utiliza un conjunto de direcciones públicas asignadas por el ISP. Cuando un equipo interno intentar navegar, el router le asigna una IP disponible del conjunto. Si están todas ocupadas el siguiente dispositivo deberá esperar que se libere una.
- PAT (Port Address Translation) ó Sobrecarga: Es la forma más común y eficiente permitiendo múltiples dispositivos compartiendo una misma IP pública. Para distinguir el tráfico de cada equipo el router utiliza diferentes números de puertos (capa 4) creando una tabla de traducción que vincula la IP privada y su puerto con la IP pública y un puerto asignado.
### 3.6 Soluciones al agotamiento de direcciones IPv4 - CIDR
CIDR (**C**lassless **I**nter-**D**omain **R**outing) fue un estándar que ayudó a que IPv4 no colapsase prematuramente al distribuir geográficamente las direcciones IPv4 públicas que aún no habían sido asignadas. 
Al lograr un encaminamiento más eficiente también se logró lo siguiente:
- Utilizar más eficientemente las direcciones IP.
- Reducir el tamaño de las tablas de encaminamiento.
- Agilizar el procesamiento de paquetes en los routers.
- Permitir redes de tamaño variable según la necesidad.
Con esto, desaparece el concepto de asignación por clase, ya que se asignan las direccion IP en función de la necesidad. Esto permite repartir las direcciones IPv4 restantes en bloques de tamaño variable, y la implementación de **resumen de rutas** o **sumarización de rutas**. Las ventajas del CIDR son las siguientes:
- Elimina las clases A, B y C.
- Reduce el desperdicio de las direcciones.
- Permite crear redes del tamaño exacto necesario.
- Facilita el resumen de rutas.
- Disminuye el tamaño de las tablas de enrutamiento.
- Es utilizado tanto en IPv4 como en IPv6.
### 3.7 Soluciones al agotamiento de direcciones IPv4 - VLSM
CIDR habilita el uso de VLSM (**V**ariable **L**enght **S**ubnet **M**ask) es una técnica de subnetting que permite usar máscaras de subred diferentes dentro de una red principal, según las necesidades de cada subred. 
Con VLSM no estaremos limitados a dividir toda la red en partes iguales. En cambio, podemos asignar bloques más grandes/pequeños dependiendo del número de hosts necesarios en cada segmento.
Esta técnica:
- Permite crear esquemas de direccionamiento eficientes y escalables.
- Permite crear subredes dentro de subredes.
- Se implementa en direcciones IPv4 públicas.
- Utiliza máscaras largas para direccionar pocos hosts.
- Utiliza máscaras cortas para direccionar muchos hosts.
- Necesita de nuevo protocolos de encaminamiento.
- Se implementa un nivel más de jerarquía en la dirección IPv4.
Para aplicar VLSM, usaremos un diseño jerarquico que consiste en subdividr una red principal adaptando las mascaras bit por bit segun la necesidad real de hosts. Para no cometer errores ni solapar direcciones, se sigue una secuencia de pasos:
1. **Ordenar los requerimientos de mayor a menor**: Tenemos que hacer una lista de las subredes que necesitamos (incluyendo los enlaces punto a punto de los routers) y ordenarlas estrictamente según la cantidad de hosts que requiera cada una, de mayor a menor.
2. **Calcular los bits de host para el requerimiento actual**: Tomando la primera red de la lista, calcular cuántos bits de host ($h$) necesitamoss utilizando la fórmula $2^h - 2 \ge \text{hosts requeridos}$.
3. **Establecer la nueva máscara**: Los bits restantes del octeto se destinan a la subred. Esto alargará la máscara original (por ejemplo, pasando de un prefijo /24 a un /26 si dejamos 6 bits para hosts)
4. **Calcular las direcciones de la subred**:
	1. Dirección de subred: Primera IP del bloque (bits de host en 0).
	2. Broadcast: Última IP del bloque (bits de host en 1).
	3. Rango utilizable: Las IPs que quedan en el medio (desde subred + 1 hasta broadcast - 1).
5. **Repetir para la siguiente subred**: Tomamos la dirección IP inmediatamente posterior al broadcast calculado en el paso anterior y repetimos el proceso para el siguiente requerimiento de la lista. Como este requerimiento será igual o menor, la máscara se mantendrá o se alargará más (por ejemplo, a /27 o /28), segmentando los bloques libres de forma eficiente.
6. **Direccionar los enlaces WAN al final**: Las conexiones punto a punto entre routers solo necesitan 2 direcciones válidas, por lo que siempre se calculan al final utilizando una máscara /30 (que solo deja 2 bits para hosts y evita cualquier desperdicio).
### 3.8 Administracion de direcciones IP
La administracion y asignacion  de direcciones IP en el mundo funciona de manera jerarquica, donde IANA y los RIR son entidades responsables de manejar y controlar la cadena de distribucion, actuando como los eslabones principales de esta.
#### 3.8.1 IANA (Internet Assigned Number Authority)
Es el responsable de distribuir parte del espacio global de direcciones IP y los numeros de sistemas autonomos a los RIR. En la estructura jerarquica, es la entidad de maxima autoridad a nivel global, donde su funcion clave es garantizar el orden global y asegurar que no existan duplicaciones de direcciones IP en el planeta.
#### 3.8.2 RIR (Regional Internet Registry)
Son los organismos responsables de administrar, registrar y asignar las direcciones IP y los números de sistemas autónomos **dentro de su región geográfica específica**. El mundo está dividido en **5 grandes zonas o RIRs**. Estos registros reciben los bloques de la IANA y se encargan de repartirlos a los proveedores de servicios de Internet (ISPs) y a las grandes empresas de su área. En Latinoamerica y el Caribe, el RIR encargado es LACNIC.
## 4. ICMP
### 4.1 Temario
- Necesidad del protocolo ICMP
- Caracteristicas
- Formato de la cabecera de ICMP
- Tipos de mensajes
- Aplicaciones
- Protocolo ARP
### 4.2 ICMPv4
ICMP (**I**nternet **C**ontrol **M**essage **P**rotocol version 4) es un protocolo de la capa de red que forma parte de la familia de protocolos TCP/IP. Su función principales permitir que los dispositivos de una red intercambien mensajes de contorl, diagnostico y notificacion de errores durante la transmision de datos mediante IPv4. A diferencia de otros protocolos como **TCP** O **UDP**, **ICMP** no se usa para transportar informacion de aplicaciones de usuario, sino para informar sobre el estado de las comunicaciones en la red. 
Como el protocolo IPv4 no es orientado a conexion, (y entrega un servicio de comunicacion de "menor" esfuerzo) esto termina generando los siguientes problemas:
- Duplicacion y/o perdida de datagramas o paquetes
- Retardo y/o desorden en la entrega de datagramas o paquete
- No fiabilidad
- No se garantiza que se entregue el paquete en el destino
- No se informa si el paquete no llega a destino
- No informa la causa por la cual un paquete no es entregado
Para alivianar esto, se creó ICMP para ayudar a darle fiabilidad a las conexiones y complementar IPv4. Sus funciones son:
- Evaluacion del estados de redes
- Notificar cuando un paquete no llego a destino y el porqué
- Transporta mensajes en la capa de red
- Trabaja en conjunto con IPv4
### 4.3 Importancia del ICMP
Cuando un paquete IP no puede llegar a su destino o se presenta algun problema durante el recorrido, ICMP permite que los dispositivos involucrados informen la situacion al emisor. Gracias a ICMP podemos:
- Detectar problemas de conectividad
- Verificar si un equipo está disponible en la red
- Determinar la ruta seguida por los paquetes
- Informar errores de direccionamiento o encaminamiento
- Facilitar tareas de monitoreo y administracion de redes
### 4.4 Caracteristicas de ICMP
- Complemento a IP: Como vimos anteriormente, IPv4 es un protocolo no fiable, en el sentido de que no esta orientado a la conexion, y por eso ICMP se crea como su complemento.
- Operacion en Capa de Red: Pertenece y opera en la capa 3 (Interred o Internet en TCP/IP y Red en OSI)
- Encapsulamiento: Sus mensajes se encapsulan directamente dentro de un paquete IP. En el caso de IPv4, se identifica con el valor 1 en el campo Protocolo de la cabecera IP.
- Cabecera de 8 bytes: Posee una cabecera de 8 bytes, de los cuales 4 son fijjos y el resto depende del tipo de mensaje. Sus campos son:
	- Tipo: Define la funcion del mensaje.
	- Codigo: Especifica subtipos dentro del tipo de mensaje.
	- Suma de verificacion: Controla la integridad del mensaje para saber si descartarlo o no.
	- Encabezado opcional
	- Datos: Copia la cabecera IPv4 original y los primeros bytes de datos del paquete que fallo para que el host emisor identifique exactamente que paquete no fue entregado.
- Bajo consumo de recursos: Los mensajes ICMP soy muy pequeños, por lo que no consumen un ancho de banda significativo de la red.
- Diagnostico y control de la red: Permite controlar el estado de la red midiendo los tiempos que tardan en ir y volver los paquetes. Es la herramienta subyacente de comandos de diagnostico como:
	- `ping`: Utiliza mensajes de solicitud de eco (Echo Request) y respuesta de eco (Echo Response) para verificar si un host esta activo.
	- `tracert` / `traceroute`: Utiliza los mensajes de tiempo de vida excedido (Time Exceeded) enviados por los routers para determinar la ruta que sigue un paquete.
- Soporte de versiones: Existe una version de ICMP para cada protocolo de red.
A grandes rasgos, ICMP encapsula sus mensajes dentro de paquetes IPv4. Cuando ocurre una situacion particular en la red, un router o un host genera un mensaje ICMP y lo envia al origen del trafico para informarle lo sucedido. Por ejemplo:
1. Una computadora envia un paquete IP.
2. Un router detecta que no puede enviarlo.
3. El router genera un mensaje ICMP indicando el problema.
4. El mensaje regresa al emisor para que este conozca la causa del fallo.
#### 4.4.1 ICMP y la seguridad
Aunque ICMP es fundamental para el diagnostico de redes, tambien puede ser utilizado en ataques o actividades de reconocimiento. Por ello, muchas organizaciones:
- Filtran ciertos tipos de mensajes ICMP.
- Limitan respuestas a solicitudes Echo.
- Monitorean trafico ICMP anomalo.
SIn embargo, bloquear completamente ICMP puede dificultar la deteccion de problemas de red y afectar el funcionamiento de herramientas de diagnostico.

### 4.5 Formato de la cabecera de ICMP
El mensaje que mande ICMP se va a encapsular en un paquete IPv4. Es decir, se envia un paquete IP comun, y la carga util de este paquete (el espacio de datos que normalmente usaria un segmento TCP o UDP de la capa de transporte) se ocupa con la cabecera y los datos de ICMP. Al hacer esto, ICMP se salta la capa de transporte. Se compone de lo siguiente:

|  Campo o componente   |                                 Paquete IPv4 normal                                 |                                                                   Paquete IPv4 con ICMP                                                                    |
| :-------------------: | :---------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------: |
|     Version (4b)      |                        Indica la version 4 en binario (0100)                        |                                                                    Igual que el normal                                                                     |
|       IHL (4b)        |                            Mide el tamaño de la cabecera                            |                                                                    Igual que el normal                                                                     |
|    Protocolo (8b)     |      Contiene un valor que identifica al protocolo (6 para TCP y 17 para UDP)       |                 Contiene el valor 1 que corresponde a ICMP. Esto le avisa al receptor que no debe buscar un puerto TCP/UDP sino leer ICMP                  |
| TTL, Checksum y demas |     Campos estándar para el control de bucles y la integridad de la cabecera IP     |                                                                    Igual que el normal                                                                     |
| IPs origen y destino  |         IP del host que envía el mensaje y del host/servidor que lo recibe.         |                                 IP del dispositivo que genera el ICMP (puede ser un router intermedio) y del host destino.                                 |
|        Payload        | Comienza con la **Cabecera de Capa de Transporte** (Cabecera TCP o UDP de puertos). |                    **No hay capa de transporte**. Comienza directamente la **Cabecera ICMP de 8 bytes** (Tipo, Código, Checksum, etc.).                    |
|     Datos finales     |        Contiene los **Datos de la aplicación** (ej. texto, HTTP, archivos).         | Contiene **Datos específicos de ICMP**: En un Ping, datos de prueba; en un error, una copia de la cabecera IP que falló para que el emisor la identifique. |
Es decir, queda de la siguiente manera:
![[Pasted image 20260830125735.png]]
Donde:
- Cabecera IPv4: Es la cabecera del paquete IP que viaja por la red en el momento y porta el mensaje de error. Sus campos mas importantes son:
	- IP Origen: La direccion IP del router que detecto el problema y genero el mensaje ICMP.
	- IP Destino: La direccion IP del equipo que origino el trafico original.
- Mensaje ICMP: Se organiza en dos palabras de 32 bits, totalizando en 8 bytes o 64 bits
	- Tipo: Define la funcion general o la categoria del mensaje ICMP.
	- Codigo: Funciona como un subtipo para especifica aun mas la causa del mensaje definido en el campo anterior (Tipo).
	- Suma de verificacion/Checksum: Verifica la integridad de todo el mensaje ICMP.
	- Encabezado opcional: Es de longitud fija pero contenido variable, depende del tipo de mensaje ICMP
	- Datos: Contiene la cabecera IPv4 del paquete original que se envio y termino siendo descartado, y 8 bytes de datos que corresponden al inicio de la cabecera TCP/UDP
### 4.6 Tipos de mensajes ICMP
Este protocolo plantea la existencia de 9 mensajes en total, siendo 5 de error y 4 de informacion.

|         Mensaje         | Numero de tipo |   Funcion   |
| :---------------------: | :------------: | :---------: |
| Destination Unreachable |       3        |    Error    |
|      Source Quench      |       4        |    Error    |
|        Redirect         |       5        |    Error    |
|      Time Exceeded      |       11       |    Error    |
|    Parameter Problem    |       12       |    Error    |
|      Echo Request       |       8        | Informacion |
|       Echo Reply        |       0        | Informacion |
|    Timestamp Request    |       13       | Informacion |
|     Timestamp Reply     |       14       | Informacion |
En verdad, como el campo Tipo son 8 bits, podrian ser hasta 256 tipos de mensajes, pero estos son los mas importantes y los que vimos en clase.
#### 4.6.1 Destination Unreachable
Este mensaje es generado por un router intermedio que no puede encaminar el paquete, y se activa de manera automatica cuando un paquete IP es descartado en el camino porque no pudo ser entreado a su destino final. Se identifica con el **tipo 3** en la cabecera ICMP y tiene los siguientes codigos

| Codigo |                     Nombre                     | Significado                                                                                                                                                              |
| :----: | :--------------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|   0    |                Red inalcanzable                | La red de destino no existe                                                                                                                                              |
|   1    |               Host inalcanzable                | La red de destino si existe y es alcanzable, pero el host destino no responde                                                                                            |
|   2    |             Protocolo inalcanzable             | El protocolo de nivel de transporte no esta activo o no es soportado                                                                                                     |
|   3    |              Puerto inalcanzable               | El puerto UDP/TCP no tiene ningun servicio escuchando                                                                                                                    |
|   4    | Requiere fragmentar pero el bit DF esta activo | El paquete que se esta enviando es demasiado grande para el siguiente enlace fisico y el router necesita dividirlo pero no puede por el bit DF                           |
|   5    |              Source route failed               | Un paquete quiere usar IP Source Routing (especifica el camino exacto por donde viajar) pero un router en ese camino no puede mandar el paquete al siguiente dispositivo |
|   6    |           Red de destino desconocida           | El router desconoce por completo la red de destino                                                                                                                       |
|   7    |            Host destino desconocido            | El host de destino no existe en la red especificada                                                                                                                      |
|   8    |              Source host isolated              | \[ OBSOLETO \] El router no puede encaminar el paquete porque el host emisor esta completamente aislado de la red                                                        |
|   9    |     Comunicacion prohibida con red destino     | Un firewall/politica esta bloqueando el acceso a la red                                                                                                                  |
|   10   |    Comunicacion prohibida con host destino     | Un firewall/politica esta bloqueando el acceso al host                                                                                                                   |
|   11   |     Red inalcanzable por tipo de servicio      | No existe ninguna ruta hacia la red de destino que sea capaz de soportar el Tipo de Servicio (TOS) solicitado en el paquete IP.                                          |
|   12   |     Host inalcanzable por tipo de servicio     | Indica que, aunque la red es accesible, el host de destino no puede ser alcanzado bajo los parámetros del Tipo de Servicio (TOS) configurados por el emisor.             |
#### 4.6.2 Source Quench
Es un mensaje de la capa de red utilizado como una herramienta activa para el **control de congestión**, no tiene codigo de subcategoria por ende se le asigna el codigo 0 que se define como "No Code". Su objetivo principal es evitar que la red colapse cuando un router se ve desbordado por el volumen de tráfico entrante, notificando al host emisor para que disminuya su velocidad de transmisión.
Dicho en paisano, se utiliza para el control de congestión por parte del router cuando el buffer de mensajes está llegando al límite, lo que se hace es decirle al origen que afloje con la cantidad de mensajes por segundo. 
#### 4.6.3 Redirect
Este si posee codigos de subcategoria y lo usa un router para notificar al host local que existe una ruta mas optima o directa, o por otra cualquier razon, a traves de otro router conectado en su misma red. Tiene los siguientes codigos:

| Codigo | Nombre                                                | Significado                                                                                                                                                                      |
| ------ | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0      | Redirect Datagram for the Network                     | Indica al host emisor que configure un camino más óptimo para todo el tráfico que vaya dirigido a esa red de destino completa.                                                   |
| 1      | Redirect Datagram for the Host                        | Indica al host emisor que configure una ruta directa únicamente para llegar a ese host de destino específico (dirección IP individual).                                          |
| 2      | Redirect Datagram for the Type of Service and Network | Solicita desviar el tráfico de una red completa hacia otro router, aplicando la regla de forma exclusiva para aquellos paquetes que tengan un Tipo de Servicio (ToS) particular. |
| 3      | Redirect Datagram for the Type of Service and Host    | Solicita desviar el tráfico de un host individual hacia otro router, aplicando el desvío únicamente a los paquetes que coincidan con un Tipo de Servicio (ToS) específico.       |
#### 4.6.4 Time Exceeded
Es generado por un router o por el host de destino cuando un paquete no puede completar su trayecto antes de que expiren sus límites temporales. Este mecanismo es vital para evitar la congestión infinita de datos en la red ocasionada por bucles o loops de encaminamiento.

| Codigo | Nombre                            | Significado                                                                                                          |
| ------ | --------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 0      | Time to Live exceeded in transit  | El campo TTL de la cabecera del paquete IP llego a cero antes de alcanzar el host destino                            |
| 1      | Fragment reassembly time exceeded | Enviando por el host destino cuando no recibe todas las partes fragmentadas de un paquete dentro de un tiempo limite |
#### 4.6.5 Parameter Problem
#### 4.6.6 Echo Request
#### 4.6.7 Echo Reply
#### 4.6.8 Timestamp Request
#### 4.6.9 Timestamp Reply
