###### tags: `auditoría`

# CVSS


## Rúbricas de puntuación V 3.1
Las rúbricas de puntuación son una ayuda para puntuar vulnerabilidades al complementar las definiciones de métricas en el Documento de especificación.

Diagrama 1: Rúbrica vectorial de ataque
![](https://i.imgur.com/CzCGztR.png)


Diagrama 2: Rúbrica de Complejidad de Ataque
![](https://i.imgur.com/kAY1x6B.png)

Diagrama 3: Rúbrica de interacción del usuario
![](https://i.imgur.com/TTc54qH.png)

Diagrama 4: Rúbrica de privilegios necesarios
![](https://i.imgur.com/XRCAzq5.png)

Diagrama 5: Rúbrica de alcance
![](https://i.imgur.com/fKkeCHd.png)

Tenga en cuenta que si no se ha producido un cambio en el alcance, los impactos de confidencialidad, integridad y disponibilidad reflejan las consecuencias para el componente vulnerable, de lo contrario, reflejan las consecuencias para el componente que sufre el mayor impacto.

Diagrama 6: Rúbrica de impacto de confidencialidad
![](https://i.imgur.com/e0MwSqk.png)

Diagrama 7: Rúbrica de impacto de integridad
![](https://i.imgur.com/fkiRDeK.png)

Diagrama 8: Rúbrica de impacto de disponibilidad
![](https://i.imgur.com/Ct8plJA.png)








---




## Guía de puntuación
A continuación se presentan una serie de recomendaciones para los analistas al calificar vulnerabilidades con CVSS v3.1.

### 1. Puntuación CVSS en el ciclo de vida de explotación
Al comprender cuándo calificar el impacto de las vulnerabilidades, los analistas deben restringir los impactos a un impacto final razonable que estén seguros de que un atacante puede lograr. La capacidad de causar este impacto debe estar respaldada por el puntaje mínimo de Explotabilidad como mínimo, pero también puede incluir detalles de la descripción de la vulnerabilidad. Por ejemplo, considere las siguientes dos vulnerabilidades.

En la vulnerabilidad 1, un atacante remoto no autenticado puede enviar una solicitud trivial y elaborada a un servidor web que hace que el servidor web revele la contraseña de texto sin formato de la cuenta raíz (administrador). El analista solo sabe por las métricas de subpuntaje de explotabilidad y la descripción de la vulnerabilidad que el atacante tiene acceso para enviar una solicitud diseñada al servidor web con el fin de explotar la vulnerabilidad. El impacto debería detenerse allí; Si bien un atacante puede utilizar estas credenciales para ejecutar código posteriormente como administrador, no se sabe si el atacante tiene acceso a un mensaje o método de inicio de sesión para ejecutar comandos con esas credenciales. Obtener acceso a esta contraseña representa una pérdida directa y grave de confidencialidad únicamente:

Puntaje base: 7.5 CVSS: 3.1 / AV: N / AC: L / PR: N / UI: N / S: U / C: H / I: N / A: N

En la vulnerabilidad 2, un usuario local con pocos privilegios puede enviar una solicitud trivial y diseñada al sistema operativo que hace que revele la contraseña de texto sin formato de la cuenta raíz (administrador). El analista sabe por las métricas de subpuntaje de explotabilidad y la descripción de vulnerabilidad que el atacante tiene acceso al sistema operativo, y puede iniciar sesión como un atacante local con pocos privilegios. Obtener acceso a esta contraseña representa una pérdida directa y grave de Confidencialidad, Integridad y Disponibilidad porque el analista puede emitir comandos razonablemente como la cuenta raíz / administrador (suponga que el atacante podría cerrar sesión desde su propia cuenta e iniciar sesión nuevamente como raíz) :

Puntaje base: 7.8 CVSS: 3.0 / AV: L / AC: L / PR: L / UI: N / S: U / C: H / I: H / A: H

### 2. Confidencialidad e integridad, versus impactos de disponibilidad
Las métricas de confidencialidad e integridad se refieren a los impactos que afectan los datos utilizados por el servicio. Por ejemplo, contenido web que ha sido alterado maliciosamente, o archivos del sistema que han sido robados. La métrica de impacto de disponibilidad se refiere a la operación del servicio. Es decir, la métrica Disponibilidad habla del rendimiento y funcionamiento del servicio en sí mismo, no de la disponibilidad de los datos. Considere una vulnerabilidad en un servicio de Internet como web, correo electrónico o DNS que permite a un atacante modificar o eliminar todos los archivos web en un directorio. El único impacto es a la Integridad, no a la Disponibilidad, ya que el servicio web todavía está funcionando, simplemente está devolviendo contenido alterado.

### 3. Vulnerabilidades locales explotadas por atacantes remotos
La orientación sobre los ataques locales se mejoró en CVSS v3.0 al aclarar las definiciones de la red y los valores adyacentes de la métrica del vector de ataque. Específicamente, los analistas solo deben calificar para Red o Adyacente cuando una vulnerabilidad está vinculada a la pila de red. Las vulnerabilidades que requieren la interacción del usuario para descargar o recibir contenido malicioso (que también podría entregarse localmente, por ejemplo, a través de unidades USB) deben calificarse como Local.

Por ejemplo, una vulnerabilidad de análisis de documentos, que no depende de la red para ser explotada, generalmente debe puntuarse con el valor Local, independientemente del método utilizado para distribuir dicho documento malicioso (por ejemplo, podría ser un enlace a un sitio web o mediante una unidad flash USB).

### 4. Encadenamiento de vulnerabilidad
CVSS está diseñado para clasificar y calificar vulnerabilidades individuales. Sin embargo, es importante apoyar las necesidades de la comunidad de análisis de vulnerabilidad al acomodar situaciones en las que se explotan múltiples vulnerabilidades en el curso de un solo ataque para comprometer un host o una aplicación. La puntuación de múltiples vulnerabilidades de esta manera se denomina encadenamiento de vulnerabilidad. Tenga en cuenta que esta no es una métrica formal, sino que se incluye como guía para los analistas al calificar este tipo de ataques.

Al calificar una cadena de vulnerabilidades, es responsabilidad del analista identificar qué vulnerabilidades se combinan para formar el puntaje encadenado. El analista debe enumerar las distintas vulnerabilidades y sus puntajes, junto con el puntaje encadenado. Por ejemplo, esto puede comunicarse dentro de un aviso de divulgación de vulnerabilidad publicado en una página web.

Además, el analista puede incluir otros tipos de vulnerabilidades relacionadas que podrían encadenarse con las vulnerabilidades que se puntúan. Específicamente, el analista puede enumerar tipos genéricos (o clases) de vulnerabilidades relacionadas que a menudo se encadenan juntas, o proporcionar descripciones adicionales de las condiciones previas requeridas que deben existir. Por ejemplo, uno podría describir cómo ciertos tipos de vulnerabilidades de inyección SQL son precursores de un ataque de scripting entre sitios (XSS), o cómo un tipo particular de desbordamiento de búfer otorgaría privilegios locales. Enumerar los tipos genéricos o clases de vulnerabilidades proporciona la información mínima necesaria para advertir a otros usuarios, sin informar potencialmente a los atacantes sobre nuevas oportunidades de explotación.

Alternativamente, el analista puede identificar (en forma de una lista de vulnerabilidades legibles por máquina y analizables como ID de CVE o CWE), una lista completa de vulnerabilidades relacionadas específicas que se sabe que están (o es muy probable que estén) encadenadas a una o Se puntúan más vulnerabilidades encadenadas para explotar un sistema de TI. En el caso de que una vulnerabilidad pueda explotarse solo después de que se cumplan otras condiciones previas (como la primera explotación de otra vulnerabilidad), es aceptable combinar dos o más puntajes CVSS para describir la cadena de vulnerabilidades al calificar para la sub-explotación menos restrictiva. métricas de puntuación y puntuación para las métricas de sub-puntuación de Impact más impactantes. El siguiente ejemplo utiliza los puntajes secundarios de explotabilidad, alcance e impacto para describir la cadena.

La vulnerabilidad A es CVSS: 3.1 / AV: L / AC: L / PR: L / UI: N / S: U / C: H / I: H / A: H. Requiere un usuario local con pocos privilegios para poder explotar.

La vulnerabilidad B es CVSS: 3.1 / AV: N / AC: L / PR: N / UI: R / S: U / C: L / I: L / A: L. Proporciona a un atacante remoto sin privilegios la capacidad de ejecutar código en un sistema con bajo impacto si un usuario local interactúa para completar el ataque.

Dados A y B, la cadena C podría describirse como la cadena de B → A,
CVSS: 3.1 / AV: N / AC: L / PR: N / UI: R / S: U / C: H / I: H / A: H, que combina la Explotabilidad de B, el alcance no cambia en ambos casos, y el Impacto de A, porque si uno puede explotar B y obtener la ejecución del código como un usuario local, entonces uno ha cumplido el requisito previo para posteriormente lanzar A causando un impacto de la vulnerabilidad A.

### 5. Alcance, componente vulnerable y componente impactado
Cuando una vulnerabilidad en un componente gobernado por una autoridad de seguridad puede afectar los recursos gobernados por otra autoridad de seguridad, se produce un cambio de Alcance. Esto suele ocurrir cuando el componente vulnerable y el componente afectado son parte de diferentes sistemas (físicos o lógicos) gobernados por diferentes autoridades de seguridad; o cuando se ha establecido un límite artificial para separar lógicamente los componentes vulnerables e impactados por razones de seguridad (por ejemplo, al ejecutar un proceso en un entorno limitado). Cuando un mecanismo de límite de seguridad que separa componentes se elude debido a una vulnerabilidad y esto causa un impacto de seguridad fuera del alcance de seguridad del componente vulnerable, se ha producido un cambio de Alcance. En este caso,

Las siguientes vulnerabilidades de ejemplo analizan diferentes aspectos del alcance de puntuación:

Una vulnerabilidad en una máquina virtual que permite a un atacante leer y / o eliminar archivos en el sistema operativo host (quizás incluso su propia máquina virtual) se considera un cambio de Alcance. En este ejemplo, hay dos autoridades de seguridad separadas: una que define y aplica el control de acceso para la máquina virtual y sus usuarios, y otra que define y aplica el control de acceso para el sistema host dentro del cual se ejecuta la máquina virtual.

Se debe considerar una violación de un límite de seguridad entre los niveles de privilegio del microprocesador al puntuar vulnerabilidades utilizando CVSS. Las capacidades de los programas de espacio de usuario que se ejecutan en niveles de privilegios más bajos generalmente están limitadas en qué instrucciones pueden ejecutar y en qué registros pueden escribir incluso cuando se ejecutan con privilegios de administrador del sistema operativo. Una vulnerabilidad que permite que un programa que se ejecuta en un nivel de privilegio más bajo se rompa y ejecute código arbitrario en un nivel de privilegio más alto debe considerarse un cambio de Alcance.

El límite de seguridad entre los enclaves seguros integrados en los microprocesadores y el resto de los procesos del sistema operativo, incluido el núcleo del sistema operativo, debe tenerse en cuenta al puntuar las vulnerabilidades utilizando CVSS. Una vulnerabilidad que permita que otros procesos afecten la confidencialidad, integridad o disponibilidad de datos o código en un enclave seguro debe considerarse un cambio de alcance.

Un cambio de alcance se produce cuando una vulnerabilidad en una aplicación web afecta a los clientes usuarios, por ejemplo, los navegadores web. Las vulnerabilidades comunes de este tipo incluyen secuencias de comandos entre sitios y redirección de URL. La vulnerabilidad se encuentra en la aplicación web, pero hay un impacto en los datos / comportamiento de los navegadores web de los usuarios víctimas, que están dentro de un alcance de seguridad diferente.

En un entorno distribuido, una vulnerabilidad en un componente que proporciona servicios de conectividad, protección o autenticación a componentes en una autoridad de seguridad diferente debe calificarse como un cambio de Alcance si un ataque exitoso impacta a estos otros componentes. Por ejemplo, una vulnerabilidad en un componente como un enrutador, firewall o administrador de autenticación que afecta la disponibilidad primaria de uno o más componentes posteriores debe calificarse como un cambio de Alcance. Sin embargo, si un ataque exitoso no afecta en absoluto, o solo causa un impacto insignificante en los componentes de una autoridad de seguridad diferente, la vulnerabilidad debe calificarse como Alcance sin cambios. Por ejemplo, una vulnerabilidad en un componente diseñado para implementarse como parte de una topología tolerante a fallas más grande no debe puntuarse con un alcance modificado si la tolerancia a fallas significa que un ataque exitoso no afecta los componentes en diferentes autoridades de seguridad. Cualquier efecto sobre los servicios adicionales proporcionados por el componente vulnerable se considera un impacto secundario y no un cambio de alcance.

Una vulnerabilidad en un simple lector de Formato de Documento Portátil (PDF) que permite a un atacante comprometer otros archivos en el mismo sistema operativo cuando una víctima abre un documento PDF malicioso se califica como Alcance sin cambios. Esto supone que el lector de PDF no tiene ninguna funcionalidad de autorización que se consideraría una autoridad de seguridad separada del sistema operativo subyacente.

Una vulnerabilidad de inyección SQL en una aplicación web generalmente no se considera un cambio de Alcance suponiendo que las credenciales se comparten entre la aplicación web y la base de datos SQL afectada, y por lo tanto son parte del mismo alcance de seguridad.

Una vulnerabilidad que bloquea un servidor web o un servidor SSH no se considera un cambio de Alcance ya que el impacto se limita solo al servicio provisto por el servidor afectado. El impacto en los usuarios es secundario y no se considera un cambio de Alcance ya que los usuarios no se consideran componentes.

Una vulnerabilidad que permita que un atacante agote un recurso compartido del sistema, como llenar un sistema de archivos, no debe considerarse un cambio de Alcance ya que el atacante todavía está actuando bajo las capacidades habituales de la aplicación y no está violando ningún límite de seguridad.

Al explotar una vulnerabilidad en una aplicación que permite a los usuarios acceso restringido a recursos compartidos con otros componentes a través de múltiples ámbitos de seguridad (por ejemplo, recursos del sistema operativo tales como archivos del sistema), un atacante puede acceder a recursos a los que no debería poder acceder. Como ya existe una ruta válida a través del límite de confianza, no hay cambio de Alcance.

Una vulnerabilidad en una aplicación que implementa su propia autoridad de seguridad que permite a los atacantes afectar los recursos fuera de su alcance de seguridad se califica como un cambio de Alcance. Esto supone que la aplicación no proporciona características para que los usuarios accedan a recursos gobernados por una autoridad de seguridad de nivel superior compartida con otros componentes a través de múltiples ámbitos de seguridad (por ejemplo, los recursos del sistema operativo subyacente). Un ejemplo sería una aplicación web que permite a los usuarios leer y modificar páginas web y archivos solo bajo las rutas de instalación de la aplicación web, y no proporciona ninguna característica para que los usuarios interactúen más allá de estas rutas. Una vulnerabilidad en esta aplicación que permite que un usuario malintencionado acceda a archivos del sistema operativo no relacionados con esta aplicación se considera un cambio de Alcance.

### 6. Componentes vulnerables protegidos por un firewall
Si una vulnerabilidad se califica con un Vector de ataque (AV) de la red (N) y el analista tiene una gran confianza en que el componente vulnerable se implementa en una red segura no disponible en Internet, el Vector de ataque modificado (MAV) puede calificarse como Adyacente, reduciendo el puntaje general de CVSS v3.1.

Ejemplo: Inyección de SQL almacenado MySQL (CVE ‑ 2013‑0375)

Puntaje base: 6.4 CVSS: 3.1 / AV: N / AC: L / PR: L / UI: N / S: C / C: L / I: L / A: N

Calificación ambiental: 5.4 CVSS: 3.1 / AV: N / AC: L / PR: L / UI: N / S: C / C: L / I: L / A: N / MAV: A

### 7. Vulnerabilidades de puntuación en bibliotecas de software (y similares)
Al evaluar el impacto de una vulnerabilidad en una biblioteca, independientemente de cualquier programa o implementación adoptada, el analista a menudo no podrá tener en cuenta las formas en que se podría usar la biblioteca. Si bien los productos específicos que usan la biblioteca deben generar puntajes CVSS específicos de cómo usan la biblioteca, la calificación de la biblioteca en sí misma requiere suposiciones. El analista debe calificar para el escenario razonable de implementación del peor de los casos. Cuando sea posible, la información de CVSS debe detallar estos supuestos.

Por ejemplo, una biblioteca que realiza la conversión de imágenes sería utilizada razonablemente por programas que aceptan imágenes de fuentes no confiables a través de una red. En el peor de los casos razonables, los pasaría a la biblioteca sin verificar la validez de las imágenes. Como tal, un analista que califica una vulnerabilidad en la biblioteca que se relaciona con los datos entrantes debe asumir un Vector de Ataque (AV) de la Red (N), pero explicar esta suposición en el resumen de la vulnerabilidad. Si la biblioteca puede ejecutarse con privilegios normales, con un menor impacto en la implementación de incrustación, o con altos privilegios, lo que aumenta los impactos, el analista debe asumir altos privilegios al calificar la vulnerabilidad en la biblioteca.

Al calificar una vulnerabilidad en una implementación dada usando la biblioteca impactada, la puntuación se debe volver a calcular para esa implementación específica. Por ejemplo, si una implementación incorpora la biblioteca vulnerable mencionada en el ejemplo anterior, pero solo opera en archivos locales, el Vector de ataque (AV) sería Local (L). Si la implementación que incorpora esta biblioteca no invoca ninguna de las funciones defectuosas o no admite el modo que desencadena esa vulnerabilidad, no tendría interfaz ni vector de ataque para explotar la vulnerabilidad. Por lo tanto, esa vulnerabilidad en la biblioteca incrustada no tendría ningún impacto en esa implementación, lo que daría como resultado una puntuación para la implementación dada de 0.

### 8. Múltiples puntajes base de CVSS
Es común que una vulnerabilidad esté presente en múltiples versiones de productos, plataformas y / o sistemas operativos. En algunas circunstancias, las métricas base pueden diferir en diferentes versiones de productos, plataformas y / o sistemas operativos. Por ejemplo, una vulnerabilidad hipotética es aplicable a múltiples sistemas operativos producidos por el mismo proveedor. La Complejidad de ataque (AC) de esta vulnerabilidad en un sistema operativo heredado es Baja (L). Sin embargo, un sistema operativo más nuevo tiene nuevas capacidades de protección inherentes que cambian la Complejidad de ataque a Alta (H). Esta variación finalmente conduce a diferentes puntuaciones base para la misma vulnerabilidad en los dos sistemas operativos.

Es aceptable calificar y publicar múltiples puntajes base para una sola vulnerabilidad, siempre que cada uno tenga un lenguaje adicional que describa las versiones específicas del producto, las plataformas y / o los sistemas operativos que son relevantes para el puntaje. Los valores para todos los atributos de Puntaje base (no solo un Puntaje base precalculado) se deben proporcionar para cada versión, plataforma y / o sistema operativo del producto afectado utilizando un formato estándar. En situaciones donde se aplican múltiples puntajes base pero solo se proporciona un puntaje único, se debe utilizar el puntaje base más alto.

### 9. Marco de extensiones CVSS
Existen oportunidades para aprovechar la base central de CVSS para esfuerzos de puntuación adicionales. Por ejemplo, se presentó una propuesta al CVSS Special Interest Group (SIG) para incorporar la privacidad en CVSS mediante la superposición de combinaciones de CVSS Base y métricas ambientales para derivar un impacto en la privacidad.

Las siguientes pautas definen un método estándar para extender CVSS para incluir métricas y grupos de métricas adicionales mientras se retienen las métricas base, temporales y ambientales oficiales. Las métricas adicionales permiten a los sectores industriales como la privacidad, la seguridad, la automoción, la atención médica, etc., calificar factores que están fuera del estándar CVSS.

#### 9.1. Pautas
Las fórmulas, constantes o definiciones de las métricas CVSS Base, Temporales o Ambientales existentes no deben modificarse. Si se desea un cambio en un elemento existente, cree un nuevo grupo de indicadores con un nuevo nombre y trabaje en él como desee.

Las nuevas métricas no se deben agregar a los grupos de métricas existentes, sino que se deben agregar a los nuevos grupos de métricas. Los nuevos grupos de indicadores se pueden basar en grupos de indicadores existentes.

Las nuevas métricas pueden basarse en sub-fórmulas en el estándar, como la sub-puntuación de Explotabilidad, pero estas podrían cambiar, eliminarse o reemplazarse en futuras revisiones del estándar, por lo que no se debe confiar en los valores absolutos.

Los nuevos grupos de indicadores pueden tener opcionalmente una puntuación. Si lo hacen, el puntaje debe estar entre 0.0 y 10.0, siendo 10.0 el más severo. El puntaje debe basarse en el ajuste del puntaje base y / o puntajes ambientales y temporales, de manera similar a cómo los puntajes ambientales / temporales ajustan el puntaje base para producir el puntaje final.

El CVSS SIG no aprueba oficialmente las extensiones, sino que actúa como un organismo de consultoría, similar al IETF 1 . El CVSS SIG da la bienvenida y fomenta la innovación, pero tiene interés en mantener la coherencia en todas las extensiones propuestas.

La lista de extensiones validadas aparecerá en el sitio web de first.org, similar a IANA 2 .

Campos obligatorios: nombre, descripción, página web externa autorizada

Campos opcionales: esquema JSON, esquema XML, calculadora JavaScript

#### 9.2. Formato de cadena de vector sugerido
Las cadenas de vectores de extensión CVSS deben enumerarse por separado, utilizando el siguiente formato:

CVSS: 3.1 / AV: x / AC: x / PR: x / UI: x / S: x / C: x / I: x / A: x

EXT: 1.0 / NUEVO1: VAL1 / NUEVO2: VAL2

dónde:

EXT: n . n es un identificador de extensión único y un número de versión major.minor

NUEVO n es un atributo único de la extensión para cada nueva métrica

VAL n es un valor único para el atributo para cada nuevo valor de indicador

### 10. Consideraciones de vectores de ataque
Al calificar el Vector de ataque, use Adyacente o Red (según corresponda), cuando se requiera una conexión de red para que un ataque tenga éxito, incluso si el ataque no se lanza a través de una red. Por ejemplo, un atacante local puede engañar a un programa local vulnerable y privilegiado para que envíe datos confidenciales a un servidor que el atacante elija a través de una red. Como se requiere una conexión de red para recopilar los datos confidenciales, esto se puntúa con un Vector de ataque de red.

Las vulnerabilidades en las que un componente recibe datos maliciosos en una red y luego se pasan a un componente separado con una vulnerabilidad deben puntuarse con un Vector de ataque local. Un ejemplo es un navegador web que descarga un documento de Office malicioso, lo guarda en el disco y luego inicia una aplicación de Office vulnerable que lee el archivo guardado.

En los casos en que la funcionalidad vulnerable es parte del componente que recibe los datos maliciosos, Attack Vector debe calificarse como Red. Un ejemplo es un navegador web con una vulnerabilidad en el navegador en sí, o un complemento o extensión del navegador, que se activa cuando se reciben los datos maliciosos.

### 11. Requerimientos de seguridad
Las métricas de requisitos de seguridad son parte del grupo de métricas ambientales y modifican la ponderación que las métricas de impacto modificadas tienen en la puntuación ambiental general. Esta sección proporciona orientación sobre cómo seleccionar valores métricos apropiados para estos en función de las características de un entorno específico. Los ejemplos están simplificados para ilustrar los conceptos.

#### 11.1. Requisito de confidencialidad (CR)
El requisito de confidencialidad de un sistema debe basarse en el nivel de clasificación de los datos almacenados o utilizados por el usuario y / o las aplicaciones que se ejecutan en el sistema de destino. El cifrado de los datos en reposo en este dispositivo también debe tenerse en cuenta al establecer el Requisito de confidencialidad. Los datos que pasan a través de un dispositivo sin ser consumidos o procesados ​​(por ejemplo, un interruptor o firewall) no deben tenerse en cuenta al evaluar este atributo. Ver abajo para ejemplos.

*Nota*: El volumen de datos puede influir en el valor del atributo, pero no debería tener tanto impacto como la clasificación (es decir, el tipo) de datos que se almacenan o utilizan.

Un dispositivo que almacena datos clasificados en el nivel más alto debe tener este atributo calificado como Alto. Sin embargo, si los datos confidenciales se cifran en reposo, este atributo puede clasificarse como Medio.

Un dispositivo que almacena datos clasificados como no públicos pero no tan altos como el nivel más alto debe tener este atributo calificado como Medio. Sin embargo, si los datos confidenciales se cifran en reposo, este atributo puede calificarse como Bajo.

Un dispositivo que almacena datos que se pueden compartir abiertamente públicamente debe tener este atributo calificado como Bajo.

El equipo de red como un enrutador, conmutador o firewall generalmente se calificará como Medio debido estrictamente a la sensibilidad de la información, como tablas de enrutamiento, etc.

Cualquier sistema que almacene credenciales de inicio de sesión sin cifrado debe tener este atributo calificado como Alto. Esto incluye cuentas de servicio y credenciales integradas en scripts o código fuente.

#### 11.2. Requisito de integridad (IR)
Los requisitos de integridad de un sistema se centran en la importancia de la precisión de los datos que almacena o utiliza. Los datos que pasan a través de un dispositivo sin ser consumidos o procesados ​​(por ejemplo, un interruptor o firewall) no deben tenerse en cuenta al evaluar este atributo. El uso de cifrado en los datos en reposo no debe tenerse en cuenta para este atributo. Vea abajo para ejemplos:

Los dispositivos que contienen datos de transacciones monetarias y / o información de identificación personal (PII) deben tener una calificación alta.

Los dispositivos que contienen datos directamente utilizados para tomar decisiones comerciales o de gestión de riesgos deben tener una calificación mínima de Medio. A medida que aumenta la severidad de las decisiones, también debería aumentar la calificación del requisito de integridad.

Los dispositivos que contienen datos directamente utilizados para tomar decisiones de salud deben tener una calificación alta.

Los equipos de red como un enrutador o conmutador generalmente tendrán una calificación de al menos Medio debido estrictamente a la sensibilidad de la información, como las tablas de reenvío, etc.

Los cortafuegos deben clasificarse como altos debido a la sensibilidad del conjunto de reglas.

#### 11.3. Requisito de disponibilidad (AR)
El requisito de disponibilidad de un sistema debe basarse en los requisitos de tiempo de actividad y la redundancia del dispositivo o las aplicaciones alojadas por el dispositivo. Los dispositivos que forman parte de clústeres redundantes tendrán requisitos de disponibilidad más bajos. Vea abajo para ejemplos:

Los dispositivos sin redundancia de capacidad total que están clasificados con requisitos de recuperación de menos de 24 horas deben tener una clasificación alta.

Los dispositivos sin redundancia de capacidad total que están clasificados con requisitos de recuperación entre 1 y 5 días deben estar clasificados como medios.

Los dispositivos con requisitos de recuperación de más de 5 días deben tener una calificación baja.

Los dispositivos en clúster y / o aquellos con redundancia de capacidad total deben clasificarse como Bajos.

Los dispositivos que deben tener tiempos de respuesta rápidos para fines transaccionales basados ​​en los requisitos reglamentarios deben tener una calificación alta.








# Cambios de la versión 3.0


Resumen cuadro:


| Version 2.0                                                                                                                                                                                    | Version 3.0                                                                                                                                                                                                   |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Las vulnerabilidades se puntúan en relación con el impacto general en la plataforma de host.                                                                                                   | Las vulnerabilidades ahora se puntúan en relación con el impacto en el componente afectado.                                                                                                                   |
| No hay conocimiento de situaciones en las que una vulnerabilidad en una aplicación afecta a otras aplicaciones en el mismo sistema.                                                            | Una nueva métrica, Scope, ahora acomoda vulnerabilidades donde la cosa que sufre el impacto (el componente afectado) es diferente de la cosa que es vulnerable (el componente vulnerable).                    |
| Access Vector puede combinar ataques que requieren acceso al sistema local y ataques de hardware físico.                                                                                       | Los valores locales y físicos ahora están separados en la métrica del vector de ataque.                                                                                                                       |
| En algunos casos, Access Complexity combinó la configuración del sistema y la interacción del usuario.                                                                                         | Esta métrica se ha separado en Complejidad de ataque (que representa la complejidad del sistema) e Interacción del usuario (que representa la participación del usuario en un ataque exitoso).                |
| En la práctica, las puntuaciones métricas de autenticación se sesgaron hacia dos de los tres resultados posibles, y no capturaron de manera efectiva el aspecto deseado de una vulnerabilidad. | Una nueva métrica, Privilegios requeridos, reemplaza la autenticación y ahora refleja los mayores privilegios requeridos por un atacante, en lugar de la cantidad de veces que el atacante debe autenticarse. |
| Las métricas de impacto reflejan el porcentaje de impacto causado a una aplicación vulnerable.                                                                                                 | Los valores de la métrica de impacto ahora reflejan el grado de impacto y se renombran a Ninguno, Bajo y Alto.                                                                                                |
| No se consideró que las métricas medioambientales de la distribución objetivo y el potencial de daño colateral fueran útiles.                                                                  | La distribución objetivo y el potencial de daño colateral han sido reemplazados por factores mitigantes.                                                                                                      |
| CVSS v2.0 no pudo acomodar la puntuación de múltiples vulnerabilidades utilizadas en el mismo ataque.                                                                                          | Si bien no es una métrica formal, se proporciona orientación sobre la puntuación de múltiples vulnerabilidades con el Encadenamiento de Vulnerabilidad.                                                       |




---


### 1. Alcance, componente vulnerable y componente impactado

CVSS v2.0 presentó dificultades para los proveedores al puntuar vulnerabilidades que comprometerían completamente su software, pero que solo afectarían parcialmente el sistema operativo del host. En v2.0, las vulnerabilidades se puntúan en relación con el sistema operativo host, lo que llevó a un proveedor de aplicaciones a adoptar una convención métrica de impacto "Parcial +".[3] CVSS v3.0 aborda este problema con actualizaciones sobre dónde se puntúan las métricas de impacto y una nueva métrica llamada Alcance (se trata más adelante). Por lo tanto, un cambio conceptual importante en CVSS v3.0 es la capacidad de calificar las vulnerabilidades que existen en un componente de software (al que nos referimos formalmente como el componente vulnerable ) pero que afectan a un componente de software, hardware o red separado (al que nos referimos formalmente como el componente afectado ), como se ilustra en la Figura 1.[4]

Cambio de alcance Figura 1: cambio de alcance

Por ejemplo, considere una vulnerabilidad en una máquina virtual que compromete el sistema operativo del host. El componente vulnerable es la máquina virtual, mientras que el componente afectado es el sistema operativo host. Debido a que estos dos componentes administran de manera independiente los privilegios de los recursos informáticos, representan autoridades separadas (autorización). En la Figura 1, la máquina virtual es administrada por la "Autoridad A", mientras que el sistema operativo host es administrado por la "Autoridad B". Cuando dos autoridades están involucradas en una vulnerabilidad de vulnerabilidad, CVSS considera que se ha producido un cambio de alcance . Esta condición es capturada por la nueva métrica, Scope.


![](https://i.imgur.com/n5BQ9sA.png)

Como se muestra en la Figura 1, cuando se puntúan las vulnerabilidades en CVSS v3.0, las métricas de explotabilidad se puntúan en relación con el componente vulnerable. Es decir, se puntúan considerando el componente que sufre el defecto de codificación. Por otro lado, las métricas de impacto se puntúan en relación con el componente afectado. En algunos casos, el componente vulnerable puede ser el mismo que el componente afectado, en cuyo caso no se ha producido ningún cambio en el alcance. Sin embargo, en otros casos, puede haber un impacto en el componente vulnerable, así como en el componente afectado. En estos casos, se ha producido un cambio en el alcance, y las métricas de Impacto de confidencialidad, integridad y disponibilidad deben reflejar el impacto en el componente vulnerable o en el componente afectado, lo que sea más grave.

*Otos ejemplos*:
En el caso de una vulnerabilidad que permita el robo de un archivo de contraseña, si bien puede haber pasos posteriores que el atacante tome para cometer acceso no autorizado a la cuenta, el resultado más directo es una pérdida de confidencialidad del archivo del sistema local. Como tal, no habría cambio de alcance. Sin embargo, en el caso de una vulnerabilidad que permita que un atacante sobrescriba la tabla ARP de un enrutador, hay dos impactos. Primero, al archivo del sistema del enrutador (Impacto de integridad en el componente vulnerable), y segundo, a los servicios de Internet atendidos por el enrutador (Impacto de disponibilidad a los sistemas afectados). Debido a que el puntaje debe reflejar el resultado más severo, el puntaje de la métrica de impacto puede reflejar la pérdida de integridad para el componente vulnerable o la pérdida de disponibilidad para los servicios de Internet, lo que sea más severo.


### 2. Vector de acceso

El Vector de acceso (de v2.0) se ha renombrado como Vector de ataque, pero todavía refleja la "lejanía" del atacante en relación con el componente vulnerable. Es decir, cuanto más remoto sea un atacante al componente vulnerable (en términos de distancia de red lógica y física), mayor será el puntaje Base. Además, esta métrica ahora distingue entre ataques locales que requieren acceso al sistema local (como un ataque contra una aplicación de escritorio) y ataques físicos que requieren acceso físico a la plataforma para explotar una vulnerabilidad (como con un firewire, USB, o ataque de jailbreak).

### 3. Complejidad de ataque
La Complejidad de acceso (de la versión 2.0) combinó dos problemas: cualquier condición de software, hardware o red más allá del control del atacante que debe existir u ocurrir para que la vulnerabilidad sea explotada con éxito (por ejemplo, una condición de carrera de software o configuración de la aplicación) , y el requisito de interacción humana (por ejemplo, exigir que un usuario ejecute un ejecutable malicioso). Por lo tanto, la Complejidad de acceso se ha separado en dos métricas, Complejidad de ataque (que aborda la condición anterior) e Interacción del usuario (que aborda la última condición).

### 4. Privilegios requeridos
La nueva métrica, Privilegios necesarios, reemplaza la métrica de autenticación de v2.0. En lugar de medir la cantidad de veces que un atacante debe autenticarse por separado en un sistema, Privilegios necesarios captura el nivel de acceso requerido para un ataque exitoso. Específicamente, los valores métricos Alto, Bajo y Ninguno reflejan los privilegios requeridos por un atacante para aprovechar la vulnerabilidad.

### 5. Métricas de impacto
La Confidencialidad, Integridad y Disponibilidad impactan los valores métricos de v2.0 de Ninguno, Parcial y Completo han sido reemplazados por Ninguno, Bajo y Alto. En lugar de representar el porcentaje general (proporción) de los sistemas afectados por un ataque, los nuevos valores métricos reflejan el grado general de impacto causado por un ataque. Por ejemplo, mientras el Heartbleed[6] la vulnerabilidad solo causó una pérdida de una pequeña cantidad de información, el impacto fue bastante severo. En CVSS v2.0, esto se habría calificado como Parcial, mientras que en CVSS v3.0, esto se calificó apropiadamente como Alto.

Además, en el ejemplo anterior, las métricas de impacto ahora reflejan la consecuencia del componente afectado. Y el componente afectado puede o no ser el mismo que el componente que posee la vulnerabilidad que se está explotando.

### 6. Métrica Temporal
La influencia de las métricas temporales se ha reducido en v3.0, en relación con v2.0. La explotabilidad ha sido renombrada como Explotación del código de madurez para representar mejor lo que mide la métrica.

### 7. Métrica Ambiental
La métrica ambiental La distribución del objetivo y el potencial de daños colaterales han sido reemplazados por factores modificados que se adaptan a los controles de mitigación o debilidades de control que pueden existir dentro del entorno del usuario que podrían reducir o aumentar el impacto de una vulnerabilidad explotada con éxito.

### 8. Escala de calificación cualitativa
Algunas organizaciones crearon sistemas para asignar CVSS v2.0 Puntajes base a calificaciones cualitativas. CVSS v3.0 ahora proporciona un mapeo estándar de puntajes numéricos a los términos de calificación de gravedad Ninguno, Bajo, Medio, Alto y Crítico, como se explica en el documento de especificación CVSS v3.0. El uso de estas clasificaciones de gravedad cualitativas es opcional, y no es necesario incluirlas al publicar las puntuaciones de CVSS.

Se solicita a las organizaciones que usan puntajes CVSS v3.0 que deseen usar un sistema de calificación de gravedad alternativo que utilicen diferentes términos de calificación o que establezcan claramente que sus calificaciones no cumplen con la especificación CVSS v3.0, para evitar confusiones.

