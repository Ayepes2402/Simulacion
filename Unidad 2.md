# Actividad 5  
## Intención    

Para este reto quise explorar la tensión entre la creatividad individual y la presión del sistema por mantener el orden. Mi idea surgió al pensar que muchas veces las personas creativas tienen ideas diferentes, pero la sociedad, las instituciones o incluso las normas establecidas hacen que esas ideas sean rechazadas o limitadas porque no encajan con lo que se considera "normal". Quise representar esa contradicción mediante un sistema de partículas donde la creatividad siempre intenta abrirse camino, pero constantemente encuentra obstáculos que la obligan a cambiar de dirección. Mi intención no es mostrar que un lado sea completamente bueno o malo, sino **hacer visible cómo existe una tensión constante entre crear algo nuevo y adaptarse a las reglas del entorno.**  

## Tipos de partículas

**Partículas creativas (multicolor)**
Seleccioné este tipo de partículas porque quiero hacer perceptible a las personas con ideas diferentes, que buscan expresarse libremente y cuestionar lo establecido. Espero que produzcan movimientos rápidos, impredecibles y que intenten abrirse camino hacia el centro del sistema.

**Partículas del núcleo social (rojas)**  
Seleccioné este tipo de partículas porque quiero representar las instituciones, las normas y el statu quo. Espero que produzcan un punto de estabilidad alrededor del cual gira el resto del sistema y que transmitan la sensación de un orden difícil de cambiar.

**Partículas del margen (amarillas)**  
Seleccioné este tipo de partículas porque quiero representar la presión social y los mecanismos que protegen el orden establecido. Espero que produzcan una barrera que impida que las partículas creativas lleguen libremente al núcleo.  

# Cantidad de partículas de cada tipo
Creativas: 100 partículas
Núcleo social: 60 partículas
Margen: 90 partículas

Seleccioné estas cantidades porque quiero que las personas creativas sean el grupo más numeroso, representando que existen muchas ideas diferentes. Sin embargo, aunque el núcleo es más pequeño, está respaldado por una gran cantidad de partículas del margen que actúan como protección. Espero que esto produzca una sensación de desigualdad, donde muchas ideas terminan siendo contenidas por un sistema organizado.

## Matriz  

Las relaciones entre partículas son:

Las creativas se repelen ligeramente entre sí para que cada una conserve su individualidad.  
Las creativas sienten atracción hacia el núcleo social porque buscan participar y aportar nuevas ideas.  
El margen rechaza fuertemente a las creativas para impedir que lleguen al centro.  
El núcleo permanece unido gracias a una atracción interna.  
El margen coopera con el núcleo para mantener la estructura del sistema.  

Seleccioné esta matriz porque quiero hacer perceptible que la contradicción no depende de los colores, sino de las reglas de interacción. Espero que produzca intentos constantes de acercamiento, persecución y rechazo.  

| **Influye sobre →** | **Creativas** | **Núcleo social** | **Margen** |
| ------------------- | :-----------: | :---------------: | :--------: |
| **Creativas**       |    **-0.4**   |      **0.3**      |   **0.1**  |
| **Núcleo social**   |    **-0.1**   |      **0.4**      |   **0.6**  |
| **Margen**          |    **-1.0**   |      **0.7**      |  **-0.2**  |

| Relación                         | Justificación                                                                                                                                                           |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Creativas → Creativas (-0.4)** | Se repelen ligeramente para que cada individuo conserve su identidad y no forme grupos demasiado compactos.                                                             |
| **Creativas → Núcleo (0.3)**     | Las personas creativas intentan acercarse al sistema porque quieren aportar sus ideas y ser escuchadas.                                                                 |
| **Creativas → Margen (0.1)**     | Apenas sienten atracción hacia el margen; simplemente se cruzan con él mientras buscan llegar al centro.                                                                |
| **Núcleo → Creativas (-0.1)**    | El sistema no busca perseguirlas activamente, pero tampoco facilita su integración.                                                                                     |
| **Núcleo → Núcleo (0.4)**        | Las instituciones permanecen unidas para conservar la estabilidad y el orden establecido.                                                                               |
| **Núcleo → Margen (0.6)**        | El núcleo mantiene una relación de cooperación con el margen para proteger la estructura del sistema.                                                                   |
| **Margen → Creativas (-1.0)**    | Es la relación más fuerte. El margen rechaza a las personas creativas e impide que lleguen al núcleo, representando la presión social que reprime las ideas diferentes. |
| **Margen → Núcleo (0.7)**        | El margen protege al núcleo y permanece cerca de él para mantener el orden.                                                                                             |
| **Margen → Margen (-0.2)**       | Se repelen ligeramente para distribuirse alrededor del núcleo y formar una barrera en lugar de un grupo compacto.                                                       |

## Relación asimétrica  

**La relación asimétrica principal es:**

Creativas → Núcleo = 0.3 (las creativas quieren acercarse al sistema).  
Núcleo → Creativas = -0.1 (el sistema no responde con la misma apertura).  

**Además, la relación más importante del sistema es:**

