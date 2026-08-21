# Actividad 4  



## Mapa del sistema

| Fuerza / Modulación | Tecla(s) / Control | Archivo | ¿Qué hace? | Fragmento de Código Asociado |
| :--- | :--- | :--- | :--- | :--- |
| **1. Fuerza de Retorno & Formaciones** | `1`, `2`, `3`, `N`, `D`, `X`, `C` | `createSimulation.js` | Atrae continuamente a cada partícula hacia su posición de destino (`home`) y permite cambiar o congelar su formación geométrica. | ```javascript<br>const delta = targetHome.sub(p).toVar();<br>const returnForce = delta.mul(params.returnSpeed);<br>v.addAssign(returnForce.mul(dt));<br>``` |
| **2. Oscilador de Voz** | `V` | `createSimulation.js` | Modifica dinámicamente el objetivo local usando funciones trigonométricas y radiales para crear expansión y contracción. | ```javascript<br>If(params.voiceOscillator.greaterThan(0.001), () => {<br>  const len = localTarget.length();<br>  // ... cálculo de ondas y bulge<br>  localTarget.addAssign(dir.mul(bulge.mul(params.voiceOscillator)));<br>});<br>``` |
| **3. Onda por Columnas** | `M` | `createSimulation.js` | Desplaza las partículas con patrones sinusoidales y cosenoidales independientes basados en el índice de cada columna. | ```javascript<br>If(params.columnWaveEnabled.greaterThan(0.5), () => {<br>  // ... cálculo de swayX y bobY<br>  localTarget.addAssign(vec3(swayX, bobY, 0.0));<br>});<br>``` |
| **4. Impulso de Ritmo (Beat)** | `B` | `createSimulation.js` | Fuerza explosiva de tipo radial y direccional aleatoria que altera bruscamente la velocidad al disparar un beat. | ```javascript<br>const beatImpulse = Fn(() => {<br>  const dir = p.normalize();<br>  v.assign(dir.mul(params.beatForce.mul(2.5)).add(randDir.mul(params.beatForce.mul(1.2))));<br>}).compute(count);<br>``` |
| **5. Deriva Global (Viento)** | `F` (Auto-Flujo) o `W` (Preset Viento) | `main.js` y `createSimulation.js` | Desplaza el espacio sumando un vector acumulado en el tiempo al offset global de las posiciones base. | ```javascript<br>// main.js<br>params.globalOffset.value.x += params.driftX.value * delta * 0.35;<br>// createSimulation.js<br>const shiftedHome = localTarget.add(params.globalOffset);<br>``` |
| **6. Amortiguación y Velocidad Máxima** | *N/A (Parámetro base)* | `createSimulation.js` | Fuerzas de fricción pasivas que estabilizan la simulación y evitan velocidades infinitas. | ```javascript<br>v.assign(v.mul(params.damping));<br>If(speed.greaterThan(params.maxSpeed), () => {<br>  v.assign(v.normalize().mul(params.maxSpeed));<br>});<br>``` |
