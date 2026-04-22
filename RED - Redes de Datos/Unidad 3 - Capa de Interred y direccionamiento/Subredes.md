# **Diseño y Cálculo de Subredes (Subnetting) \- Enfoque en IPv4**

**Materia:** Redes de Computadoras
**Resumen en una oración:** La clase profundiza en el diseño de subredes para optimizar topologías de red, enseñando a calcular máscaras, rangos de IPs válidas y direcciones de broadcast mediante el préstamo de bits (de host a red), con ejemplos prácticos paso a paso en redes Clase A y B.

## **Conceptos clave**

* **Dominio de Colisión y Broadcast:** Es el alcance lógico donde los paquetes de broadcast (mensajes dirigidos a todos los dispositivos) son propagados. Los switches extienden el dominio de broadcast, lo que puede congestionar la red. Los routers, en cambio, dividen estos dominios, haciendo obligatoria la creación de subredes.  
* **Subnetting (Creación de subredes):** Es el proceso de tomar una red principal (Clase A, B o C) y dividirla en redes más pequeñas lógicas. Se logra "pidiendo prestados" bits que originalmente estaban destinados a identificar *hosts* para usarlos como identificadores de *subred*.  
* **Dirección de Red / Subred:** Es la primera dirección de un rango, donde todos los bits de la porción de host están en 0\. **Nunca** se le puede asignar a un host. Sirve para que los routers identifiquen la red.  
* **Dirección de Broadcast:** Es la última dirección de un rango, donde todos los bits de la porción de host están en 1\. Se usa para enviar mensajes a todos los equipos de esa subred. **Tampoco** se le asigna a un host.  
* **IP Válida:** Cualquier dirección IP que se encuentre entre la dirección de red y la de broadcast. Son las únicas que se pueden asignar a las interfaces físicas (computadoras, impresoras, interfaces de routers).  
* **Máscara de Subred:** Es un valor que define qué parte de una dirección IP corresponde a la red y qué parte a los hosts. Al pedir bits prestados para subredes, estos bits se transforman en 1 dentro de la máscara.  
* **Gateway (Puerta de enlace):** Es la IP de la interfaz del router que conecta una subred (LAN) con el exterior u otras redes. Por convención, se le suele asignar la primera o la última dirección IP válida de esa subred.

## **Desarrollo de la clase**

### **1\. El problema de la topología plana y la necesidad de Subredes**

El docente comenzó recordando por qué es necesario dividir redes. Si en una empresa se agregan constantemente computadoras usando únicamente switches (sin routers), el dominio de broadcast se vuelve gigante.  
Protocolos como DHCP u otros procesos de control generan tráfico que se envía a *todos* los dispositivos conectados. A mayor cantidad de dispositivos, más paquetes "basura" circulan, lo que agota los recursos de los switches y degrada drásticamente el rendimiento general de la red (se congestiona).  
Para solucionar esto, se introducen routers que no dejan pasar el broadcast. Al dividir la topología física con routers, obligatoriamente hay que dividir el espacio de direcciones IP lógicas creando subredes.

### **2\. Cálculos fundamentales de Subredes**

Dada una dirección base (según su clase), el proceso implica decidir cuántos bits pedir prestados de la parte de host.

* **Cálculo de Subredes:** Se calcula como $2^n$, donde *n* es la cantidad de bits prestados. (No se resta nada porque se usan todas las combinaciones).  
* **Cálculo de Hosts por subred:** Se calcula como $2^h - 2$, donde *h* es la cantidad de bits que *quedaron* para los hosts. Se restan 2 porque la primera combinación de ceros es la dirección de subred y la última (todos unos) es el broadcast.  
* **Relación inversamente proporcional:** Mientras más bits pido para crear más subredes, menos bits me quedan para hosts (las redes son más chicas).

### **3\. La Máscara de Subred en el diseño**

Al alterar la estructura clásica (A, B o C), la máscara también cambia. Los bits que se piden prestados pasan a valer 1 en la máscara.  
Por ejemplo, en una **Clase B (/16)** clásica la máscara es 255.255.0.0. Si pedimos prestados **3 bits** del tercer octeto:

