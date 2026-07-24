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
<a name="ej1"></a>
Como la contaminación y el cambio climático están afectando al planeta, especialmente a los polos, quiero crear una experiencia interactiva que muestre cómo estos ecosistemas pueden cambiar con el paso del tiempo.

La idea es representar cómo el deterioro puede avanzar rápidamente, pero también cómo eventos poco probables y las acciones humanas pueden ayudar a que el ecosistema se recupere lentamente. Con esto busco generar conciencia sobre cómo nuestras decisiones actuales pueden influir en el futuro del planeta.
**"La destruccion de un ecosistema es mucho mas rapida que su recuperacion"**

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

Ya despues de muchos intentos por fin logré un código decente  
```js
let hielo = 100;
let temperatura = 0; // 0 = frío polar, 100 = calor extremo
let particulas = [];

function setup() {
  createCanvas(800, 500);
  noCursor(); // Ocultamos el cursor normal para crear un efecto de "halo de calor" personalizado
}

function draw() {
  // 1. CIELO DINÁMICO (Cambia de un azul aurora boreal a un tono naranja/rojo por el calor)
  let r = map(temperatura, 0, 100, 135, 230);
  let g = map(temperatura, 0, 100, 206, 120);
  let b = map(temperatura, 0, 100, 250, 80);
  background(r, g, b);

  // Estrellas sutiles o partículas de aire frío si hay poco calor
  if (temperatura < 40) {
    fill(255, 150);
    noStroke();
    ellipse(random(width), random(height / 2), 2, 2);
  }

  // 2. OCÉANO (Crece a medida que el hielo disminuye)
  let alturaOcean = map(hielo, 100, 0, 150, 320);
  fill(14, 116, 144);
  noStroke();
  rect(0, height - alturaOcean, width, alturaOcean);

  // Reflejos suaves en el agua
  fill(6, 182, 212, 100);
  rect(0, height - alturaOcean, width, 10);

  // 3. EL GLACIAR (Estructura poligonal y elegante que se derrite)
  let alturaGlaciar = map(hielo, 0, 100, 10, 220);
  
  // Dibujar capas de hielo con transparencias para dar profundidad
  fill(224, 242, 254, 230);
  beginShape();
  vertex(100, height - alturaOcean);
  vertex(200, height - alturaOcean - alturaGlaciar * 0.8);
  vertex(350, height - alturaOcean - alturaGlaciar);
  vertex(500, height - alturaOcean - alturaGlaciar * 0.9);
  vertex(650, height - alturaOcean - alturaGlaciar * 0.4);
  vertex(750, height - alturaOcean);
  endShape(CLOSE);

  // 4. FAUNA VULNERABLE (Un tierno oso polar o pingüino que depende del hielo)
  if (hielo > 15) {
    fill(255);
    // Pequeño oso polar estático sobre el hielo
    let xOso = 350;
    let yOso = height - alturaOcean - alturaGlaciar - 15;
    ellipse(xOso, yOso, 35, 25); // Cuerpo
    ellipse(xOso + 12, yOso - 10, 18, 18); // Cabeza
    fill(0);
    ellipse(xOso + 18, yOso - 12, 3, 3); // Ojo
  }

  // 5. INFLUENCIA DEL CURSOR (El calor humano al pasar por encima)
  // Calculamos si el mouse se está moviendo sobre el área del glaciar
  let distanciaAlGlaciar = dist(mouseX, mouseY, width / 2, height - 200);
  
  if (mouseY < height - 100 && mouseY > 50) {
    // Al pasar el mouse, generamos calor y partículas de vapor/derretimiento
    temperatura = min(100, temperatura + 0.3);
    hielo = max(0, hielo - 0.25);
    
    // Crear partículas visuales de calor/agua
    if (frameCount % 3 === 0) {
      particulas.push({
        x: mouseX + random(-10, 10),
        y: mouseY + random(-10, 10),
        alpha: 255
      });
    }
  } else {
    // Tendencia natural: se recupera poquísimo si no hay humanos, pero el calor base persiste
    temperatura = max(0, temperatura - 0.05);
  }

  // Dibujar y actualizar partículas de calor del cursor
  for (let i = particulas.length - 1; i >= 0; i--) {
    let p = particulas[i];
    fill(255, 255, 255, p.alpha);
    noStroke();
    ellipse(p.x, p.y, 6, 6);
    p.y -= 1; // Suben como vapor
    p.alpha -= 10;
    if (p.alpha <= 0) {
      particulas.splice(i, 1);
    }
  }

  // 6. CURSOR PERSONALIZADO (Halo de calor humano)
  noFill();
  stroke(255, 80, 80, 150);
  strokeWeight(3);
  ellipse(mouseX, mouseY, 40, 40);
  fill(255, 100, 100, 50);
  noStroke();
  ellipse(mouseX, mouseY, 25, 25);

  // 7. PANEL DE INTERFAZ ESTÉTICA
  fill(15, 23, 42, 210);
  noStroke();
  rect(width / 2 - 250, 20, 500, 50, 25);

  fill(255);
  textAlign(CENTER, CENTER);
  textSize(14);
  text(`Calor Humano: ${temperatura.toFixed(0)}%  |  Masa Polar: ${hielo.toFixed(1)}%`, width / 2, 45);

  // Mensaje final poético
  if (hielo <= 0) {
    fill(15, 23, 42, 230);
    rect(0, 0, width, height);
    fill(255, 100, 100);
    textSize(28);
    text("El ecosistema ha colapsado.", width / 2, height / 2 - 20);
    fill(255);
    textSize(16);
    text("Nuestra presencia invisible dejó huella. El futuro depende de nuestras decisiones.", width / 2, height / 2 + 25);
  } else {
    // Texto guía inferior
    fill(255, 220);
    textSize(13);
    text("Pasa el cursor suavemente sobre la pantalla para sentir la influencia del ser humano en el clima.", width / 2, height - 25);
  }
}
````
En este al menos ya estaba el iceberg, el agua y un animal y ya al menos tenia forma chajaja  
<img width="589" height="357" alt="Captura de pantalla 2026-07-23 220739" src="https://github.com/user-attachments/assets/1610b7b2-f4ce-408f-9225-b765adb9513e" />  

Despues lo intente cambiar para que tuviera al menos tres conceptos de la unidad añadiendo probabilidades en el iceberg, copos de nieve, al derretir hielo y al salvarlo  
````js
let hielo = 80;
let temperatura = 30;
let particulas = [];
let tPerlin = 0;
let walkX = 225; // Caminata aleatoria constante para la Tendencia

function setup() {
  createCanvas(450, 800); // Formato vertical 9:16
  noCursor();
}

function draw() {
  // 1. CONCEPTO 1: RUIDO PERLIN (Clima base constante, continuo y autónomo)
  tPerlin += 0.004;
  let climaRuido = noise(tPerlin);

  let mouseDentro = (mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height);
  let influenciaActiva = mouseDentro && (mouseY < height - 100 && mouseY > 50);

  // Inercia térmica: La temperatura evoluciona de forma fluida y orgánica
  let tempBase = map(climaRuido, 0, 1, 15, 60);
  
  if (influenciaActiva) {
    // Al interactuar, el calor sube de manera sostenida
    temperatura += (85 - temperatura) * 0.04;
  } else {
    // Sin interacción, busca el clima base del ruido Perlin lentamente
    temperatura += (tempBase - temperatura) * 0.02;
  }
  temperatura = constrain(temperatura, 10, 95);

  // COMPORTAMIENTO ASIMÉTRICO DE DESHIELO Y RECUPERACIÓN (Derretimiento más rápido)
  if (temperatura > 45) {
    // El hielo se reduce más rápido de manera proporcional al exceso de calor
    hielo -= (temperatura - 45) * 0.0038;
  } else {
    // Recuperar hielo es un proceso sumamente lento y acumulativo (no un rebote instantáneo)
    hielo += (45 - temperatura) * 0.0004;
  }
  hielo = constrain(hielo, 5, 95);

  // CIELO DINÁMICO
  let r = map(temperatura, 0, 100, 120, 225);
  let g = map(temperatura, 0, 100, 190, 105);
  let b = map(temperatura, 0, 100, 240, 65);
  background(r, g, b);

  // MOMENTO - POSIBILIDAD Y NORMALIDAD: Uso de randomGaussian() para que la mayoría 
  // de las trayectorias permanezcan cerca de lo habitual (distribución en campana alrededor de walkX)
  if (random(1) < 0.3) {
    let xNormal = walkX + randomGaussian(0, 50);
    xNormal = constrain(xNormal, 20, width - 20);
    particulas.push({
      x: xNormal,
      y: random(height * 0.4),
      vx: random(-1.5, 1.5),
      vy: random(-1.5, 1.5),
      tipo: 'posibilidad',
      alpha: random(80, 200)
    });
  }

  // MOMENTO - EXCEPCIÓN: Evento improbable que descubre un territorio nuevo
  if (random(1) < 0.005) {
    particulas.push({
      x: random(width),
      y: random(height * 0.5, height * 0.75),
      vx: random(-3, 3),
      vy: random(-2, 2),
      tipo: 'excepcion',
      alpha: 255
    });
  }

  // 2. CONCEPTO 2: CAMINATA ALEATORIA (Tendencia constante y suave)
  if (frameCount % 20 === 0) {
  if (random(1) < 0.6) {
    walkX += random(1, 4);
  } else {
    walkX -= random(1, 4);
  }
}

walkX = constrain(walkX, 90, width - 90);

  // OCÉANO
  let alturaOcean = map(hielo, 100, 0, 180, 500);
  fill(14, 116, 144, 230);
  noStroke();
  rect(0, height - alturaOcean, width, alturaOcean);

  // 3. CONCEPTO 3: DISTRIBUCIÓN NORMAL (Normalidad: estructura estable y armónica del glaciar)
  let alturaGlaciar = map(hielo, 0, 100, 10, 310);
  
  fill(224, 242, 254, 235);
  beginShape();
  vertex(40, height - alturaOcean);
  vertex(120, height - alturaOcean - alturaGlaciar * 0.8);
  vertex(walkX, height - alturaOcean - alturaGlaciar);
  vertex(330, height - alturaOcean - alturaGlaciar * 0.85);
  vertex(410, height - alturaOcean);
  endShape(CLOSE);

  // FAUNA VULNERABLE (Pingüino)
  if (hielo > 10) {
    let xP = walkX;
    let yP = height - alturaOcean - alturaGlaciar - 14;
    
    // Cuerpo negro
    fill(30, 41, 59);
    ellipse(xP, yP, 20, 26);
    
    // Vientre blanco
    fill(255);
    ellipse(xP, yP + 2, 12, 18);
    
    // Cabeza
    fill(30, 41, 59);
    ellipse(xP, yP - 12, 14, 14);
    
    // Pico naranja
    fill(249, 115, 22);
    triangle(xP + 5, yP - 13, xP + 11, yP - 11, xP + 5, yP - 9);
    
    // Ojo
    fill(255);
    ellipse(xP + 3, yP - 13, 3, 3);
    fill(0);
    ellipse(xP + 4, yP - 13, 1.5, 1.5);
  }

  // Actualización constante de partículas
  for (let i = particulas.length - 1; i >= 0; i--) {
    let p = particulas[i];
    if (p.tipo === 'excepcion') {
      fill(250, 204, 21, p.alpha);
      ellipse(p.x, p.y, 5, 5);
    } else if (p.tipo === 'influencia') {
      fill(255, 120, 120, p.alpha);
      ellipse(p.x, p.y, 4, 4);
    } else {
      fill(255, p.alpha);
      ellipse(p.x, p.y, 3, 3);
    }

    p.x += p.vx;
    p.y += p.vy;
    p.alpha -= 4.5;

    if (p.alpha <= 0) {
      particulas.splice(i, 1);
    }
  }

  // Emisión por influencia directa del visitante
  if (influenciaActiva) {
    if (frameCount % 3 === 0) {
      particulas.push({
        x: mouseX + random(-8, 8),
        y: mouseY + random(-8, 8),
        vx: random(-0.5, 0.5),
        vy: random(-2, -0.8),
        tipo: 'influencia',
        alpha: 220
      });
    }
  }

  // CURSOR PERSONALIZADO (Solo visible dentro del canvas)
  if (mouseDentro) {
    noFill();
    stroke(255, 90, 90, 160);
    strokeWeight(2.5);
    ellipse(mouseX, mouseY, 35, 35);
    fill(255, 100, 100, 45);
    noStroke();
    ellipse(mouseX, mouseY, 20, 20);
  }

  // PANEL DE INTERFAZ 9:16
  fill(15, 23, 42, 210);
  noStroke();
  rect(width / 2 - 160, 25, 320, 42, 20);

  fill(255);
  textAlign(CENTER, CENTER);
  textSize(12);
  text(`Temperatura: ${temperatura.toFixed(0)}% | Hielo: ${hielo.toFixed(1)}%`, width / 2, 46);

  // Texto guía inferior
  fill(255, 190);
  textSize(11);
  text("Perlin, Caminata Aleatoria y Distribución Normal", width / 2, height - 25);
}
````
<img width="322" height="584" alt="image" src="https://github.com/user-attachments/assets/f83ccee6-3d18-4ccd-b0b2-36178a20c699" />  

Despues de esto decidí cambiar mi idea para que en vez de que el humano derritiera el hielo mejor lo salvara y que cuando se esté derritiendo los años pasen más rapido mientras que cuando intentes salvarlo va mas lento debido a que La destruccion de un ecosistema es mucho mas rapida que su recuperacion y así nació mi super código final yupiii  
<a name="ej3"></a>
````js
let hielo = 80;
let temperatura = 30;
let particulas = [];
let tPerlin = 0;
let walkX = 225; // Caminata aleatoria constante para la Tendencia
let anioDecimal = 2026; // Contador de años desde el presente

function setup() {
  createCanvas(450, 800); // Formato vertical 9:16
  noCursor();
}

function draw() {
  // 1. CONCEPTO 1: RUIDO PERLIN (Clima base constante, continuo y autónomo)
  tPerlin += 0.004;
  let climaRuido = noise(tPerlin);

  let mouseDentro = (mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height);
  let influenciaActiva = mouseDentro && (mouseY < height - 100 && mouseY > 50);

  // Control del tiempo (Años): La destrucción del ecosistema es veloz, 
  // pero al interactuar el tiempo va más lento (señal de que la recuperación requiere esfuerzo sostenido)
  if (influenciaActiva) {
    anioDecimal += 0.005; // El tiempo avanza lento durante la interacción
    hielo += 0.002;       // Sanación muy sutil y lenta en comparación con el deterioro
  } else {
    anioDecimal += 0.03;  // El tiempo avanza rápido (destrucción natural acelerada)
    hielo -= 0.012;       // El ecosistema se degrada de manera notable
  }
  hielo = constrain(hielo, 5, 95);

  // Inercia térmica
  let tempBase = map(climaRuido, 0, 1, 20, 70);
  
  if (influenciaActiva) {
    temperatura += (40 - temperatura) * 0.04;
  } else {
    temperatura += (tempBase - temperatura) * 0.02;
  }
  temperatura = constrain(temperatura, 10, 95);

  // CIELO DINÁMICO
  let r = map(temperatura, 0, 100, 120, 225);
  let g = map(temperatura, 0, 100, 190, 105);
  let b = map(temperatura, 0, 100, 240, 65);
  background(r, g, b);

  // MOMENTO - POSIBILIDAD Y NORMALIDAD (Uso de randomGaussian alrededor de walkX)
  if (random(1) < 0.3) {
    let xNormal = walkX + randomGaussian(0, 50);
    xNormal = constrain(xNormal, 20, width - 20);
    particulas.push({
      x: xNormal,
      y: random(height * 0.4),
      vx: random(-1.5, 1.5),
      vy: random(-1.5, 1.5),
      tipo: 'posibilidad',
      alpha: random(80, 200)
    });
  }

  // MOMENTO - EXCEPCIÓN: Evento improbable que en lugar de destruir, hace que el ecosistema se recupere un poco
  let probabilidadRecuperacion = influenciaActiva ? 0.02 : 0.003;

if (random(1) < probabilidadRecuperacion) {
  hielo = min(95, hielo + 1);

  particulas.push({
    x: random(width),
    y: random(height * 0.5, height * 0.75),
    vx: random(-3, 3),
    vy: random(-2, 2),
    tipo: 'excepcion',
    alpha: 255
  });
}

  // 2. CONCEPTO 2: CAMINATA ALEATORIA (Tendencia constante y suave)
  // 2. CONCEPTO 2: CAMINATA ALEATORIA CON TENDENCIA
if (frameCount % 20 === 0) {
  if (random(1) < 0.6) {
    walkX += random(1, 4); // pequeña preferencia hacia la derecha
  } else {
    walkX -= random(1, 4); // movimiento contrario menos frecuente
  }
}

walkX = constrain(walkX, 90, width - 90);

  // OCÉANO
  let alturaOcean = map(hielo, 100, 0, 180, 500);
  fill(14, 116, 144, 230);
  noStroke();
  rect(0, height - alturaOcean, width, alturaOcean);

  // 3. CONCEPTO 3: DISTRIBUCIÓN NORMAL (Normalidad: estructura estable y armónica del glaciar)
  let alturaGlaciar = map(hielo, 0, 100, 10, 310);
  
  fill(224, 242, 254, 235);
  beginShape();
  vertex(40, height - alturaOcean);
  vertex(120, height - alturaOcean - alturaGlaciar * 0.8);
  vertex(walkX, height - alturaOcean - alturaGlaciar);
  vertex(330, height - alturaOcean - alturaGlaciar * 0.85);
  vertex(410, height - alturaOcean);
  endShape(CLOSE);

  // FAUNA VULNERABLE (Pingüino)
  if (hielo > 10) {
    let xP = walkX;
    let yP = height - alturaOcean - alturaGlaciar - 14;
    
    // Cuerpo negro
    fill(30, 41, 59);
    ellipse(xP, yP, 20, 26);
    
    // Vientre blanco
    fill(255);
    ellipse(xP, yP + 2, 12, 18);
    
    // Cabeza
    fill(30, 41, 59);
    ellipse(xP, yP - 12, 14, 14);
    
    // Pico naranja
    fill(249, 115, 22);
    triangle(xP + 5, yP - 13, xP + 11, yP - 11, xP + 5, yP - 9);
    
    // Ojo
    fill(255);
    ellipse(xP + 3, yP - 13, 3, 3);
    fill(0);
    ellipse(xP + 4, yP - 13, 1.5, 1.5);
  }

  // Actualización constante de partículas
  for (let i = particulas.length - 1; i >= 0; i--) {
    let p = particulas[i];
    if (p.tipo === 'excepcion') {
      fill(250, 204, 21, p.alpha);
      ellipse(p.x, p.y, 5, 5);
    } else if (p.tipo === 'influencia') {
      fill(255, 120, 120, p.alpha);
      ellipse(p.x, p.y, 4, 4);
    } else {
      fill(255, p.alpha);
      ellipse(p.x, p.y, 3, 3);
    }

    p.x += p.vx;
    p.y += p.vy;
    p.alpha -= 4.5;

    if (p.alpha <= 0) {
      particulas.splice(i, 1);
    }
  }

  // Emisión por influencia directa del visitante
  if (influenciaActiva) {
    if (frameCount % 3 === 0) {
      particulas.push({
        x: mouseX + random(-8, 8),
        y: mouseY + random(-8, 8),
        vx: random(-0.5, 0.5),
        vy: random(-2, -0.8),
        tipo: 'influencia',
        alpha: 220
      });
    }
  }

  // CURSOR PERSONALIZADO (Solo visible dentro del canvas)
  if (mouseDentro) {
    noFill();
    stroke(255, 90, 90, 160);
    strokeWeight(2.5);
    ellipse(mouseX, mouseY, 35, 35);
    fill(255, 100, 100, 45);
    noStroke();
    ellipse(mouseX, mouseY, 20, 20);
  }

  // PANEL DE INTERFAZ 9:16
  fill(15, 23, 42, 210);
  noStroke();
  rect(width / 2 - 160, 25, 320, 42, 20);

  fill(255);
  textAlign(CENTER, CENTER);
  textSize(12);
  text(`Año: ${Math.floor(anioDecimal)} | Hielo: ${hielo.toFixed(1)}%`, width / 2, 46);

  // Texto guía inferior
  fill(255, 190);
  textSize(11);
  text("Perlin, Caminata Aleatoria y Distribución Normal", width / 2, height - 25);
}
````

**Para hacerlo más estetico claude me ayudó a mejorar el diseño y así se ve más pro**  
````js
// ---------------------------------------------------------------
// PALETA (tokens)
// ---------------------------------------------------------------
// Noche polar   #0B1D3A   -> cielo frío, alto hielo
// Colapso       #C0392B   -> cielo cálido, bajo hielo
// Hielo         #E8F6FF   -> glaciar / acentos claros
// Océano        #0E4C5C -> #1B7A8C
// Aurora        #7FE7C4   -> elemento distintivo, solo con hielo alto
// Sol/luz cálida #FFD27A
// Tinta panel   #0A1220

let hielo = 80;
let temperatura = 30;
let particulas = [];
let tPerlin = 0;
let walkX = 225;
let anioDecimal = 2026;

function setup() {
  const c = createCanvas(450, 800);
  c.parent(document.querySelector('main'));
  noCursor();
  angleMode(RADIANS);
  colorMode(RGB, 255, 255, 255, 255);
}

function draw() {
  // -------------------------------------------------------------
  // 1. RUIDO PERLIN — clima base continuo
  // -------------------------------------------------------------
  tPerlin += 0.004;
  let climaRuido = noise(tPerlin);

  let mouseDentro = (mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height);
  let influenciaActiva = mouseDentro && (mouseY < height - 100 && mouseY > 50);

  if (influenciaActiva) {
    anioDecimal += 0.005;
    hielo += 0.002;
  } else {
    anioDecimal += 0.03;
    hielo -= 0.012;
  }
  hielo = constrain(hielo, 5, 95);

  let tempBase = map(climaRuido, 0, 1, 20, 70);
  if (influenciaActiva) {
    temperatura += (40 - temperatura) * 0.04;
  } else {
    temperatura += (tempBase - temperatura) * 0.02;
  }
  temperatura = constrain(temperatura, 10, 95);

  // -------------------------------------------------------------
  // CIELO — degradado multi-stop según temperatura (frío -> cálido)
  // -------------------------------------------------------------
  drawSky(temperatura);

  // Aurora: elemento distintivo, se intensifica con más hielo (recompensa visual de sanar el ecosistema)
  drawAurora(hielo, temperatura);

  // Sol / disco de luz, se tiñe según temperatura
  drawSunGlow(temperatura);

  // -------------------------------------------------------------
  // MOMENTO — POSIBILIDAD (randomGaussian alrededor de walkX)
  // -------------------------------------------------------------
  if (random(1) < 0.3) {
    let xNormal = walkX + randomGaussian(0, 50);
    xNormal = constrain(xNormal, 20, width - 20);
    particulas.push({
      x: xNormal,
      y: random(height * 0.4),
      vx: random(-1.5, 1.5),
      vy: random(-1.5, 1.5),
      tipo: 'posibilidad',
      alpha: random(80, 200),
      size: random(1.5, 3)
    });
  }

  // MOMENTO — EXCEPCIÓN (recuperación improbable)
  let probabilidadRecuperacion = influenciaActiva ? 0.02 : 0.003;
  if (random(1) < probabilidadRecuperacion) {
    hielo = min(95, hielo + 1);
    particulas.push({
      x: random(width),
      y: random(height * 0.5, height * 0.75),
      vx: random(-3, 3),
      vy: random(-2, 2),
      tipo: 'excepcion',
      alpha: 255,
      size: 6
    });
  }

  // -------------------------------------------------------------
  // 2. CAMINATA ALEATORIA CON TENDENCIA
  // -------------------------------------------------------------
  if (frameCount % 20 === 0) {
    if (random(1) < 0.6) {
      walkX += random(1, 4);
    } else {
      walkX -= random(1, 4);
    }
  }
  walkX = constrain(walkX, 90, width - 90);

  // -------------------------------------------------------------
  // OCÉANO — con leve oleaje y reflejo del glaciar
  // -------------------------------------------------------------
  let alturaOcean = map(hielo, 100, 0, 180, 500);
  drawOcean(alturaOcean);

  // -------------------------------------------------------------
  // 3. GLACIAR — distribución normal / silueta orgánica con sombreado
  // -------------------------------------------------------------
  let alturaGlaciar = map(hielo, 0, 100, 10, 310);
  drawGlacier(alturaOcean, alturaGlaciar, walkX);

  // -------------------------------------------------------------
  // FAUNA VULNERABLE — pingüino con sombra suave
  // -------------------------------------------------------------
  if (hielo > 10) {
    drawPenguin(walkX, height - alturaOcean - alturaGlaciar - 14);
  }

  // -------------------------------------------------------------
  // PARTÍCULAS
  // -------------------------------------------------------------
  updateAndDrawParticles();

  if (influenciaActiva) {
    if (frameCount % 3 === 0) {
      particulas.push({
        x: mouseX + random(-8, 8),
        y: mouseY + random(-8, 8),
        vx: random(-0.5, 0.5),
        vy: random(-2, -0.8),
        tipo: 'influencia',
        alpha: 220,
        size: 4
      });
    }
  }

  // Viñeta sutil para dar profundidad
  drawVignette();

  // Cursor personalizado
  if (mouseDentro) {
    drawCursor();
  }

  // -------------------------------------------------------------
  // PANEL DE INTERFAZ
  // -------------------------------------------------------------
  drawHUD(influenciaActiva);
}

// ===================================================================
// FUNCIONES DE DIBUJO
// ===================================================================

function drawSky(temp) {
  let coldTop    = color(8, 20, 48);
  let coldBottom = color(58, 90, 130);
  let warmTop    = color(140, 60, 46);
  let warmBottom = color(232, 152, 82);

  let topColor    = lerpColor(coldTop, warmTop, map(temp, 10, 95, 0, 1));
  let bottomColor = lerpColor(coldBottom, warmBottom, map(temp, 10, 95, 0, 1));

  noStroke();
  let skyH = height - 60;
  for (let y = 0; y < skyH; y++) {
    let t = y / skyH;
    let c = lerpColor(topColor, bottomColor, t);
    stroke(c);
    line(0, y, width, y);
  }
  noStroke();
}

function drawAurora(hielo, temp) {
  // Solo visible cuando el frío predomina — recompensa visual de un ecosistema sano
  let intensidad = map(hielo, 40, 95, 0, 1, true) * map(temp, 10, 60, 1, 0, true);
  if (intensidad <= 0.02) return;

  push();
  blendMode(ADD);
  noFill();
  let bandas = [
    color(127, 231, 196),
    color(120, 200, 255),
    color(180, 255, 220)
  ];
  for (let b = 0; b < 3; b++) {
    stroke(red(bandas[b]), green(bandas[b]), blue(bandas[b]), 55 * intensidad);
    strokeWeight(10);
    beginShape();
    for (let x = -20; x <= width + 20; x += 20) {
      let y = 90 + b * 26
        + sin(x * 0.012 + frameCount * 0.01 + b * 2) * 22
        + sin(x * 0.03 + frameCount * 0.02) * 8;
      curveVertex(x, y);
    }
    endShape();
  }
  blendMode(BLEND);
  pop();
}

function drawSunGlow(temp) {
  let sx = width - 80;
  let sy = 90;
  let warmth = map(temp, 10, 95, 0, 1);
  let sunColor = lerpColor(color(226, 236, 250), color(255, 205, 120), warmth);

  push();
  noStroke();
  for (let r = 90; r > 0; r -= 6) {
    let a = map(r, 0, 90, 0, 26);
    fill(red(sunColor), green(sunColor), blue(sunColor), a);
    ellipse(sx, sy, r, r);
  }
  fill(255, 250, 240, 230);
  ellipse(sx, sy, 34, 34);
  pop();
}

function drawOcean(alturaOcean) {
  push();
  let oceanTop = color(18, 90, 110, 235);
  let oceanBottom = color(6, 40, 55, 245);
  noStroke();
  let baseY = height - alturaOcean;
  for (let y = 0; y < alturaOcean; y += 4) {
    let t = y / alturaOcean;
    let c = lerpColor(oceanTop, oceanBottom, t);
    fill(c);
    rect(0, baseY + y, width, 4);
  }

  // Cresta de oleaje sutil en la superficie
  stroke(226, 246, 255, 90);
  strokeWeight(1.4);
  noFill();
  beginShape();
  for (let x = 0; x <= width; x += 10) {
    let y = baseY + sin(x * 0.05 + frameCount * 0.04) * 2.5;
    vertex(x, y);
  }
  endShape();
  pop();
}

function drawGlacier(alturaOcean, alturaGlaciar, walkX) {
  let baseY = height - alturaOcean;

  push();
  // Sombra proyectada en el agua (reflejo tenue)
  noStroke();
  fill(220, 240, 255, 35);
  beginShape();
  vertex(40, baseY);
  vertex(120, baseY + alturaGlaciar * 0.18);
  vertex(walkX, baseY + alturaGlaciar * 0.26);
  vertex(330, baseY + alturaGlaciar * 0.2);
  vertex(410, baseY);
  endShape(CLOSE);
  pop();

  // --- Contorno principal del glaciar (silueta real, suavizada con curvas) ---
  push();
  fill(235, 246, 255, 245);
  stroke(255, 255, 255, 120);
  strokeWeight(1);
  beginShape();
  curveVertex(30, baseY);
  curveVertex(40, baseY);
  curveVertex(120, baseY - alturaGlaciar * 0.8);
  curveVertex(walkX, baseY - alturaGlaciar);
  curveVertex(330, baseY - alturaGlaciar * 0.85);
  curveVertex(410, baseY);
  curveVertex(420, baseY);
  endShape(CLOSE);

  // Grietas / textura sutil de hielo
  stroke(150, 190, 220, 90);
  strokeWeight(1);
  line(walkX - 40, baseY - alturaGlaciar * 0.5, walkX - 15, baseY - alturaGlaciar * 0.75);
  line(walkX + 30, baseY - alturaGlaciar * 0.4, walkX + 55, baseY - alturaGlaciar * 0.65);

  // Highlight de luz en la cresta
  noFill();
  stroke(255, 255, 255, 160);
  strokeWeight(2);
  beginShape();
  curveVertex(120, baseY - alturaGlaciar * 0.8);
  curveVertex(walkX, baseY - alturaGlaciar);
  curveVertex(330, baseY - alturaGlaciar * 0.85);
  endShape();
  pop();
}

function drawPenguin(xP, yP) {
  push();
  // sombra suave sobre el hielo
  noStroke();
  fill(20, 40, 60, 60);
  ellipse(xP, yP + 15, 26, 8);

  // Cuerpo negro
  fill(24, 34, 48);
  ellipse(xP, yP, 20, 26);

  // Vientre blanco
  fill(250, 250, 252);
  ellipse(xP, yP + 2, 12, 18);

  // Cabeza
  fill(24, 34, 48);
  ellipse(xP, yP - 12, 14, 14);

  // Pico naranja
  fill(247, 140, 60);
  triangle(xP + 5, yP - 13, xP + 11, yP - 11, xP + 5, yP - 9);

  // Ojo
  fill(255);
  ellipse(xP + 3, yP - 13, 3, 3);
  fill(10);
  ellipse(xP + 4, yP - 13, 1.5, 1.5);
  pop();
}

function updateAndDrawParticles() {
  for (let i = particulas.length - 1; i >= 0; i--) {
    let p = particulas[i];
    noStroke();
    if (p.tipo === 'excepcion') {
      fill(250, 204, 21, p.alpha);
      ellipse(p.x, p.y, p.size + 2, p.size + 2);
      fill(255, 240, 200, p.alpha * 0.5);
      ellipse(p.x, p.y, p.size + 8, p.size + 8);
    } else if (p.tipo === 'influencia') {
      fill(255, 130, 130, p.alpha);
      ellipse(p.x, p.y, p.size, p.size);
    } else {
      fill(255, 255, 255, p.alpha);
      ellipse(p.x, p.y, p.size, p.size);
    }

    p.x += p.vx;
    p.y += p.vy;
    p.alpha -= 4.5;

    if (p.alpha <= 0) {
      particulas.splice(i, 1);
    }
  }
}

function drawVignette() {
  push();
  noFill();
  for (let i = 0; i < 60; i++) {
    let a = map(i, 0, 60, 0, 70);
    stroke(4, 8, 16, a * 0.06);
    strokeWeight(i);
    rect(0, 0, width, height);
  }
  pop();
}

function drawCursor() {
  push();
  noFill();
  stroke(255, 110, 110, 170);
  strokeWeight(2);
  ellipse(mouseX, mouseY, 35, 35);
  fill(255, 110, 110, 40);
  noStroke();
  ellipse(mouseX, mouseY, 18, 18);
  pop();
}

function drawHUD(influenciaActiva) {
  push();
  // Panel translúcido tipo "vidrio"
  let panelW = 340;
  let panelH = 54;
  let px = width / 2 - panelW / 2;
  let py = 24;

  noStroke();
  fill(6, 12, 22, 190);
  rect(px, py, panelW, panelH, 16);
  stroke(255, 255, 255, 30);
  strokeWeight(1);
  noFill();
  rect(px, py, panelW, panelH, 16);

  noStroke();
  textAlign(CENTER, CENTER);

  textFont('JetBrains Mono');
  fill(230, 240, 250);
  textSize(15);
  text(`${floor(anioDecimal)}`, width / 2, py + 20);

  textSize(10.5);
  let estado = influenciaActiva ? 'SANANDO' : 'EN DECLIVE';
  fill(hielo > 40 ? color(140, 220, 200) : color(240, 150, 120));
  text(`HIELO ${hielo.toFixed(1)}%  ·  ${estado}`, width / 2, py + 38);

  // Texto guía inferior
  textFont('Space Grotesk');
  fill(220, 230, 240, 170);
  textSize(11);
  text("Ruido Perlin · Caminata aleatoria · Distribución normal", width / 2, height - 24);
  pop();
}
````
<img width="337" height="557" alt="image" src="https://github.com/user-attachments/assets/0d8188d7-2a45-4443-9ee9-6d87837c2173" />

**Links**  
<a name="ej4"></a>
[Prototipo sin mejora de diseño](https://editor.p5js.org/Ayepes2402/sketches/QyeTzFMVk)   
[Prototipo con mejora de diseño](https://editor.p5js.org/Ayepes2402/sketches/QURmtWrVO)

**Uso conceptos de la unidad**  
<a name="ej2"></a>
La experiencia utiliza diferentes conceptos de la unidad para transformar la aleatoriedad en un sistema visual con significado. Se aplican ruido Perlin, caminata aleatoria con tendencia y distribución normal para representar el comportamiento cambiante de un ecosistema polar.

**Ruido Perlin:** se utiliza para controlar las variaciones del clima y la temperatura del sistema. A diferencia de un movimiento completamente aleatorio, permite generar cambios continuos y naturales que representan la evolución del ambiente con el paso del tiempo.  
**Caminata aleatoria con tendencia:** se aplica al desplazamiento del estado del glaciar mediante walkX. Aunque el movimiento mantiene variaciones aleatorias, existe una pequeña preferencia hacia una dirección, representando cómo pequeñas alteraciones repetidas pueden generar una tendencia a largo plazo.
**Distribución normal:** se utiliza mediante randomGaussian() para generar partículas alrededor de un punto esperado. Esto representa que la mayoría de los comportamientos del ecosistema permanecen cerca de un estado habitual, mientras que algunos casos presentan variaciones más alejadas.

Además, se incorpora una excepción probabilística, donde un evento poco frecuente puede favorecer la recuperación del hielo, y la influencia del visitante modifica la probabilidad de que estos eventos ocurran. De esta manera, la incertidumbre no funciona como un comportamiento sin reglas, sino como un sistema donde diferentes formas de aleatoriedad producen diferentes posibilidades.  

**Dificultades y soluciones**  
<a name="ej5"></a>
Mis dificultades fueron que me generara un codigo con lo que yo queria porque tal como muestro a lo largo de mi trayecto fue bastante complejo sacar algo bonito y funcional y que no se viera tan basico y mi solucion fue pelear con gemini hasta que lograra darme algo bueno asi sea que me tocara cambiar de tema un monton de veces  

**Uso de IA solo en código nada en cambios de diseño o de idea**  

| Criterio | Cumplo | No cumplo | Evidencia |
| :--- | :---: | :---: | :--- |
| **Encargo completo:** interpreto los cinco momentos dentro de un mismo sistema visual. | X | | [evidencia 1](#ej1)|
| **Simulación con intención:** utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo. | X | | [evidencia 2](#ej2)|
| **Interacción significativa:** la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención. | X | |[evidencia 3](#ej3)|
| **Prototipo funcional:** la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla. | X | | [evidencia 4](#ej4)|
| **Proceso documentado:** la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo. | X | | [evidencia 5](#ej5)|













