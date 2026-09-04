# Reto 4  

**Link del proyecto**    
[Proyecto](https://ayepes2402.github.io/retop4/)   


Para esta actividad quise hacer una simulación que representara el modelo de Kuramoto de una forma más visual y fácil de entender, por lo tanto hice un jardín nocturno donde hay 8 mariposas que funcionan como osciladores. La idea principal es que cada mariposa tiene su propio ritmo, pero al mismo tiempo puede verse afectada por las demás. Dependiendo de qué tan fuerte sea la conexión entre ellas, pueden pasar de estar completamente desordenadas a empezar a moverse de una manera más coordinada.

También hice que las mariposas interactuaran con las flores y que todo el sistema tuviera sonido, para que la sincronización no solamente se pudiera ver, sino también escuchar.

Mi concepto terminó siendo básicamente:

Un jardín donde cada mariposa tiene su propio ritmo, pero poco a poco las mariposas pueden encontrar un ritmo común. Por otro lado también me inspiré en sky que es un juego bastante relajante y tiene unas mariposas al rededor del mapa.

<img width="3108" height="2160" alt="IMG_6008" src="https://github.com/user-attachments/assets/47dd29f0-ebac-44a0-a5f1-a3e36bc71053" />

**¿Qué hace Kuramoto aquí?**

La parte más importante del proyecto es el modelo de Kuramoto, porque es lo que controla el comportamiento de las mariposas.

Cada mariposa tiene principalmente dos cosas:

θ (theta): representa la fase de la mariposa, o sea, en qué parte de su ciclo se encuentra.
ω (omega): representa su frecuencia natural, es decir, qué tan rápido sigue su propio ritmo.

Además está:

K: representa la fuerza con la que las mariposas se influyen entre ellas.

La ecuación que utilizo es:

<img width="221" height="72" alt="image" src="https://github.com/user-attachments/assets/3ab77d90-c04b-43ff-95d5-f4cc31d41302" />


En palabras más sencillas, cada mariposa intenta seguir su propio ritmo, pero también recibe influencia de las otras. Entonces, si K es bajo, las mariposas tienen más libertad para seguir sus propios ritmos. Si K aumenta, la influencia entre ellas aumenta y empiezan a acercar sus fases. Por eso no estoy usando simplemente un temporizador que diga "todas se mueven ahora". Cada mariposa está calculando su propio comportamiento y después el sistema hace que se influyan entre sí.  

**Las mariposas**  

En el programa tengo 8 mariposas, y cada una funciona como un oscilador. Además, hice diferentes tipos de mariposas dependiendo del tipo de flor que tienen asociado:

* Rosa  
* Girasol  
* Tulipán  
* Lavanda  

Cada tipo tiene valores diferentes de velocidad, movimiento y frecuencia. Esto hace que no todas las mariposas sean exactamente iguales. Por ejemplo, en el código cada tipo tiene:

* speed  
* omega  
* delta  
* wobble  

Estas variables ayudan a que cada grupo tenga pequeñas diferencias en su comportamiento. También cada mariposa empieza con una fase diferente. Esto es importante porque si todas comenzaran exactamente en la misma fase, ya estarían sincronizadas desde el principio y no se podría observar el proceso de organización.

**Elparámetro de orden r**  
Una de las partes más importantes del proyecto es el parámetro de orden R. R sirve para saber qué tan sincronizadas están las mariposas. El código calcula R utilizando las fases de todas las mariposas:

<img width="124" height="64" alt="image" src="https://github.com/user-attachments/assets/da8e29fd-b32d-43f5-a25a-9d3e3fc759b8" />  

No necesito mostrar toda esa fórmula para entender el resultado.

Básicamente:

* R cercano a 0: las mariposas están muy desordenadas.  
* R intermedio: algunas empiezan a organizarse.  
* R cercano a 1: las mariposas están bastante sincronizadas.  

En mi proyecto lo convertí en tres estados:  

**Desorden**  

Cuando: R < 0.38 Las mariposas siguen ritmos muy diferentes.  

**Organización parcial**

Cuando: 0.38 ≤ R < 0.72 Empiezan a aparecer grupos de mariposas que se comportan de manera parecida.

**Sincronización estable**

Cuando: R ≥ 0.72 La mayoría de las mariposas ya está siguiendo un comportamiento bastante coordinado. También hice que la interfaz mostrara este estado y el valor de R en tiempo real.

**¿Cómo se mueven las mariposas?**

Algo que quería evitar era que las mariposas simplemente se movieran de un lado para otro sin relación con el modelo. Por eso hice que su posición dependiera de su fase. En updatePositions() calculo una posición para cada mariposa usando:  

Math.cos()  
Math.sin()  

La fase de Kuramoto entra directamente en estos cálculos.Entonces:  

Kuramoto calcula la fase → la fase cambia → cambia la posición → cambia el movimiento de la mariposa. Esto significa que el comportamiento visual realmente está conectado con el modelo matemático. Además, las mariposas pueden tener diferentes órbitas y movimientos dependiendo de su tipo.

**Las flores**   

También hice diferentes flores para que el jardín tuviera más personalidad. Hay:

* Rosas  
* Girasoles  
* Tulipanes  
* Lavandas  

Las flores no están solamente de decoración, también funcionan como puntos de interacción. Cuando se toca una flor, se produce una perturbación que modifica las fases de las mariposas, esto permite observar qué pasa cuando un sistema que estaba organizado recibe una alteración externa.

**Perturbación de las flores**

Las flores también pueden afectar al sistema. Cuando hago click sobre una flor, el código revisa qué tan cerca está cada mariposa. Dependiendo de esa distancia, se calcula cuánto afecta la perturbación a cada una. Entonces una mariposa que está más cerca de la flor puede recibir una influencia diferente a una que está más lejos. Esto hace que la interacción sea un poco más interesante y evita que todas reciban exactamente el mismo cambio.

**El viento (cursor)**  

Otra interacción que agregué fue el viento. Cuando hago click en un espacio vacío y arrastro el mouse, se activa el viento. El programa calcula la distancia entre el cursor y cada mariposa. Si una mariposa está suficientemente cerca del cursor, su fase cambia. Entonces el viento funciona como otra perturbación externa del sistema. No controla directamente a las mariposas, sino que altera su fase y después el modelo de Kuramoto continúa haciendo su trabajo.

**El sonido**  

También quise relacionar la sincronización con el sonido. Para esto hice una clase llamada GardenAudio, que se encarga de generar el sonido utilizando Web Audio, por lo que no estoy reproduciendo una canción completa ya grabada. Las mariposas generan eventos sonoros dependiendo de su fase y, cuando una mariposa completa su ciclo y su fase vuelve a pasar por el inicio, se genera un evento de sonido. La fase \(\theta\) determina qué nota se utiliza, mientras que el valor de \(R\) afecta el volumen. De esta manera, la fase de cada mariposa determina la nota y la sincronización del grupo determina la intensidad del sonido. Esto hace que el sonido también esté directamente relacionado con el comportamiento matemático del sistema.

**Cada tipo de mariposa tiene su sonido**  

No todas las mariposas producen exactamente el mismo sonido. Dependiendo de su tipo, cada una utiliza diferentes características sonoras. Las mariposas Rosa utilizan un sonido tipo sine, que es más suave y tiene vibrato. Las Girasol también utilizan una onda sine, pero con una frecuencia más alta. Las Tulipán utilizan una onda triangle, lo que hace que tengan un carácter sonoro un poco diferente, mientras que las Lavanda utilizan nuevamente una onda sine, pero con mayor vibrato y un filtro. De esta forma, las diferentes mariposas no solamente se diferencian visualmente, sino también por el sonido que producen.

**La armonía también depende del colectivo**  

Otra parte que me pareció interesante fue hacer que la armonía dependiera del comportamiento colectivo. La clase GardenAudio recibe los valores order y meanPhase. El order corresponde al parámetro de orden \(R\), que representa el nivel de sincronización del grupo, mientras que meanPhase representa la fase promedio de las mariposas. Esta fase media se utiliza para decidir qué acorde tocar, por lo que la música no depende solamente de una mariposa individual, sino también del comportamiento general del grupo. En otras palabras, las mariposas cambian de fase, después se calcula la fase media, esta determina el acorde y finalmente se genera el sonido. Así, el sonido termina siendo otra forma de representar la dinámica del jardín.

**La interfaz**  

También hice una interfaz para poder controlar el sistema y modificar diferentes aspectos del modelo. Uno de los controles principales es K, que representa la fuerza de acoplamiento. Cuando aumento \(K\), las mariposas reciben una mayor influencia entre ellas, lo que puede ayudar a que el sistema se sincronice. También está el control de diversidad de \(\omega\), que modifica qué tan diferentes son las frecuencias naturales de las mariposas. Si existe una mayor diversidad, cada mariposa tiene un ritmo natural más diferente al de las demás. Además, la interfaz cuenta con un control de volumen y botones para activar el sonido, romper la sincronía y reiniciar el sistema. 

**Lo que aprendí haciendo el proyecto**  

Una de las cosas que más entendí haciendo este proyecto es que el modelo de Kuramoto no significa simplemente "hacer que todos se muevan juntos". La gracia está precisamente en que cada individuo tiene su propio comportamiento, pero existe una interacción entre ellos. Por eso el parámetro \(K\) es tan importante. Al principio puede parecer que solamente estoy moviendo mariposas utilizando sin() y cos(), pero realmente estas funciones se utilizan para convertir las fases calculadas por Kuramoto en un movimiento que se pueda observar. También entendí mejor la importancia de \(R\), porque permite convertir algo matemático en algo visual. No tengo que mirar solamente la ecuación para saber qué está pasando, sino que puedo observar cómo el sistema pasa de DESORDEN → ORGANIZACIÓN PARCIAL → SINCRONIZACIÓN ESTABLE, mientras el valor de \(R\) también cambia.

**Errores, crisis y experimentación**  

Una de las cosas que más tuve que revisar fue que las perturbaciones no reemplazaran el modelo de Kuramoto. Al principio podría ser fácil simplemente cambiar las posiciones de las mariposas y decir que se desordenaron, pero eso no demostraría realmente el funcionamiento del modelo. Por eso hice que las perturbaciones modificaran principalmente las fases. Después de una perturbación, el sistema vuelve a utilizar normalmente la ecuación de Kuramoto:

<img width="215" height="70" alt="image" src="https://github.com/user-attachments/assets/ab0bbd3e-2418-4ffd-bdb8-995146d3de23" />

De esta manera puedo demostrar que, después de una perturbación, el sistema sigue funcionando mediante las mismas reglas de interacción. También tuve que hacer diferentes pruebas con el valor de \(K\) para encontrar un punto donde realmente se pudiera observar la diferencia entre el desorden y la sincronización. Si el acoplamiento es muy bajo, las mariposas pueden mantenerse demasiado separadas, mientras que si es más fuerte empiezan a aparecer comportamientos colectivos.

**¿Qué pasa cuando todo se sincroniza?**   

Esta es probablemente la parte más bonita de ver. Cuando el sistema está desordenado, cada mariposa parece seguir su propio ritmo, pero cuando el acoplamiento empieza a funcionar, algunas comienzan a acercarse en fase. Después aparecen grupos y, finalmente, cuando \(R\) es suficientemente alto, se puede observar que gran parte del grupo está siguiendo un comportamiento parecido. Visualmente, el sistema pasa de un DESORDEN, donde cada mariposa va por su lado, a un estado PARCIAL, donde aparecen pequeños grupos, y finalmente a un estado ESTABLE, donde las mariposas empiezan a actuar juntas. Todo esto surge de las fases y de la interacción entre los osciladores.

**Parte de Three.js y partículas**  

Además del jardín de mariposas, hice una parte de simulación de partículas utilizando Three.js WebGPU y TSL. Para esto tengo dos buffers principales, positionBuffer y velocityBuffer. Uno guarda la posición de cada partícula y el otro guarda su velocidad. La simulación funciona de una manera parecida a un sistema de posición + velocidad → fuerzas → nueva velocidad → nueva posición. Entre las fuerzas que se pueden activar están la fuerza constante o viento, la atracción, la repulsión, el vórtice y la resistencia o drag. Por ejemplo, la fuerza radial puede atraer o alejar las partículas dependiendo del valor de radialStrength, mientras que el vórtice hace que tengan un movimiento circular alrededor de un eje. El drag funciona como una resistencia que reduce la velocidad y también existe una velocidad máxima para evitar que las partículas se muevan demasiado rápido.

**Pruebas de fuerzas** 

En el panel de laboratorio dejé diferentes pruebas para poder comprobar el comportamiento de las fuerzas. Estas pruebas corresponden a 1 · Inercia, 2 · Fuerza constante +X, 3 · Atracción, 4 · Repulsión y 5 · Vórtice. La idea es que antes de ejecutar cada prueba pueda pensar qué debería pasar y después compararlo con lo que realmente ocurre. Esto me ayuda a comprobar que las fuerzas están funcionando correctamente y que el comportamiento observado corresponde con lo esperado.

AUTOEVALUACIÓN 
Leí y revisé que mi proyecto cumple con los requisitos mínimos de la unidad: 25 puntos.  
Considero que todavía debo mejorar mi capacidad para explicar con claridad qué representa cada variable del modelo de Kuramoto: 20 puntos.  
Considero que todavía debo mejorar la explicación de cómo las variables del modelo producen el comportamiento observado en las mariposas: 20 puntos.  
Puedo demostrar que mi proyecto utiliza la sincronización, las perturbaciones y el parámetro de orden para mostrar el comportamiento del sistema: 25 puntos.  

NOTA: 90/100 = 4.5  

**Algunas capturas de los chats y del proyecto**  
<img width="1277" height="800" alt="Captura de pantalla 2026-09-03 153110" src="https://github.com/user-attachments/assets/b324b008-9e52-463a-b432-adc3713501f1" />
<img width="1280" height="749" alt="Captura de pantalla 2026-09-03 195003" src="https://github.com/user-attachments/assets/918be46b-55be-4abe-92c9-ac76cd94438a" />
<img width="569" height="707" alt="Captura de pantalla 2026-09-03 193038" src="https://github.com/user-attachments/assets/e71f3346-e65f-4003-ae54-11494dfd217b" />
<img width="620" height="247" alt="Captura de pantalla 2026-09-03 153141" src="https://github.com/user-attachments/assets/f9b37a63-f8e9-4dac-b9f2-c19748d9c112" />
<img width="655" height="436" alt="Captura de pantalla 2026-09-03 153133" src="https://github.com/user-attachments/assets/7e026e69-b304-48ad-addd-6774020562d3" />
