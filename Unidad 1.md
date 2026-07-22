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