* En binario, esos 3 bits prendidos son 11100000\.  
* Su equivalente decimal es 128 \+ 64 \+ 32 \= **224**.  
* La nueva máscara (para todas las subredes de este diseño) será 255.255.224.0 (Prefijo /19).

**Regla de oro de configuración:** En una misma LAN, las máquinas deben tener una **IP distinta**, pero obligatoriamente deben compartir **la misma Máscara** y el **mismo Gateway**.

### **4\. Metodología para obtener el Rango de IPs**

El diseño de subredes requiere pensar sí o sí en binario y escribirlo en papel.

1. **Fijar la red:** De acuerdo a la clase original (A, B o C), hay octetos que no se pueden tocar.  
2. **Identificar el préstamo:** Marcar claramente cuáles son los bits que se pidieron para identificar subredes y cuáles quedan para hosts.  
3. **Calcular la Subred:** Poner todos los bits de la parte de subred en la combinación deseada y todos los bits de host en 0\.  
4. **Primera IP válida:** Es la dirección de subred \+ 1 (en el último bit).  
5. **Broadcast:** Poner toda la porción de host (todos los bits que sobraron) en 1\.  
6. **Última IP válida:** Es el Broadcast \- 1\.

## **Ejemplos y casos mencionados**

### **Analogía del Broadcast en el aula**

Para explicar la congestión por broadcast, el docente usó un ejemplo físico: "Si yo hablo solo, estoy generando un broadcast y me escuchan. ¿Pero qué pasa si les digo que hablen 10 de ustedes al mismo tiempo? ¿Y si sumamos 10 más? Empieza a hacerse un despelote, no entendemos nada". En las redes sucede exactamente igual.

### **Ejemplo 1: Clase B prestando 8 bits**

* **Red base:** 180.5.0.0 /16  
* **Préstamo:** 8 bits (todo el 3er octeto).  
* **Subredes generadas:** $2^8 = 256$ subredes.  
* **Hosts por subred:** $2^8 - 2 = 254$ hosts válidos.

### **Ejemplo 2: Clase B prestando 4 bits (Prefijo /20)**

* **Red base:** 180.5.0.0 /16  
* **Préstamo:** 4 bits del tercer octeto. Subredes generadas: $2^4 = 16$.  
* **Máscara:** 255.255.240.0 (11110000 \= 128+64+32+16 \= 240).  
* **Saltos:** Los bits cambian en el valor del bit prestado de menor peso (en este caso, 16). Las subredes van saltando de a 16: 180.5.0.0, 180.5.16.0, 180.5.32.0, 180.5.48.0...  
* **Análisis de la Subred 2 (la .32.0):**  
  * Subred: 180.5.32.0  
  * Primera válida: 180.5.32.1  
  * Última válida: 180.5.47.254 (Ya que la siguiente subred es la 48.0)  
  * Broadcast: 180.5.47.255

### **Ejemplo 3: El "Caso Florencia" (Ingeniería Inversa desde una IP)**

Se analizó la IP de una alumna: 10.16.4.112 con máscara 255.255.224.0.

1. **Identificar clase original:** Es 10.x.x.x, por lo tanto es **Clase A (/8)**. Fijo el primer octeto (10).  
2. **Identificar la máscara en bits:** 255.255.224.0 significa:  
   * 1er octeto: 8 bits (originales de red).  
   * 2do octeto: 8 bits prestados (255).  
   * 3er octeto: 3 bits prestados (224 es 11100000).  
   * **Prefijo total:** 8 \+ 8 \+ 3 \= **/19**.  
   * **Total bits prestados:** 11 bits (8 del segundo \+ 3 del tercero).  
3. **Identificar a qué subred pertenece:** Para que el tercer octeto sea 4, en la porción de subred los bits deben estar apagados, por lo tanto la subred de esta IP es la **10.16.0.0**.  
4. **Calcular el rango válido de la subred 10.16.0.0:**  
   * Primera válida: 10.16.0.1  
   * Broadcast: Se ponen los 13 bits de host en 1\. En el tercer octeto sobran 5 bits de host (00011111 \= 31). En el cuarto octeto son 8 bits (11111111 \= 255). Por ende, Broadcast \= 10.16.31.255.  
   * Última válida: 10.16.31.254