Margen → Creativas = -1.0, donde la presión social actúa como un mecanismo de rechazo que dificulta que las ideas creativas lleguen al centro.  

Esa diferencia en las reglas hace que la contradicción se vea en el movimiento de las partículas y no solamente en su significado simbólico.  

## Intensidad y alcance de cada relación

Las fuerzas de atracción y repulsión tienen distintas intensidades según el tipo de partícula. La relación más fuerte es la repulsión del margen hacia las partículas creativas, mientras que la atracción de las creativas hacia el núcleo es moderada.

Seleccioné estas intensidades porque quiero que el conflicto sea evidente sin impedir completamente el movimiento de las partículas. Espero que produzca trayectorias cambiantes y situaciones donde algunas logren acercarse al núcleo mientras otras son expulsadas.  

## Distancias de interacción

Las partículas interactúan dentro de un radio aproximado de 140 píxeles.

Seleccioné esta distancia porque quiero que las relaciones ocurran únicamente cuando las partículas están relativamente cerca unas de otras. Espero que produzca agrupaciones, bloqueos y reorganizaciones constantes.

## Fricción y velocidad máxima

La fricción del sistema es 0.88, lo que permite movimientos fluidos sin que las partículas pierdan completamente su impulso.

Las velocidades máximas son diferentes para cada tipo:

Creativas: 8
Núcleo social: 2
Margen: 4.5

Seleccioné estos valores porque quiero que las partículas creativas transmitan dinamismo y búsqueda constante, mientras que el núcleo permanezca estable y el margen pueda reaccionar rápidamente para contenerlas. Espero que produzca una diferencia clara entre los comportamientos de cada población.  

## Distribución inicial

Las partículas creativas aparecen distribuidas aleatoriamente por todo el espacio.

Las partículas del núcleo social nacen agrupadas en el centro.

Las partículas del margen forman un anillo alrededor del núcleo.

Seleccioné esta distribución porque quiero que desde el inicio pueda reconocerse la estructura del sistema. Espero que produzca la sensación de que las ideas creativas intentan atravesar una barrera para llegar al centro.  

## Parámetros constantes y variables

Constantes

Matriz de relaciones.
Radio de interacción.
Fricción.
Velocidad máxima de cada tipo.
Distribución inicial de cada población.

Estos parámetros mantienen la identidad del sistema en todas las ejecuciones.

Variables

Posición inicial exacta de cada partícula.
Dirección inicial.
Velocidad inicial.
Cantidad de partículas mediante el panel de control.

Estos parámetros hacen que cada simulación sea diferente sin perder el concepto principal.

## Apariencia e interacción

Las partículas creativas cambian continuamente de color y dejan una estela a su paso para representar que las ideas pueden dejar una huella incluso cuando son rechazadas.

Las partículas del núcleo social son más grandes y de color rojo para transmitir estabilidad y permanencia.

Las partículas del margen son amarillas y rodean el núcleo como una barrera de contención.

Además, el usuario puede modificar la cantidad de partículas de cada población mediante controles deslizantes. Esto permite observar cómo cambia el equilibrio del sistema cuando aumenta o disminuye la creatividad, el poder institucional o la presión social.

# Ficha breve  

## Tensión e intención

**Tensión:** Creatividad individual vs. presión del sistema.

**Intención:** Representar cómo las personas creativas intentan aportar ideas y acercarse al centro de la sociedad, pero encuentran barreras impuestas por las normas y la presión social que limitan o reprimen esa creatividad.



## Tipos y cantidades

| Tipo de partícula | Cantidad | Representa                                         |
| ----------------- | :------: | -------------------------------------------------- |
| Creativas         |    100   | Personas con ideas nuevas e innovadoras.           |
| Núcleo social     |    60    | Instituciones, normas y statu quo.                 |
| Margen            |    90    | Presión social y mecanismos que protegen el orden. |



## Reglas

* Las partículas creativas se mueven rápidamente y buscan acercarse al núcleo.
* El núcleo permanece unido y estable en el centro.
* El margen forma una barrera alrededor del núcleo.
* Cuando las creativas intentan atravesar esa barrera, el margen las rechaza y las obliga a cambiar de dirección.
* Cada ejecución es diferente debido a la aleatoriedad de las posiciones y velocidades iniciales.



## Matriz de relaciones

| **Influye sobre →** | Creativas |  Núcleo |  Margen  |
| ------------------- | :-------: | :-----: | :------: |
| **Creativas**       |  **-0.4** | **0.3** |  **0.1** |
| **Núcleo**          |  **-0.1** | **0.4** |  **0.6** |
| **Margen**          |  **-1.0** | **0.7** | **-0.2** |



## Parámetros y justificación

* **Radio de interacción:** 140 px, para que las relaciones ocurran cuando las partículas están relativamente cerca.
* **Fricción:** 0.88, para obtener movimientos fluidos.
* **Velocidad máxima:**

  * Creativas: **8**
  * Núcleo: **2**
  * Margen: **4.5**
