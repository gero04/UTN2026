## Redes WLAN
### Temario
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
### Características de las redes WLAN
Las redes **WLAN** (**W**ireless **L**ocal **A**rea **N**etwork o Red Inalámbrica de Área Local) se componen de un conjunto de dispositivos conectados entre sí mediante ondas electromagnéticas de radio enlace. 
Esto permite mayor movilidad a los usuarios al minimizar las conexiones cableadas y, debido a ello, son más populares en los hogares para compartir el acceso a Internet entre varios dispositivos. 
Su principal **ventaja** reside en la reducción del costo, debido a que no tenemos que utilizar tantos cables como en una red LAN tradicional y tampoco tenemos que realizar mucha planificación.
Sus principales **desventajas** son en seguridad, debido a que estaremos mostrando nuestra red de manera pública, y además también estaremos ingresando en nuestro dispositivo a multitud de redes públicas, exponiendo y dejando vulnerable nuestra privacidad.
### Access Point
El **Access Point**, o punto de acceso, es un dispositivo de red que interconecta equipos de comunicación inalámbricos para formar una red inalámbrica que interconecta dispositivos móviles o tarjetas de red inalámbricas (por ejemplo Notebooks, Tablets, Smartphones, Smart TVs).
Los estándares que utiliza la IEEE 802.11 permiten la conexión de una red cableada con una red inalámbrica, brindando mayor movilidad a los usuarios y conectando redes con protocolos de enlace diferentes, realizando una conversión de tramas en el proceso. Para esto, es necesario que cada uno de los dispositivos conectados tenga una dirección IP para poder ser configurados y comunicarse entre sí en las redes.
### Modos de implementación de una red WLAN
1. ***Modo Ad-Hoc***: En este modo, un conjunto de computadoras están asociadas entre sí, lo cuál permite que se puedan enviar tramas entre sí. En este modo no está presente un Access Point.
2. ***Modo Infraestructura***: En este modo, cada cliente o dispositivo se asocia a un Access Point, donde este último se conecta a otra red (la cableada) y realiza las funciones de coordinación donde todo el tráfico de red pasa a través de él (es decir, el cliente envía y recibe sus tramas a través del Access Point). En este modo es posible conectar varios AP juntos mediante una red por cable para formar un "sistema de distribución", formando así una red 802.11 extendida.
### Router módem WiFi
El router de servicios integrados (ISR) es un dispositivo comúnmente usado en redes inalámbricas hogareñas, que permiten interconectar dispositivos varios (PC, notebooks, smartphones, etcétera) debido a que brinda las siguientes funciones:
- ***Router***: Direcciona (enruta) las solicitudes internas.
- ***Switch***: Interconecta dispositivos.
- ***Access Point***: Junta las señales en un solo lugar.
- ***Módem***: Modula y le asigna una frecuencia a cada dispositivo.
- ***Conexión a Internet***: Provista e instalada por el ISP.
- ***DHCP***: Asignación dinámica de direcciones IP.
### Arquitectura de IEEE 802.11
Esta arquitectura se compone de un sistema basada en arquitectura celular, donde usamos celdas llamadas **BSS** (**B**asic **S**ervice **S**et o Conjunto de Servicio Básicos, siendo este un conjunto de estaciones que se comunican entre ellas ya sea por modo ad-hoc o modo infraestructura) que es controlado por su propio Access Point el cual está conectado a una red troncal o DS (**D**istribution **S**ystem). A este conjunto se lo conoce como ESS (**E**xtended **S**ervice **S**et ó Conjunto de Servicio Extendido) que resulta ser la unión de todas las celdas posibles de una red. 
En esta arquitectura se reconocen los siguientes componentes:
1. Estaciones o dispositivos finales.
2. Medio inalámbrico (radio frecuencias).
3. Celda: Área geográfica en la cual una serie de dispositivos se interconectan entre sí por un medio inalámbrico.
4. Access Point: Une las redes y dispositivos funcionando como un **bridge** o puente.
5. Sistema de distribución