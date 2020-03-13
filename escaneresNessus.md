###### tags: `auditoría` `nessus`

# Tipos de escáners en Nessus
## V. 8.9.1

### *Descubrimiento*



#### Descubrimiento de host ![](https://i.imgur.com/ULshpmj.jpg)
Realiza un escaneo simple para descubrir hosts en vivo y puertos abiertos.



---


---


### *Vulnerabilidades*

#### Escaneo de red básico ![](https://i.imgur.com/fBiGoQF.jpg)
Realiza una exploración completa del sistema que es adecuada para cualquier host. Por ejemplo, podría usar esta plantilla para realizar un análisis de vulnerabilidad interna en los sistemas de su organización.


---


#### Escaneo avanzado ![](https://i.imgur.com/7f5BawK.jpg)
Escaneos sin ninguna recomendación.


---


#### Escaneo dinámico avanzado ![](https://i.imgur.com/nOfSBjl.jpg)
Una exploración avanzada sin ninguna recomendación, donde puede configurar un filtro de complemento dinámico en lugar de seleccionar manualmente familias de complementos o complementos individuales. A medida que Tenable lanza nuevos complementos o cambios en los atributos de los complementos, el escaneo incluye o excluye dinámicamente complementos dependiendo de su filtro. Esto le permite personalizar sus escaneos para vulnerabilidades específicas al tiempo que garantiza que el escaneo se mantenga actualizado a medida que se lanzan nuevos complementos. Consulte Configurar complementos dinámicos .


---



#### Escaneo de malware![](https://i.imgur.com/CU21sms.jpg)
Analiza en busca de malware en sistemas Windows y Unix.
Video: auditorías de aplicaciones, malware y contenido
https://dmigcwbhclqpw.cloudfront.net/nessus/ODT-NES-ACOM/app_malware_l/index.html
Video: aplicación, software malicioso y auditorías de contenido
https://dmigcwbhclqpw.cloudfront.net/nessus/ODT-NES-ACOM/app_malware_d/index.html


---

#### Escaneo de dispositivo móvil ![](https://i.imgur.com/s8d5kf0.jpg)
Evalúa dispositivos móviles a través de Microsoft Exchange o un MDM.


---

##### Pruebas de aplicaciones web ![](https://i.imgur.com/5KrbCrM.jpg)
Analice vulnerabilidades web publicadas y desconocidas.


---

#### Auditoría de parches acreditados ![](https://i.imgur.com/LwChTay.jpg)
Autentica hosts y enumera las actualizaciones que faltan.


---

#### Detección de Badlock ![](https://i.imgur.com/1zWi0B6.jpg)
Realiza controles remotos y locales para CVE-2016-2118 (Samba) y CVE-2016-0128 (Microsoft).
Es una vulnerabilidad de elevación de privilegios. Según el Boletín de Microsoft, la vulnerabilidad es "causada por la forma en que los protocolos remotos SAM y LSAD establecen el canal de Llamada a procedimiento remoto (RPC)". La vulnerabilidad está en la forma en que el protocolo SAMR maneja los niveles de autenticación.

Un factor clave en la explotación de esta vulnerabilidad es la necesidad de que el atacante realice primero un ataque de hombre en el medio (MitM) para interceptar cualquier tráfico DCERPC entre un cliente y un servidor, para hacerse pasar por el cliente y obtener los mismos privilegios que la cuenta de usuario autenticada. Esto es más problemático contra los controladores de dominio de directorio activo. Esto implica que el atacante debe tener un conocimiento razonable de la red de destino. No es tan simple como descargar herramientas de explotación de Internet y disparar un exploit.

Además, tenga en cuenta que después de un ataque exitoso, el atacante obtendría la elevación de privilegios. Con estos privilegios elevados, el atacante podría obtener acceso de lectura y escritura a la base de datos SAM, que se puede utilizar para forzar las contraseñas por fuerza bruta (obtención de hashes).
Con estas credenciales, un atacante puede suplantar a otro usuario.

