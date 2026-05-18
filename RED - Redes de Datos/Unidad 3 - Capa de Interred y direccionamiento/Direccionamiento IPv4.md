# **Direccionamiento IPv4 y Clases de Red (A, B y C)**

**Materia:** Redes de Datos  
**Resumen en una oración:** La clase se centró en la práctica fundamental del direccionamiento IPv4 utilizando clases puras (A, B y C), el cálculo de cantidades de redes y hosts disponibles mediante fórmulas binarias, y la identificación de direcciones asignables frente a las reservadas o de red/broadcast.

## **Conceptos clave**

* **Direccionamiento con Clases Puras:** Configuración inicial de redes utilizando las clases comerciales por defecto (A, B y C) sin aplicar división en subredes (subnetting). Se trabaja principalmente en formato decimal, aunque se basa en la estructura binaria de los octetos.  
* **Direcciones Asignables (o Válidas):** Son aquellas direcciones IP que se pueden configurar legalmente en la interfaz de red de un host o equipo (router, PC, switch). Pueden ser públicas o privadas.  
* **Direcciones No Asignables:** Direcciones que el sistema operativo rechazará si se intentan configurar en un host. Incluyen:  
  * **Dirección de Red:** Identifica a la red en sí. Se caracteriza por tener todos los bits de la porción de host en 0\.  
  * **Dirección de Broadcast (Difusión):** Se utiliza para enviar un paquete a todos los hosts de esa red. Se caracteriza por tener todos los bits de la porción de host en 1\.  
  * **Direcciones Reservadas:** Direcciones con propósitos especiales preasignados, como la red 127.0.0.0 (Loopback).  
* **Máscara de Subred (por defecto):** Es el parámetro que, mediante una operación lógica AND, permite a los equipos distinguir qué parte de una dirección IP corresponde a la red y qué parte corresponde al host. Los octetos de red se representan con 255 (todos los bits en 1\) y los de host con 0 (todos los bits en 0).  
* **Broadcast Universal o Global (255.255.255.255):** Una dirección especial de difusión que excede todos los rangos de clases comerciales. Se utiliza para enviar un mensaje a absolutamente todos los dispositivos alcanzables físicamente en el segmento local, típicamente usado cuando un equipo recién se conecta y necesita solicitar una IP mediante DHCP (ya que aún no conoce a qué red pertenece).

## **Desarrollo de la clase**

### **1\. Introducción al Direccionamiento IPv4**

El direccionamiento IP es la base de toda la configuración de redes y es un tema que se utilizará constantemente. En esta etapa inicial, se trabaja exclusivamente con **Clases Puras (A, B y C)**, que son las clases comerciales que se pueden configurar en los dispositivos y en internet (las clases D y E tienen otros usos específicos y no se evalúan en esta instancia práctica).  
Por ahora, los cálculos se realizan en base decimal. A partir de la próxima clase, cuando se introduzca el concepto de **Subredes (Subnetting)**, donde los octetos se "parten" a la mitad, será obligatorio trabajar y convertir los números a formato binario para hacer las particiones correctamente.

### **2\. Análisis de Clases Puras (Estructura y Fórmulas)**

Para poder identificar a qué clase pertenece una dirección IP, no hace falta analizar todo el primer byte (octeto). **Basta con mirar los primeros bits iniciales de la dirección.**

#### **Fórmulas generales utilizadas:**

* **Cantidad de Redes:** $2^n$, donde $2^n$ es la cantidad de bits de la porción de red que se pueden variar libremente (descontando los bits fijos que identifican a la clase).  
* **Cantidad de Hosts por Red:** $2^n - 2$, donde $2^n$ es la cantidad de bits de la porción de host. Se resta 2 porque dentro de cualquier red, la primera dirección (Dirección de Red) y la última dirección (Dirección de Broadcast) no son asignables a los hosts.

#### **Clase A**

* **Identificador binario:** Comienza siempre con el bit 0\.  
* **Intervalo del primer octeto:**  
  * Técnicamente va de **0 a 127**.  
  * *Aclaración válida:* También es correcto decir que va de **1 a 126**, siempre y cuando se justifique que el 0 y el 127 no se cuentan porque están reservados (por ejemplo, el 127 para Loopback). Ambas respuestas son aceptadas en un examen si están bien justificadas.  
* **Estructura:** Red.Host.Host.Host (R.H.H.H) \-\> 1 octeto de red, 3 de host.  
* **Máscara por defecto:** 255.0.0.0 (o /8).  
* **Cantidad de Redes posibles:** $2^7$. (De los 8 bits del octeto de red, 1 bit está fijo en 0, por lo que quedan 7 bits variables).  
* **Cantidad de Hosts por Red:** $2^{24} - 2$. (Se tienen 3 octetos enteros para hosts, es decir, 24 bits. Se restan las direcciones de red y broadcast).  
* *Uso:* Diseñada para muy pocas redes en el mundo, pero con una cantidad inmensa de hosts por cada red.

#### **Clase B**

* **Identificador binario:** Comienza siempre con los bits 1 0\.  
* **Intervalo del primer octeto:** De **128 a 191**.  
* **Estructura:** Red.Red.Host.Host (R.R.H.H) \-\> 2 octetos de red, 2 de host.  
* **Máscara por defecto:** 255.255.0.0 (o /16).  
* **Cantidad de Redes posibles:** $2^{14}$. (De los 16 bits de los octetos de red, los 2 primeros están fijos en 1 0, dejando 14 bits variables).  
* **Cantidad de Hosts por Red:** $2^{16}-2$. (Quedan 16 bits completos para hosts, se restan red y broadcast).  
* *Uso:* Punto intermedio. Muchas subredes disponibles con una cantidad de hosts interesante por subred.

#### **Clase C**

* **Identificador binario:** Comienza siempre con los bits 1 1 0\.  
* **Intervalo del primer octeto:** De **192 a 223**. (Dato clave: si una IP empieza con 224 o más, ya no es clase C, ni A, ni B, por lo tanto no se trabaja con ella en asignaciones estándar).  
* **Estructura:** Red.Red.Red.Host (R.R.R.H) \-\> 3 octetos de red, 1 de host.  
* **Máscara por defecto:** 255.255.255.0 (o /24).  
* **Cantidad de Redes posibles:** $2^{21}$. (De los 24 bits de red, 3 están fijos en 1 1 0, dejando 21 bits variables).  
* **Cantidad de Hosts por Red:** $2^8-2=254$ hosts asignables.  
* *Uso:* Pensado para empresas pequeñas. Muchísimas redes posibles, pero pocos hosts (254) por cada una.

### **3\. Cálculo rápido de IP válida (Ejemplo de la clase)**

La mejor forma de calcular la última IP válida (asignable) de una red sin equivocarse es:

1. Calcular la Dirección de Broadcast (poniendo toda la parte de host en 1, lo que en decimal suele ser 255).  
2. A ese último octeto, restarle 1\.

## **Ejemplos y casos mencionados**

1. **Cálculo sobre Clase C (193.45.5.79):**  
   * **Clase:** C (porque 193 está entre 192 y 223).  
   * **Dirección de Red:** 193.45.5.0 (Cuarto octeto a cero).  
   * **Primera válida:** 193.45.5.1 (Red \+ 1).  
   * **Última válida:** 193.45.5.254 (Broadcast \- 1).  
   * **Broadcast:** 193.45.5.255 (Porción de host todo a 1).  
   * **Máscara:** 255.255.255.0  
2. **Cálculo sobre Clase B (128.240.240.240):**  
   * **Clase:** B (porque 128 entra justo en el rango 128-191).  
   * **Dirección de Red:** 128.240.0.0 (Los últimos dos octetos a cero).  
   * **Broadcast:** 128.240.255.255.  
