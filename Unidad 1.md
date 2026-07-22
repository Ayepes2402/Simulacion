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

## Actividad 6  
**Crea un nuevo sketch en p5.js donde los visualices.**  
**Explica por qué lo visualizaste de esa manera y qué resultados esperabas obtener.**  