* **Distribución inicial:**

  * Creativas distribuidas aleatoriamente.
  * Núcleo concentrado en el centro.
  * Margen formando un anillo alrededor del núcleo.

**Justificación:** Estos parámetros permiten que el conflicto surja de las reglas del sistema. Las creativas son rápidas y buscan integrarse, el núcleo permanece estable y el margen actúa como una barrera que protege el orden establecido.



## Invariantes y variables

### Invariantes

* Existen siempre tres tipos de partículas.
* Se mantiene la misma matriz de relaciones.
* El núcleo permanece en el centro.
* El margen rodea y protege al núcleo.

### Variables

* Posición inicial de cada partícula.
* Dirección y velocidad inicial.
* Cantidad de partículas mediante el panel de control.

Estas variables hacen que cada simulación sea diferente, pero la tensión entre creatividad y presión social siempre sea reconocible.

## Pruebas  
<img width="1173" height="860" alt="Captura de pantalla 2026-08-04 193902" src="https://github.com/user-attachments/assets/67317739-c9c9-4de2-b8c3-18760feec231" />
<img width="1244" height="883" alt="Captura de pantalla 2026-08-04 193554" src="https://github.com/user-attachments/assets/5068b441-f0ba-4b06-b4a0-81d1bce90039" />
<img width="1256" height="1039" alt="Captura de pantalla 2026-08-04 191831" src="https://github.com/user-attachments/assets/4dd3985c-9435-4082-b740-8aa7d6d97eb3" />
<img width="1255" height="1125" alt="Captura de pantalla 2026-08-04 191638" src="https://github.com/user-attachments/assets/4cf610f9-cdd8-4a40-8337-d2fdff427b56" />
<img width="1241" height="1392" alt="Captura de pantalla 2026-08-04 191252" src="https://github.com/user-attachments/assets/e4c9b190-d244-4342-94e2-cdeca39c83fd" />
<img width="1230" height="1142" alt="Captura de pantalla 2026-08-04 211707" src="https://github.com/user-attachments/assets/d6c85773-a3cd-4d7a-8fe8-7005ae43df08" />
<img width="2545" height="1455" alt="Captura de pantalla 2026-08-04 210814" src="https://github.com/user-attachments/assets/0f736cb0-dd0b-4b7c-8e9c-ab393dadbb24" />
<img width="1117" height="1088" alt="Captura de pantalla 2026-08-04 221642" src="https://github.com/user-attachments/assets/89471839-d247-471c-a649-f36ee8f46dda" />

Al inicio quería hacerlo de las personas valientes y las personas asustadizas a situaciones nuevas pero alió tan mal y aburrido que lo cambié a mi tema actual y descubrí que al poner muchas partículas se me buguea todo

<img width="1106" height="1087" alt="image" src="https://github.com/user-attachments/assets/f8a7f7b1-f703-414e-bdb5-602c584a4fc3" />

# Link  
[Prototipo](https://editor.p5js.org/Ayepes2402/sketches/znMV2QxwN)

# Autoevluación  

| **Criterio**                                                                      | **Peso** |    **Valoración**    | **Aporte / Justificación**                                                                                                                                                                                         |
| --------------------------------------------------------------------------------- | :------: | :------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| La intención es clara y perceptible en el comportamiento.                         |    20%   |       **19/20**      | El comportamiento de las partículas comunica claramente la intención del sistema. En algunos momentos las interacciones pueden verse muy dinámicas, pero la idea general siempre se mantiene.                      |
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. |    25%   |       **24/25**      | La elección de los tipos de partículas, sus cantidades y las relaciones entre ellas responde a la intención conceptual. Los parámetros fueron ajustados mediante pruebas para obtener un comportamiento coherente. |
| Comprendo y puedo modificar el funcionamiento técnico del sistema.                |    20%   |       **19/20**      | Comprendo cómo afectan la matriz, las fuerzas, las distancias y la cantidad de partículas. Puedo modificar estos parámetros para cambiar el comportamiento del sistema sin alterar su lógica principal.            |
| El sistema produce variaciones con una identidad reconocible.                     |    15%   |       **15/15**      | Cada ejecución genera resultados diferentes gracias a la aleatoriedad inicial, pero mantiene una identidad visual y de comportamiento consistente.                                                                 |
| Experimenté, comparé, seleccioné y descarté con criterios claros.                 |    10%   |       **10/10**      | Realicé varias pruebas ajustando cantidades, intensidades y alcances, comparando los resultados hasta encontrar la configuración más adecuada para la intención del proyecto.                                      |
| Puedo distinguir y sustentar lo diseñado y lo emergente.                          |    10%   |       **9/10**       | Puedo identificar qué aspectos fueron definidos desde las reglas del sistema y cuáles aparecen como comportamientos emergentes producto de la interacción entre las partículas.                                    |
| **Total**                                                                         | **100%** | **96/100 (4.8/5.0)** | El sistema cumple con la intención planteada, mantiene coherencia entre sus reglas y el comportamiento observado, y genera variaciones que conservan una identidad reconocible.                                    |

**Nota:** 4.8