3. **Análisis de IPs extrañas (Casos trampa en exámenes):**  
   * \[Dirección con un octeto mayor a 255\]: **No es asignable**. Justificación: Excede la capacidad de un octeto de 8 bits (cuyo valor máximo es 255). Hay un valor fuera de los límites de comprensión de la máquina.  
   * 255.255.255.255: **No es asignable**. Es el Broadcast Universal. Supera cualquier intervalo de A, B o C (pertenece a un uso especial). Sirve para mandar mensajes a todo el mundo sin conocer la red local (ej. buscar servidor DHCP).  
   * 127.56.34.0: **No es asignable**. Aunque parece una red, inicia con 127, el cual está reservado para el proceso de Loopback interno.  
   * **EL CASO TRAMPA (126.56.34.0):**  
     * Cualquiera pensaría que "como termina en 0, es dirección de red y no se puede asignar".  
     * Sin embargo, hay que ver la clase primero: **Es Clase A**.  
     * En la Clase A, la porción de host son los **últimos tres octetos**.  
     * Para que sea dirección de red, TODOS los bits de la porción de host deben ser cero (debería ser 126.0.0.0).  
     * Como la IP es 126.56.34.0, la porción de host es 56.34.0. No son todos ceros. Por lo tanto, **SÍ ES UNA IP ASIGNABLE**.  
     * *Nota:* Esto cambia si aplicamos subredes (ej. un /24 a esa IP la volvería dirección de red), pero trabajando con clases puras y máscaras por defecto, es un host válido.

## **Puntos que el docente remarcó**

* **Identificar la clase es el paso CERO:** Es sumamente importante reconocer de qué clase es la dirección IP como primer paso de cualquier ejercicio.  
* **La dirección IP por sí sola no habla:** "Siempre tienen que conocer sí o sí la máscara". En esta clase se asumen las máscaras por defecto (clases puras), pero en la vida real y futuros parciales, la máscara (ej. el /24) determina todo.  
* **Justificación de intervalos:** Si en un parcial escriben la fórmula ($2^7$ o $2^{24}-2$) se tomará como correcto porque demuestra que entienden la teoría de fondo, en lugar de memorizar un número enorme (como "16 millones de hosts").  
* **Cuidado con los nervios en el parcial:** Revisar bien los octetos de las direcciones "trampa". Asegurarse de que no tengan números mayores a 255 o empiecen con 127\.

## **Para el trabajo práctico / evaluación**

* **Actividad Integrada N° 1:** Vence MAÑANA. Es un cuestionario por el laboratorio de redes. Quien no lo entregue a tiempo pierde la prueba. Tiene que estar 100% completo y es requisito para la materia.  
* **Actividad Integrada N° 2:**  
  * Consiste en una simulación de red sencilla (usando Packet Tracer u otro simulador a elección).  
  * **Requisito clave:** Grabar un video capturando la pantalla. **Debe tener audio.** No hace falta que hablen todos los miembros del grupo (pueden ser 1, 2 o 3), pero la topología debe estar explicada.  
  * **Contenido del video:** Comentar qué se hizo (ej. "Esta topología tiene 4 hosts, este switch y router"), mostrar la configuración de los equipos (todos en la misma red) y **hacer una prueba de conectividad (ping) para demostrar que funciona.**  
  * *Proyección futura:* Cada actividad integradora sumará un concepto nuevo (ej. agregar routers, configurar VLANs). En los videos futuros, se deberá hacer hincapié y demostrar que funciona *el concepto nuevo* correspondiente a esa actividad.  
  * Ya está habilitada en la UV para los grupos conformados. Hay tiempo para entregarla, no dejarse estar.

## **Dudas y cosas para revisar**

* **Subnetting (Subredes):** Quedó como introducción pendiente para la próxima clase. Implicará partir octetos a la mitad y cambiará la regla de que "una IP que termina en .0 o .255 depende de su clase pura". A partir de la próxima clase, se necesitará trabajar en binario para calcular esto.