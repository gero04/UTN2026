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
5. Sistema de distribución (DS): Proporciona movilidad entre celdas.
6. BSS: Servicios basicos de comunicaciones.
7. ESS: Union de varios BSS.
### Servicios del Sistema de Distribucion
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
#### Servicios Extra
- El cliente se debe asociar con un AP o router inalambrico
- Se utilizan tramas de administracion para completar los procesos de:
	- Descubrir nuevos AP inalambricos
	- Autenticar con el AP
	- Asociarse al AP
- Para permitir la negociacion de estos proceso se deben configurar los parametros en el AP y luego el cliente
### Asociacion de un cliente inalambrico
Para asociarse, un cliente inalambrico y un AP deben acordar parametros especificos:
- SSID: El cliente debe conocer el nombre de la red a la cual se va a asociar
- Contraseña: Para que el cliente se autentique en el AP
- Modo de red: Estandar 802.11 que se este utilizando
- Modo de seguridad: Parametros de seguridad (WEP, WPA, WPA2, WPA3)
- Configuracion de canales: Las bandas de frecuencia en uso
### Confiabilidad en IEEE 802.11
Las redes inalambricas son ruidosas e inseguras, debido a que tienen interferencias con otros dispositivos. Al alejarnos de las celdas empezara a suceder que nuestra señal se deteriora y sufre mas interferencias. Como estrategia, es bueno bajar la tasa de transmision si se pierden demasiadas tramas y cuando veamos que se empiezan a entregar tramas exitosamente, la estacion puede aumentar la tasa de transmision. Entre mas corta sea la trama, mayor va a ser la rpobabilidad de que la trama llegue correctamente a destino. Ademas, dividir la trama en fragmentos numerados individualmente permite que