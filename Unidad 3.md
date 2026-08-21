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


## Ecuación
| Fuerza / Modulación | Ecuación| Archivo de Origen |
| :--- | :--- | :--- |
| **1. Fuerza de Retorno (Resorte)** | $\vec{F}_{return} = (\vec{targetHome} - \vec{p}) \times \text{returnSpeed}$ (con corrección de límites periódicos del espacio)[cite: 1] | `createSimulation.js`[cite: 1] |
| **2. Oscilador de Voz** | $\vec{target} += \hat{dir} \times \left( \frac{\sin(8t + x_d) + \cos(6t + y_d) + \sin(10t + z_d)}{3} \times \text{voiceIntensity} \times \text{voiceOscillator} \right)$[cite: 1] | `createSimulation.js`[cite: 1] |
| **3. Onda por Columnas** | $\text{swayX} = \sin(\text{time} \cdot \text{freq} + \text{phase}) \cdot \text{amplitude}$ (con desplazamiento auxiliar en Y)[cite: 1] | `createSimulation.js`[cite: 1] |
| **4. Impulso de Ritmo (Beat)** | $\vec{v} = \hat{p} \cdot (\text{beatForce} \cdot 2.5) + \vec{randDir} \cdot (\text{beatForce} \cdot 1.2)$[cite: 1] | `createSimulation.js`[cite: 1] |
| **5. Deriva Global (Viento)** | $\vec{globalOffset} += \vec{drift} \cdot \Delta t \cdot 0.35$ (acumulado en bucle principal y aplicado como traslación espacial)[cite: 1, 3] | `main.js` y `createSimulation.js`[cite: 1, 3] |
| **6. Amortiguación y Límite** | $\vec{v} = \vec{v} \cdot \text{damping}$; si $|\vec{v}| > \text{maxSpeed}$, $\vec{v} = \hat{v} \cdot \text{maxSpeed}$[cite: 1] | `createSimulation.js`[cite: 1] |
