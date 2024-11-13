# MAYORES

- **Pregunta 1**: "Se asume que los mensajes son autenticados, de modo que los mensajes corruptos o fabricados por procesos bizantinos son detectados y
descartados por los procesos correctos". Preguntando como un novato en sistemas distribuidos, ¿es usual esto? Tenía entendido que una falla bizantina, como en la caricatura de Lamport, es protegerse ante *traidores* que sí pueden comunicarse con los procesos correctos. Concretamente puede ser que uno de los nodos haya sido hackeado, y los atacantes pueden leer y enviar mensajes desde el mismo, o incluso robar su clave privada.
- **Respuesta 1**: Entiendo que sí, que en el contexto de blockchain es usual hacer la suposición de que la clave privada es “no robable”. Es la misma suposición que se hace en el paper original de Setchain. Por la referencia que encontré allá, entiendo que viene de una clasificación dada en "Atomic Broadcast: From Simple Message Diffusion to Byzantine Agreement":
> A system component is correct if its response to inputs is consistent with its specification. A component failure occurs when a component does not behave in the manner specified. An omission failure occurs when, in response to a sequence of inputs, a component never gives the specified output. A timing failure occurs when the component gives the specified output too early, too late, or never. A Byzantine failure occurs when the component does not behave in the manner specified: either no output occurs, or the output is outside the real-time interval specified, or some output different from the one specified occurs. An important subclass of Byzantine failures are those for which any resulting corruption of messages relayed by components such as processors and links is detectable by using a message authentication protocol. We call failures in this class authentication-detectable Byzantine failures. Error detecting codes and public-key cryptosystems based on digital signatures are two examples of authentication techniques which can ensure that both unintentional and intentional message corruptions are detected with very high probability. 

- **Pregunta 2**: (p30) ¿Puede realmente conocerse la cota de servidores bizantinos (f) de antemano? A mi entender esto es más un meta-parámetro para hablar sobre la confiabilidad del sistema, pero no algo que se sabe a priori y que los servidores pueden usar. En particular, ¿esto no impide escalar horizontalmente el sistema? ¿O qué pasa en ese caso? Tal vez hay algo que no entiendo de la situación ¿es un sistema cerrado?
- **Respuesta 2**: No, no se puede conocer la cota de servidores bizantinos de antemano, el f es, en efecto, un meta-parámetro. Pero entiendo que es usual en este tipo de sistemas fijar una cota superior f y luego razonar sobre eso. Respecto a “escalar horizontalmente el sistema”, entiendo que en principio el sistema no escala. Se fija un sistema con una determinada cantidad de servidores y una cota f de servidores bizantinos. Es un sistema cerrado, en el sentido que no entran nuevos agentes, ni un agente bueno se vuelve malo.