---

#### Bash Shellshock Detection ![](https://i.imgur.com/gC8mShP.jpg)
Realiza controles remotos y locales para CVE-2014-6271 y CVE-2014-7169. 
CVE-2014-7169 Detalle: GNU Bash a través de 4.3 bash43-025 procesa cadenas finales después de ciertas definiciones de funciones malformadas en los valores de las variables de entorno, lo que permite a los atacantes remotos escribir en archivos o posiblemente tener otro impacto desconocido a través de un entorno diseñado, como lo demuestran los vectores que involucran la función ForceCommand en OpenSSH sshd, los módulos mod_cgi y mod_cgid en el Servidor Apache HTTP, scripts ejecutados por clientes DHCP no especificados y otras situaciones en las que la configuración del entorno ocurre a través de un límite de privilegios desde la ejecución de Bash. NOTA: esta vulnerabilidad existe debido a una solución incompleta para CVE-2014-6271.


---

##### Detección de DROWN ![](https://i.imgur.com/Re2K1n6.jpg)
Realiza comprobaciones remotas para CVE-2016-0800. Vulnerabilidad descubierta en 2016.
DROWN: Decrypting RSA with Obsolete and Weakened eNcryption (descifrado de RSA con un cifrado obsoleto y debilitado). Es una seria vulnerabilidad que afecta a HTTPS y a otros servicios que confían su cifrado en SSL y TLS, elementos esenciales para el cifrado de datos en Internet.
DROWN puede descifrar las sesiones TLS, aunque este último protocolo no está afectado. Para poder ser explotado se necesita que el soporte de TLS esté acompañado del viejo y vulnerable SSLv2, que tiene que estar marcado como Export para poner DROWN en marcha.
![](https://i.imgur.com/6HnQIIZ.png)

La imagen de arriba describe bastante bien cómo un atacante puede explotar DROWN. Mientras que el cliente realiza una conexión TLS supuestamente segura, el hacker aprovecha el soporte de SSLv2 del servidor para realizar el ataque y descifrar las conexiones TLS, a través del cual puede obtener todo tipo de datos que el cliente envíe al servidor, o sea, nombres de usuario, contraseñas, números de tarjetas de crédito, domicilio postal, etc. También hay otra posibilidad, y es que este grave fallo de seguridad permite a un atacante poder suplantar una web bajo HTTPS, pudiendo aprovecharse de la inocencia del usuario y obtener todos los datos que este le suministre a través de la web falsificada. **Para explotar DROWN el atacante no lanza el ataque sobre la conexión o el cliente, sino sobre el servidor que utiliza el cifrado SSLv2.**

**Cómo proteger un servidor de DROWN**
Según el software de cifrado empleado, las medidas a tomar son diferentes. Mencionaremos algunos de los más importantes y enlazaremos a otros que pueden ser interés.

* OpenSSL: En la librería criptografía más mediática lo que hay que hacer es actualizar a las versiones 1.0.2g y 1.0.1g si las usadas son 1.0.2 y 1.0.1 respectivamente o bien cualquier otra versión anterior a esas dos.
* Microsoft IIS (Windows Server): IIS 7.0 o superior tiene SSLv2 desactivado por defecto, aunque se puede activar manualmente. IIS 7.0 ya no está soportado por Microsoft, y desde el sitio web del ataque DROWN se recomienda actualizarlo en caso de ser la versión en uso y luego comprobar si las claves han sido expuestas a través de su formulario.
* Network Security Services (NSS): Otra librería de criptografía bastante común empleada por muchos servidores. A partir de la versión 3.13 SSLv2 está desactivado por defecto, aunque puede ser activado manualmente. Se recomienda a los usuarios actualizar a una versión más reciente de esta biblioteca.
* El sitio web del ataque también ofrece instrucciones para Apache, Postfix y Nginx. En cualquier caso siempre se puede emplear su formulario para comprobar que la clave privada no haya sido expuesta.
* Lo más sencillo sería desactivar el soporte para SSLv2. De hecho muchos servidores y librerías de criptografía ya lo tienen desactivado por defecto. Sin embargo todavía existe una cantidad importante de clientes que utilizan ese cifrado obsoleto, por lo que muchos administradores se ven obligados a activarlo para conseguir que su sitio web sea visitado o su servicio utilizado.

---

#### Intel AMT Security Bypass ![](https://i.imgur.com/9KnpmfB.jpg)
Realiza controles remotos y locales para CVE-2017-5689. Vulnerabilidad descubierta en 2017.
Se trata de un fallo en la tecnología ‘Active Management Technology’ (AMT), presente en equipos portátiles de gama corporativa. AMT es un acceso de administración remoto utilizado para administrar, mantener e inventariar el parqué de equipos de gama empresarial. Está presente en sistemas Intel vPro y en algunas estaciones de trabajo con procesadores de la familia Xeon.

Descubierto por la empresa finlandesa F-Secure en julio de 2017, la vulnerabilidad es más bien un fallo de configuración de fábrica de las credenciales de administración. Permite no solo el acceso administrativo al propio AMT, sino evitar además toda medida de seguridad adicional implementadas en el equipo (contraseñas de BIOS, sistema operativo, cifrado de disco), obteniendo acceso privilegiado al sistema de forma remota.

Explotación: Al iniciar estos equipos de forma local, es posible acceder a la extensión para la BIOS de AMT antes de que cualquier credencial sea requerida (incluida la contraseña de BIOS). Una vez el sistema lo requiera, un usuario malintencionado puede acceder simplemente introduciendo la contraseña por defecto: *admin*.
A partir de aquí, se puede configurar el acceso remoto a través de AMT, desactivar el consentimiento del usuario y empezar a gestionar el sistema a través de VNC (software de pantalla compartida que permite establecer una conexión con un equipo remoto ) . Aunque por defecto está limitado a accesos desde la misma red cableada, se puede configurar la opción de hacerlo a través de la misma red Wi-Fi o incluso dirigir al usuario hacia un servidor externo controlado por el atacante, usando para ello ‘Client Initiated Remote Access’ o CIRA.

A través de este acceso privilegiado, el atacante podrá leer y escribir cualquier fichero al que el usuario tenga acceso, además de ejecutar cualquier programa en su equipo.


---

#### Escaneo de Shadow Brokers ![](https://i.imgur.com/rxDJVA1.jpg)
Analiza las vulnerabilidades reveladas en las filtraciones de Shadow Brokers.
+ info: https://blogs.protegerse.com/2017/04/18/shadow-brokers-filtra-mas-herramientas-de-la-nsa-o-como-pasar-entretenido-la-semana-santa/
+ ej. de explotacion: https://www.hacking4badpentesters.com/2017/04/step-by-step-eternalblue-doublepulsar.html


---

#### Spectre y Meltdown ![](https://i.imgur.com/pBDvVAC.jpg)
Realiza controles remotos y locales para CVE-2017-5753, CVE-2017-5715 y CVE-2017-5754.
Meltdown y Spectre explotan vulnerabilidades críticas en procesadores modernos . Estas vulnerabilidades de hardware permiten que los programas roben datos que actualmente se procesan en la computadora. Si bien los programas normalmente no pueden leer datos de otros programas, un programa malicioso puede explotar Meltdown y Spectre para obtener secretos almacenados en la memoria de otros programas en ejecución. Esto puede incluir sus contraseñas almacenadas en un administrador de contraseñas o navegador, sus fotos personales, correos electrónicos, mensajes instantáneos e incluso documentos críticos para el negocio.

Meltdown y Spectre funcionan en computadoras personales, dispositivos móviles y en la nube. Dependiendo de la infraestructura del proveedor de la nube, podría ser posible robar datos de otros clientes.

**Meltdown** rompe el aislamiento más fundamental entre las aplicaciones del usuario y el sistema operativo. Este ataque permite que un programa acceda a la memoria y, por lo tanto, también a los secretos de otros programas y del sistema operativo.

Si su computadora tiene un procesador vulnerable y ejecuta un sistema operativo sin parches, no es seguro trabajar con información confidencial sin la posibilidad de filtrar la información. Esto se aplica tanto a las computadoras personales como a la infraestructura de la nube. Afortunadamente, hay parches de software contra Meltdown: para Linux: https://lwn.net/Articles/738975/

**Specter** rompe el aislamiento entre diferentes aplicaciones. Permite a un atacante engañar a los programas libres de errores, que siguen las mejores prácticas, para que filtren sus secretos. De hecho, los controles de seguridad de dichas mejores prácticas en realidad aumentan la superficie de ataque y pueden hacer que las aplicaciones sean más susceptibles a Spectre

El Spectre es más difícil de explotar que Meltdown, pero también es más difícil de mitigar. Sin embargo, es posible prevenir exploits conocidos específicos basados en Spectre a través de parches de software. https://devblogs.microsoft.com/cppblog/spectre-mitigations-in-msvc/

---

#### WannaCry Ransomware ![](https://i.imgur.com/rpbvf2o.jpg)
Busca el ransomware WannaCry.

*Info*: Los ataques ransomware normalmente infectan una computadora cuándo un usuario abre un email phishing y, a pesar de que presuntamente emails de esta clase serían los causantes de la infección WannaCry, este método de ataque no ha sido confirmado.19 Una vez instalado, WannaCry utiliza el exploit conocido como EternalBlue, desarrollado por la Agencia de Seguridad Nacional de los Estados Unidos (NSA), para extenderse a través de redes locales y anfitriones remotos que no hayan recibido la actualización de seguridad más reciente, y de esta manera infecta directamente cualquier sistema expuesto. Un “parche” crítico habría sido emitido por Microsoft el 14 de marzo de 2017 para eliminar la vulnerabilidad subyacente para sistemas soportados por Microsoft en la actualidad, lo cual se dio casi dos meses antes del ataque, sin embargo, muchas organizaciones no llegaron a aplicarlas.
Cuándo es ejecutado, el malware primero verifica el "botón de apagado" el cual corresponde a un nombre de dominio específico. Si este no es encontrado, entonces el ransomware encripta los datos del ordenador, y procede a tratar de usar el exploit SMB para extenderse a ordenadores aleatorios en el Internet, y "lateralmente" a ordenadores en la misma red. Como otras variaciones de ransomware, el *payload* (carga útil) encuentra y ubica una variedad de archivos, para luego notificar al usuario que los archivos han sido encriptados, reclamando un pago de en bitcoin.


---



---


### *Conformidad*

#### Auditoría de la infraestructura de la nube ![](https://i.imgur.com/82jwIZf.jpg)
Audita la configuración de servicios en la nube de terceros.

#### Escaneo interno de red PCI ![](https://i.imgur.com/2YjZUBM.jpg)
Realiza un análisis interno de vulnerabilidades PCI DSS (11.2.1).
Para obtener más información, consulte Análisis de validación de PCI ASV no oficial .

##### Auditoría de configuración de MDM ![](https://i.imgur.com/FD8kq2J.jpg)
Audita la configuración de los administradores de dispositivos móviles.

#### Auditoría de configuración sin conexión ![](https://i.imgur.com/kcTYhJX.jpg)
Audita la configuración de dispositivos de red.

#### Escaneo externo trimestral PCI ![](https://i.imgur.com/SQ8eHHe.jpg)
Realiza exploraciones externas trimestrales según lo requiera PCI (no validada, para ser válidarequieere un escaneo dese servidores de EEUU)

PCI DSS detalla los requisitos de seguridad para los comerciantes y proveedores de servicios que almacenan, procesan o transmiten datos de titulares de tarjetas. Para demostrar el cumplimiento de la norma PCI DSS, comercios y proveedores de servicios están obligados a llevar cabo Análisis de Vulnerabilidades trimestrales, de conformidad con el Requisito 11.2 de PCI DSS.

Según los requerimientos planteados por PCI DSS, los Escaneos Trimestrales de Vulnerabilidades externos han de ser realizados por una empresa homologada como ASV (Approved Scanning Vendor) de forma externa sobre todos los Componentes del Entorno de Cumplimiento accesibles desde Internet.

La solución PCI ASV de Tenable, un "work bench" de Tenable.io, aprovecha el escaneo de Tenable.io Vulnerability Management para optimizar el proceso de ASV.

En el contexto de PCI DSS, los "Componentes del Entorno" que deberán estar incluidos en los escaneos trimestrales incluyen cualquier componente de red, servidor o aplicación que se incluye en o conectado al entorno de datos de titulares de tarjetas. También incluye cualquier componente de virtualización tales como máquinas virtuales, switches virtuales / routers, dispositivos virtuales, aplicaciones virtuales / equipos de escritorio y los hipervisores. 
> Los componentes de red incluyen, pero no están limitados a: firewalls, switches, routers, puntos de acceso inalámbricos, dispositivos de red y otros dispositivos de seguridad. Los tipos de servidores incluyen, pero no se limitan a los siguiente: web, aplicación, base de datos, autenticación, correo, proxy, protocolo de tiempo de red (NTP) y el Sistema de Nombres de Dominio (DNS). Las aplicaciones incluyen y aplicaciones personalizadas o adquiridas a terceros, incluyendo aplicaciones alojadas en sistemas internos y externos. 

Por lo tanto la información que deberá facilitar para realizar el escaneo deberá incluir las *direcciones IP visibles o accesibles desde Internet, dominios y las URLs de aplicaciones "ocultas" o no accesibles directamente.*

**Visibilidad continua del estado**
Después de enviar un escaneo a Tenable para la revisión de ASV,
podrá ver el progreso actualizado de la solicitud de autenticación.
Cada *controversia* se indica como *no evaluada*, *evaluada*,
*aprobada*, *no aprobada* y *se necesita información adicional*.
Si se necesita información adicional, se le notificará por correo
electrónico. Cuando se hayan aprobado todas las controversias,
la solicitud del ASV se indicará como aprobada.

### Preguntas y situaciones:
#### 1. Colocar en la lista blanca o no en la lista blanca - Esa es la cuestión
Los objetivos externos de una entidad pueden ser alcanzados a partir de IPs de fuente pública. En algunos casos desde cualquier IP , pero la mayoría de las veces desde direcciones IP específicas. Si ese es el caso, el escaneo ASV podría resultar en: Escaneo ASV FALLO (por ejemplo, debido a interferencias de escaneo), escaneo ASV incompleto (por ejemplo, debido a que se detecta que el host no está vivo), etc.

##### 2. Entonces, ¿debería la entidad escaneada incluir en la lista blanca las IPs del escáner ASV?

La respuesta no es sólo un sí o un no.
Los escáneres ASV deben poder realizar la exploración sin interferencias de los "sistemas de protección activa". "Activo" se refiere a los sistemas de seguridad que modifican dinámicamente su comportamiento basándose en la información recopilada a partir de patrones de tráfico de la red que no son de ataque. Estos sistemas incluyen IPS, WAF, QoS, e incluso Firewalls que bloquean las direcciones IP al detectar un análisis de puertos (no reglas estáticas).

#### 3. ¿Qué pasa con los cortafuegos y sus reglas estáticas?
En general, las reglas estáticas de los dispositivos de red no necesitan ser cambiadas para realizar un escaneo ASV de manera compatible con PCI DSS.

Si persisten los problemas de 'host not alive’ o 'scan interference’ (host no se encuentra vivo e interferencia de escaneo) después de de incluir en la lista blanca de las IPs las del escáner ASV en los sistemas de protección activa, tranquilos existe una solución. A continuación, la configuración del análisis ASV y de los dispositivos se puede realizar de forma que el host se encuentre vivo y sin interferencias. Esto generalmente se puede hacer con una configuración temporal de escaneo/dispositivo, que incluye:

Personalice la detección de TCP
Personalice la detección de UDP
Habilitar ICMP
Cambiar el comportamiento de "closed port" del cortafuegos de drop a reject
Si lo anterior no es posible, existe otra opción: El cliente de ASV tiene que proporcionar la evidencia apropiada para apoyar su afirmación de que el escaneo no fue bloqueado activamente. Y si el ASV está de acuerdo en que el escaneo no fue bloqueado activamente, puede determinar que no es necesario un escaneo adicional. Esto significa que debe incluir soporte ASV (probablemente cada trimestre).

#### 4. Escaneos ASV trimestrales y escaneos de remediación - Cuándo y por qué
Es importante entender lo que se define como un trimestre. Por definición, un trimestre se refiere a la división de un año en cuatro partes iguales. Por lo tanto, los siguientes son todos los trimestres válidos de exploración ASV en un período de 12 meses:

 
>  Ciclo 1:
> De enero a marzo
> De abril a junio
> De julio a septiembre
> De octubre a diciembre
 
>  Ciclo 2:
> De febrero a abril
> De mayo a julio
> De agosto a octubre
> De noviembre a enero (siguiente año)
 
>  Ciclo 3:
> De marzo a mayo
> De junio a agosto
> De septiembre a noviembre
> De diciembre a febrero (siguiente año)
> El primer trimestre es el trimestre en el que una entidad realiza el primer análisis ASV.

Una entidad que cumple con el PCI DSS tiene que obtener **4 escaneos PASS ASV trimestralmente**. Esto significa que si el análisis ASV da como resultado un FALLO, tendrá que realizar el análisis ASV de corrección correspondiente en el mismo cuarto del análisis ASV fallido hasta que se realice un análisis con resultado satisfactorio.

Vamos a ver un ejemplo: Considere que tenemos los siguientes trimestres:
![](https://i.imgur.com/s5TDacC.png)


El trimestre actual de la exploración ASV está en rojo (julio-septiembre) y:

Realizamos el primer escaneo trimestral (primer círculo negro-rojo) y resulta en PCI FALLO.
Luego realizamos un escaneo de remediación (segundo círculo negro-rojo) y de nuevo resulta en un FALLO.
Si corregimos las vulnerabilidades descubiertas, se pueden observar los dos casos siguientes: 
Realizamos el escaneo de remediación de nuevo en septiembre (tercer círculo negro-verde). Este análisis de corrección es válido para el trimestre ROJO como análisis PCI PASS ASV.
Realizamos el escaneo de remediación de nuevo en octubre (cuarto círculo rojo-verde). Este análisis de corrección NO es válido para el trimestre ROJO, lo que deja un trimestre sin un análisis PASS ASV, y se puede encontrar que la entidad no es compatible con PCI DSS.
Alcanzando el cumplimiento de PCI DSS
Para cualquier entidad que desee convertirse o mantener su conformidad y certificación PCI DSS, es importante que comprenda los estándares, directrices y mejores prácticas de PCI DSS. Esto se suma a la comprensión de cada uno de los estándares de la industria y sus mejores prácticas. Sin embargo, esto no será suficiente. La experiencia adquirida en el encuentro y resolución de problemas es invaluable. Describe cada paso que una entidad tiene que realizar para alcanzar el cumplimiento de PCI DSS.

Proveedores de AVS: 
- Advantio ha sido reconocido por VISA como el segundo proveedor de QSA más grande de Europa. Las certificaciones de nuestro equipo de seguridad incluyen PCI QSA, PA DSS, ISO/IEC 27001 Lead Auditor, CISSP, CISA, CISM, OSSTMM y CSSLP. Nuestros expertos en PCI DSS están siempre al día cuando se trata de las nuevas versiones de los estándares PCI DSS.
- tenable.io

##### Auditoría de cumplimiento de políticas ![](https://i.imgur.com/4PyDoXR.jpg)
Audita las configuraciones del sistema contra una línea base conocida.

#### SCAP y Auditoría OVAL ![](https://i.imgur.com/Ywt7pgc.jpg)
Auditoría de sistemas utilizando definiciones SCAP y OVAL.




---


Cuadro rápido:


| Modelo                                     | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Descubrimiento**                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Descubrimiento de host                      | Realiza un escaneo simple para descubrir hosts en vivo y puertos abiertos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Vulnerabilidades**                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Escaneo dinámico avanzado                  | Una exploración avanzada sin ninguna recomendación, donde puede configurar un filtro de complemento dinámico en lugar de seleccionar manualmente familias de complementos o complementos individuales. A medida que Tenable lanza nuevos complementos o cambios en los atributos de los complementos, el escaneo incluye o excluye dinámicamente complementos dependiendo de su filtro. Esto le permite personalizar sus escaneos para vulnerabilidades específicas al tiempo que garantiza que el escaneo se mantenga actualizado a medida que se lanzan nuevos complementos. Consulte Configurar complementos dinámicos . |
| Escaneo avanzado                           | Escaneos sin ninguna recomendación.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Escaneo de red básico                      | Realiza una exploración completa del sistema que es adecuada para cualquier host. Por ejemplo, podría usar esta plantilla para realizar un análisis de vulnerabilidad interna en los sistemas de su organización.                                                                                                                                                                                                                                                                                                                                                                                                           |
| Detección de Badlock                       | Realiza controles remotos y locales para CVE-2016-2118 y CVE-2016-0128.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Bash Shellshock Detection                  | Realiza controles remotos y locales para CVE-2014-6271 y CVE-2014-7169.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Auditoría de parches acreditados           | Autentica hosts y enumera las actualizaciones que faltan.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Detección de DROWN                         | Realiza comprobaciones remotas para CVE-2016-0800.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Intel AMT Security Bypass                  | Realiza controles remotos y locales para CVE-2017-5689.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Escaneo de malware                         | Analiza en busca de malware en sistemas Windows y Unix.Video: auditorías de aplicaciones, malware y contenidoVideo: aplicación, software malicioso y auditorías de contenido                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Escaneo de dispositivo móvil               | Evalúa dispositivos móviles a través de Microsoft Exchange o un MDM.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Escaneo de corredores de las sombras       | Analiza las vulnerabilidades reveladas en las filtraciones de Shadow Brokers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Espectro y deshielo                        | Realiza controles remotos y locales para CVE-2017-5753, CVE-2017-5715 y CVE-2017-5754.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| WannaCry Ransomware                        | Busca el ransomware WannaCry.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Pruebas de aplicaciones web                | Analice vulnerabilidades web publicadas y desconocidas.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| **Conformidad**                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Auditoría de la infraestructura de la nube | Audita la configuración de servicios en la nube de terceros.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Escaneo interno de red PCI                 | Realiza un análisis interno de vulnerabilidades PCI DSS (11.2.1).Para obtener más información, consulte Análisis de validación de PCI ASV no oficial .                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Auditoría de configuración de MDM          | Audita la configuración de los administradores de dispositivos móviles.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Auditoría de configuración sin conexión    | Audita la configuración de dispositivos de red.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Escaneo externo trimestral PCI             | Realiza exploraciones externas trimestrales según lo requiera PCI.Para obtener más información, consulte Análisis de validación de PCI ASV no oficial .                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Auditoría de cumplimiento de políticas     | Audita las configuraciones del sistema contra una línea base conocida.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| SCAP y Auditoría OVAL                      | Auditoría de sistemas utilizando definiciones SCAP y OVAL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |