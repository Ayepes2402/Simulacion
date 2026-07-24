# Unidad 1
## Actividad 1 y 2
*Cambio de color y forma*  
```js
show() {
    stroke(44, 21, 84);
    square(this.x, this.y,40);
```
<img width="609" height="226" alt="image" src="https://github.com/user-attachments/assets/99210562-b0f0-4faa-a2fe-760fee042706" />  

## Actividad 3
**En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.**  

La distribución uniforme no tiene numero preferido y la probabilidad es repartida uniformemente y la no unifome es lo contrario 

**Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.**    
  ```js
 step() {
    const choice = floor(random(4));
   if (choice < 0.4) {
      this.x++;
    } else if (choice < 0.6) {
      this.x--;
    } else if (choice < 2) {
      this.y++;
    } else if (choice > 2) {
      this.y--;
    }
```
<img width="604" height="219" alt="image" src="https://github.com/user-attachments/assets/5e8d7d00-4748-4cb2-9bea-be88f8606e5e" />  


## Actividad 4  
**Crea un nuevo sketch en p5.js que represente una distribución normal, pero visualizándola de manera diferente a la del ejemplo.**  

 ```js
function setup() {
  createCanvas(400, 400);
  background(240);
}

function draw() {
  let x = random(width);
  let y = random(height);
  let s = abs(randomGaussian(20, 8));

  noStroke();
  fill(100, 150, 255, 100);
  circle(x, y, s);
}
```
<img width="298" height="299" alt="image" src="https://github.com/user-attachments/assets/a558cdff-24f4-4d83-a4f0-53885eada5d8" />   

Aquí se usa la distribución normal para controlar el tamaño de los círculos en lugar de su posición. Así los círculos aparecen en posiciones aleatorias, pero la mayoría tendrán un tamaño parecido y solo unos pocos serán muy pequeños o muy grandes.  

## Actividad 5
**Explica por qué usaste esta técnica y qué resultados esperabas obtener.**  

```js
let walker;

function setup() {
  createCanvas(400, 400);
  background(255);
  walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    noStroke();
    fill(147, 70, 255, 40); // Morado estilo Vegetta777
    circle(this.x, this.y, 8);
  }

  step() {
    let angle = random(TWO_PI);
    let stepSize;

   
    if (random(1) < 0.05) {
      stepSize = random(40, 80);
    } else {
      stepSize = random(1, 3);
    }

    this.x += cos(angle) * stepSize;
    this.y += sin(angle) * stepSize;


    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}
```

<img width="289" height="287" alt="image" src="https://github.com/user-attachments/assets/e50d8d21-8466-4714-95e3-ac3e1ec16bbb" />   

**Explica por qué usaste esta técnica y qué resultados esperabas obtener.**   

Al comienzo me costó un poco entender cómo usar el Lévy flight, así que empecé haciendo pruebas. Al final decidí mantener la idea de un punto que se mueve por la pantalla, pero cambié la forma en la que avanza para que casi siempre diera pasos cortos y solo algunas veces hiciera un salto largo. Con eso buscaba que el recorrido se viera más dinámico y diferente a un movimiento completamente aleatorio.

## Actividad 6  
**Crea un nuevo sketch en p5.js donde los visualices.**  
```js
let t = 0;
let walker;

function setup() {
  createCanvas(400, 400);
  background(255);
  walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = 0;
    this.y = height / 2;
  }

  show() {
    noStroke();
    fill(120, 70, 255, 40);
    circle(this.x, this.y, 10);
  }

  step() {
    let velocidad = map(noise(t), 0, 1, 1, 5);
    this.x += velocidad;

 
    this.y = map(noise(t + 50), 0, 1, 120, 280);

    if (this.x > width) {
      this.x = 0;
      background(255);
    }

    t += 0.02;
  }
}
```
<img width="289" height="236" alt="image" src="https://github.com/user-attachments/assets/a8cf95b9-c936-4151-83ce-8447f3243b8b" />  
  

**Explica por qué lo visualizaste de esa manera y qué resultados esperabas obtener.**  

Quise usar el ruido Perlin para que el movimiento del punto no fuera siempre igual. Por eso hice que cambiara tanto la velocidad como la altura de forma suave mientras avanzaba por la pantalla. Esperaba que el recorrido se viera más natural y continuo, mostrando cómo el ruido Perlin genera cambios progresivos en lugar de movimientos bruscos.

## Actividad 7 Reto de diseño  
Como la contaminación y el cambio climático están afectando al planeta, especialmente a los polos, quiero crear una experiencia interactiva que muestre cómo estos ecosistemas pueden cambiar con el paso del tiempo.

La idea es representar cómo el deterioro puede avanzar rápidamente, pero también cómo eventos poco probables y las acciones humanas pueden ayudar a que el ecosistema se recupere lentamente. Con esto busco generar conciencia sobre cómo nuestras decisiones actuales pueden influir en el futuro del planeta.
**"A destruccion de un ecosistema es mucho mas rapida que su recuperacion"**

**Posibilidad:**
El ecosistema tiene diferentes futuros posibles. Puede seguir deteriorándose con el paso del tiempo o puede encontrar una forma de recuperarse dependiendo de los eventos que ocurran.

**Tendencia:**
La mayoría de las veces el ecosistema sigue una dirección de destrucción debido a los cambios negativos que se acumulan poco a poco. Estos pequeños daños hacen que con los años el ambiente pierda su equilibrio.

**Normalidad:**
Lo más común es que el ecosistema continúe su proceso normal de deterioro, donde el paso del tiempo representa cómo los daños se acumulan y afectan cada vez más la vida del lugar.

**Excepción:**
Algunos eventos poco probables pueden cambiar el futuro del ecosistema. Estas situaciones representan momentos de esperanza donde la naturaleza puede recuperarse y volver a crecer poco a poco.

**Influencia:**
La interacción del visitante representa la ayuda humana para proteger el ecosistema. Al intervenir, el tiempo avanza más lento, mostrando que recuperar la naturaleza toma mucho más tiempo y esfuerzo que destruirla.

**Ideas descartadas**  
Antes de hacer este me quise ir por el lado de las gemas y queria hacer como unas geodas pero no funcionaron bien y salian bien feas entonces mejor descarte la idea por lo triste que quedé al verla  
<img width="421" height="359" alt="Captura de pantalla 2026-07-23 201304" src="https://github.com/user-attachments/assets/3ef41ff8-9efc-47f8-80a7-53d07936cf9f" />  

Despues en vez de geodas traté con el crecimiento Dendrítico (Copos / Minerales de Manganeso) pero tampoco me gustó y sentí que era o muy básico o no cumplia con lo pedido  
<img width="272" height="227" alt="Captura de pantalla 2026-07-23 203036" src="https://github.com/user-attachments/assets/c6271ed8-211c-4ac9-b5cd-39024ad8938b" />  
<img width="290" height="295" alt="Captura de pantalla 2026-07-23 203118" src="https://github.com/user-attachments/assets/7452f994-75e1-46ff-a0e8-29a086fbf56e" />  
<img width="269" height="266" alt="Captura de pantalla 2026-07-23 203551" src="https://github.com/user-attachments/assets/f51bcaa2-f525-4f62-b0d3-bc6d122c1b44" />  
**Referencia del ultimo**  
<img width="287" height="216" alt="image" src="https://github.com/user-attachments/assets/11d947c8-c332-4bc1-8268-10fd4e6bd3d7" />  

Luego intenté con el cerebro pero tampoco funcionó y no me gustó, se podría decir que se veia bien pero ya de ahí no mucho más  
<img width="286" height="437" alt="Captura de pantalla 2026-07-23 204213" src="https://github.com/user-attachments/assets/46c08320-1143-4692-b906-54498d7bba5d" />  

**Experimentos y versiones intermedias**  
Las primeras versiones de código tenian medianamente la idea pero se veian bastante mal visualmente y tenian cosas que sobraban y otras que funcionaban, por ejemplo al inicio la idea era que la persona fuera la que derritiera más rapido el iceberg y que dejar el mouse fuera lo hiciera recuperar, eso funcionaba pero a que costo? a que se viera horrible  

<img width="331" height="554" alt="Captura de pantalla 2026-07-23 220342" src="https://github.com/user-attachments/assets/ae30190d-d9ff-472a-8c80-d5f77004e9e9" />  

Despues de eso seguí peleando con la ia como buena guerrera que soy y me fue peor, ya no tenia lo del calentamiento y solo era un iceberg moviendose sin mas  

<img width="331" height="526" alt="Captura de pantalla 2026-07-23 213626" src="https://github.com/user-attachments/assets/3f921760-0e18-425d-a15b-7ce9b6af32f8" />  

Despues perdió hasta la forma y no parecía nada  
<img width="293" height="330" alt="Captura de pantalla 2026-07-23 213718" src="https://github.com/user-attachments/assets/99e66c58-83fd-44fc-8c17-6a6732706615" />  
<img width="296" height="311" alt="Captura de pantalla 2026-07-23 214019" src="https://github.com/user-attachments/assets/10898903-8f26-4338-ad6e-3108f96883f6" />  
<img width="320" height="374" alt="Captura de pantalla 2026-07-23 213807" src="https://github.com/user-attachments/assets/67be393a-9d1d-4d0c-b0f8-3077e68c0d2e" />