- **Pregunta 3**: ¿Hay algún estudio o cota sobre si el agregado de las pruebas a la cadena aumenta mucho el uso de recursos?
- **Respuesta 3**: No hay estudios específicos sobre la sobrecarga que generan las pruebas. Sin embargo (aunque no forman parte del trabajo realizado en la tesina), el grupo continuó haciendo otros estudios. Por ejemplo, en [este artículo](https://arxiv.org/pdf/2406.02316) se hicieron algunos cálculos respecto a cuánto cuesta firmar y chequear firmas. Existe otro artículo (que no lo puedo compartir porque está under-submission en este momento, es decir, no está público), en el cual se midió no solo cantidad de elementos por segundo añadidos a la Setchain en entornos más realistas sino la distribución de las latencias experimentadas por los elementos añadidos a Setchain para alcanzar las cinco etapas diferentes hasta su "commit" definitivo: la tx llega a la mempool de un servidor, la tx llega a la mempool de f + 1 servidores, la tx llega a la mempool de todos los servidores, la tx se incluye en un bloque, y se incluyen f+1 pruebas del bloque.

- **Punto 4**: Capítulo 5 "pruebas formales": ninguna de estas son pruebas formales, sino de lenguaje natural (no hay formalismo, no pueden ser chequeadas mecánicamente). No es un problema en sí, pero el título debería cambiar.
- **Respuesta 4**: Cambié el título a "Pruebas de corrección" y eliminé toda derivación de la palabra "formal".


# MENORES

- **Punto 1**: p1. "De estado inmutable": acá "estado" refiere al texto (código) del programa? Porque puede interpretarse como estado en el sentido de una memoria. Por ahí cambiar a "programas inmutables" / "de característica inmutable"?
- **Respuesta 1**: Cambiado a "los cuales son programas inmutables alojados en la blockchain".

- **Punto 2**: p2. "ataques bizantinos", si bien se define mejor después, tal vez una pequeña aclaración acá ayude.
- **Respuesta 2**: Esa sección fue modificada debido a otras sugerencias de cambio.

- **Punto 3**: s1.3. "para guardar transacciones ... hasta el bloque génesis": siempre es necesario esto? Tengo entendido que no hace falta, puede obtenerse toda la blockchain cuando el nodo se arma, y luego podar algún prefijo. Por otro lado la oración es medio confusa, está hablando de memoria? "Nodo" debería ser "bloque"?
- **Respuesta 3**: No tengo claro si siempre es necesario, tampoco me acordaba dónde había leído eso como para profundizar. Para no complicarla lo cambié a algo más concreto. Sobre todo porque tampoco sé si funcionará igual en todos los sistemas y era únicamente para dar un ejemplo.
Cambiado a: 
> Por otro lado, la escalabilidad vertical en la blockchain implica aumentar el poder de cómputo de los nodos existentes en la red, mediante la actualización de sus capacidades de hardware, como la mejora de GPUs o la ampliación de almacenamiento.

- **Punto 4**: - s1.3 "Visa ... 2000 transacciones por segundo" este número me pareció muy bajo (da 170M por día, imagino que sólo en EEUU hay más
que esto). El paper referenciado tiene esta cifra, pero la fuente que citan tiene el link roto. No encuentro datos muy certeros, encontré desde 1700 a 65000... No hace falta que lo cambien, sólo me dio curiosidad.
- **Respuesta 4**: No apliqué cambios. Es cierto que el número parece sospechosamente bajo. No encontré otro artículo académico para citar (no los podía descargar gratuitamente). En un [reporte de visa](https://corporate.visa.com/content/dam/VCOM/download/corporate/media/visanet-technology/visa-net-booklet.pdf) menciona distintos números calculo que en función de cómo se define "transacción".
    * More than 150 million transactions every day authorized in 175 currencies  (1700 por segundo)
    * Processing 80 billion transactions annually -Includes authorization & clearing transactions for payment and cash disbursements. - (257201 por segundo)
    * today is capable of handling more than 24,000 transaction messages per second with reliability, convenience and security. 

- **Punto 5**: Nota al pie 4 (TCP): creo que pueden asumir familiaridad del lector con TCP, aunque no está mal la nota
- **Respuesta 5**: No apliqué cambios.

- **Punto 6**: s 2.3.1: tal vez agregaría una pequeña mención a Lamport. 
- **Respuesta 6**: En efecto lo había mencionado y después lo saqué, pero ya que es tu amigo, le mando un saludo.

- **Punto 7**: 3.4: es un poco difícil de leer, agregar espacios entre los elementos de la tripla? 
- **Respuesta 7**: Sí, era realmente difícil de leer. Aclaré (es decir, las hice más cercanas al blanco) las llaves interiores para que no confunda visualmente.

- **Punto 8**: s 3.5: "con el tiempo" es demasiado informal, una pequeña aclaración ayudaría.
- **Respuesta 8**: Es un problema que tengo debido a la diferencia semántica entre "eventually" en inglés (una palabra muy práctica) y "eventualmente" en español (que significa "incierta o casualmente", es decir, no sirve). Como sea, cambié las tres ocurrencias e intenté hacerlo más formal.

- **Punto 9**: "se asume que en cualquier momento": cambiaría a "en todo momento" para ser más claro.
- **Respuesta 9**: hecho.

- **Punto 10**: Fig 1.3: esta parte me confundió y no sé si la figura ayuda mucho. El final del párrafo ("mostrando la necesidad de un protocolo de
formación de particiones") también pareció salir de nada.
- **Respuesta 10**: Borré la imagen y la frase “confusa”, me parece suficiente limitar esa sección a explicar que un método de escalabilidad para blockchain es simplemente copiar la idea de sharding de los modelos de bases de datos tradicionales.

- **Punto 11**: p30 "commited by the network" agregar una pequeña definición? Buscándola en el pdf recién noto que aparece en el glosario, tal vez una pequeña nota de que los elementos en cursiva aparecen allí ayude. De todas formas es una pavada. 
- **Respuesta 11**: Lo mencioné en la sección “organización del trabajo”:
> Finalmente, el capítulo \ref{chapter:glossary} consta de un breve glosario con algunos conceptos utilizados en inglés a lo largo del trabajo, ya que no cuentan con traducciones adecuadas al español. Estos términos son escritos en su mayor parte \textit{en cursiva}, de modo que se sugiere dirigirse al glosario cuando un término escrito con dicho estilo tipográfico genere dudas.

- **Punto 12**: p32 "más de un candidato": y a lo sumo dos, supongo? (o no alcanzaría el bit?) 
- **Respuesta 12**: Si bien la documentación de la librería dice claramente que V toma dos valores (el 0 o el 1), entiendo que teóricamente los valores candidatos podrían ser 4 (según lo que leí hay varios posts donde la gente se pregunta qué onda ese valor V, por ejemplo [este](https://ethereum.stackexchange.com/questions/42455/during-ecdsa-signing-how-do-i-generate-the-recovery-id) o [este otro](https://bitcoin.stackexchange.com/questions/38351/ecdsa-v-r-s-what-is-v/38909#38909)). No me queda claro qué sucede si ese V no alcanza para determinar exactamente cuál es la clave pública, lo que supongo es que es algo con probabilidad tan baja que ya fue. Cambié el nombre de “recovery bit” a “recovery id” porque aunque solo tome los valores 0 o 1, es un byte, no un bit.

- **Punto 13**: p35, Acá tuve la pregunta de por qué una transacción podría ser descartada, y si un atacante podría causar un DOS contaminando las
transacciones. Luego al leer que se filtran los elementos válidos entendí que no.
- **Respuesta 13**: Agregué lo siguiente.
> Un lote contiene potencialmente varios elementos enviados por uno o más clientes a un mismo nodo servidor que corre el Tendermint
Core, la aplicación y el collector. Si bien se omite en la figura, el collector valida los elementos que le llegan antes de insertarlos en un lote, con lo cual un lote construido por un collector correcto contiene solo elementos válidos.

También añadí una nota al pie:
> Una vez que el lote fue comprimido, el flujo es el mismo que el explicado en la sección anterior para \vanilla: la transacción que representa al elemento $e$ (y a otros) se chequea contra \CheckTx para determinar si debe ser insertada en la mempool o descartada\footnote{El criterio con el cual una transacción es añadida a la mempool o descartada se explica con detalle en la Sección ~\ref{subsec:compresschain-algorithms}}.


- **Punto 14**: p67 "límite de recursos destinados a Docker se mantiene constante": en total o por container? Entiendo que en total (con la CPU no hay mucha alternativa dentro de un único sistema, con la memoria sí).
- **Respuesta 14**: Sí, recursos totales. Entiendo que el CPU puede ser limitado si limitás la cantidad de cores utilizados. La siguiente oración la borré:
> Cada instancia fue empaquetada en un contenedor Docker [6] con uso limitado a 6 núcleos y 32GB de RAM.

Y la reemplacé por:
> Cada instancia fue empaquetada en un contenedor Docker~\cite{docker}, limitando los recursos totales asignados a Docker (independientemente de la cantidad de contenedores) a 6 núcleos y 32GB de RAM.

Añadí algunas aclaraciones:
> Se nota una clara degradación en la cantidad de elementos añadidos al aumentar la cantidad de nodos corriendo en el experimento. Esta baja es esperable, sin embargo, es importante notar el siguiente punto. Mientras más entidades (clientes y servidores) participen del consenso dentro de la red de Tendermint el experimento se hace más exigente en cuanto a recursos (procesador y memoria RAM). Dado que el límite de recursos totales destinados a Docker se mantiene constante durante todos los experimentos (independientemente de la cantidad de nodos), se genera una degradación en la cantidad de elementos que los clientes pueden enviar por segundo (puesto que los recursos destinados a cada contenedor disminuye cuando aumenta la cantidad de nodos). Naturalmente, y como ya se mencionó antes, al disminuir el ratio de elementos enviados por segundo, invariablemente también lo hace el ratio de elementos añadidos por segundo.

- **Punto 15**: p71 "dado que los algoritmos ... emplean bloques primitivos como Set Byzantine Consensus ..." no entendí esta oración, ni qué hace ese supuesto bloque. Pero más seriamente, creo que es la primera mención de que la implementación de Setchain no es exactamente como la del paper?
- **Respuesta 15**: Se menciona lo siguiente en la sección 1.5:
> Las implementaciones prototípicas previas de \setchain\footnote{Presentadas en \cite{Capretto.2022.Setchain}.} fueron construidas a partir de distintos componentes básicos: difusión confiable bizantina o \emph{Bizantine Reliable Broadcast}\cite{DBLP:journals/iandc/Bracha87, raynal.dist.systems}, difusión atómica bizantina o \emph{Byzantine Atomic Broadcast}\cite{Defago2004BAB}, conjuntos distribuidos que solo crecen bizantinos o \emph{Byzantine Distributed Grow-only Sets}\cite{Cholvi2021BDSO-arxiv} y consenso bizantino de conjunto o \emph{Set Byzantine Consensus}\cite{redbelly}.
En este trabajo se toma un enfoque diferente, haciendo hincapié en la construcción de implementaciones que cumplan con la especificación de \setchain pero que al mismo tiempo sean compatibles con los requerimientos del mundo real. Es por eso que cada una de las soluciones originales propuestas en este trabajo está enteramente construida sobre la plataforma de aplicación de blockchain \textit{Tendermint}\cite{Buchman.2018.Tendermint}.

No está explicado cada uno de los bloques, pero me parece que con poner las referencias sería suficiente.
Añadí una aclaración de que fue mencionado antes, cosa que si alguien ya se olvidó puede ir a buscarlo:

> Como contribuciones originales de este trabajo se presentaron tres alternativas posibles para la implementación de \setchain construidas sobre Tendermint. Como se mencionó al inicio de la sección ~\ref{sec:contributions}, los algoritmos de \setchain presentados en \cite{Capretto.2022.Setchain} emplean bloques primitivos como \emph{Set Byzantine Consensus}. Por lo tanto, no es posible replicar los mismos comportamientos.

- **Punto 16**: s2.6: No estoy seguro cuánto puede mejorarse sin convertir a esto en un manual, pero me costó seguir la explicación de Tendermint y su API.
- **Repuesta 16**: Same. La documentación de Tendermint tampoco era destacable. No apliqué cambios.

# TIPOGRÁFICOS:

Todos los puntos mencionados fueron corregidos, junto a otros descubiertos mediante un spell-checker.