### **Ejemplo 4: Cálculo de la subred número 10**

* **Red base:** 140.9.0.0 /16 (Clase B). Se requiere usar prefijo **/26**.  
* **Préstamo:** De /16 a /26 son **10 bits prestados** (8 del 3er octeto y 2 del 4to octeto).  
* **Máscara:** 255.255.255.192 (El cuarto octeto usa 2 bits: 128+64=192).  
* **Cálculo de la subred 10:** El docente enseñó a contar en binario iterando los últimos dos bits prestados hasta llegar a la posición 10\.  
  * Resultado: Subred 140.9.2.128  
  * Rango válido: 140.9.2.129 hasta 140.9.2.190  
  * Broadcast: 140.9.2.191

## **Puntos que el docente remarcó (¡Muy Importante\!)**

1. **Pensar en binario y escribirlo:** El docente insistió muchísimo: *"Esto lo tienen que escribir a tinta. Es la única forma de no perderse. Hay que pensarlo en binario, nada más"*. Tratar de calcular todo mentalmente en decimal lleva a confusiones.  
2. **Dejar margen de crecimiento:** Como diseñadores, no deben ser "tacaños". Si les piden diseñar para 50 subredes, dejen un 30% a 35% de margen y diseñen pensando en que necesitarán 65 subredes. Si les piden 150 hosts, diseñen para 180 o 200, porque "siempre hay un puesto de trabajo más".  
3. **Conocer las clases:** "Si no saben lo que es la parte de red y la parte de host de una dirección clase A, B o C, se van a confundir en lo que es subred. Saber la clase dice qué octetos van fijos y no se pueden tocar".  
4. **Regla de Gateways y Máscaras:** La máscara la saco una vez al inicio del diseño y *es la misma para todos los hosts* de esa subred. El gateway suele ser la IP .1 (la primera de las válidas).  
5. **Dada la subred, NO se pone la IP:** Una dirección de red o broadcast jamás se usa para configurar la interfaz de un equipo.

## **Para el trabajo práctico / evaluación**

* **Resolver problemas de conectividad en Topología:**  
  * *Caso Máquina C:* No tiene conectividad porque **no pertenece a la misma subred que su gateway**. Al calcular el rango válido de su LAN, su IP quedó fuera de los límites numéricos de esa subred.  
  * *Caso Máquina D:* No puede salir de su red (LAN 2\) porque **tiene mal configurado el Gateway**. La topología exigía una IP específica para la salida (ej: 33.1) y la máquina tenía cargada una errónea (ej: 32.1).  
* **Conceptos fijos para el parcial:** Asegurarse de tener claridad absoluta en distinguir dirección IP vs Dirección de Red vs Máscara.  
* Quedan pendientes los ejercicios subidos de la presentación (PDFs de la clase de ayer y hoy).

## **Dudas y cosas para revisar**

* **Paso de Binario a Decimal en el Broadcast:** Durante el "Caso Florencia", a los alumnos les costó entender de dónde salía el número 31 en el tercer octeto para el Broadcast (10.16.31.255).  
  * *Explicación para revisar:* En un /19, sobran 5 bits de host en el 3er octeto. Para calcular el broadcast, estos 5 bits se ponen a 1\. En binario 00011111 equivale a 16+8+4+2+1 \= **31**. Conviene repasar las sumas de las potencias de base 2 (128, 64, 32, 16, 8, 4, 2, 1).  
* **El salto entre octetos:** Hubo confusión al avanzar subredes combinando los bits prestados que caen en dos octetos distintos (Ejemplo 4, prestando 10 bits). Hay que repasar cómo cuando se agotan las combinaciones en el cuarto octeto (00, 01, 10, 11), se suma un 1 en el tercer octeto para continuar la secuencia.