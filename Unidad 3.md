# Actividad 4  

## Link
[Trabajo](https://ayepes2402.github.io/R3/)

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

## Diseño
La verdad es que mientras escuchaba la canción me fui imaginando diferentes formas tipo moviendose y algunnas que parecieran medio palpitando y así, ya en el proceso fui agregando la intencidad el autoflujo y demás

## Trabajo con la IA  

Primero le dije esto

te dare estos codigos para poder proceder con esto, me gustaria probar hacer diferentes formas tales como esferas, cubos y que tenga bits y esas cosas para que sea mas llamativo No es un music visualizer La cadena esperada no es «audio → parámetro visual». Es «música → percepción humana → decisión interpretativa → gesto → fuerza → comportamiento emergente». 

<img width="1102" height="948" alt="image" src="https://github.com/user-attachments/assets/e41f2b65-3b5a-404b-b33f-5d92cd030e54" />

despues le dije Pues la verdad se escucha pesado. Yo digo que le empecemos dando forma a las figuras (el cubo, las esferas) y a los resortes para ver cómo se mueven. Quiero ver cómo cambian de una forma a otra sin que se vea cortado, sino fluido.

<img width="1109" height="1069" alt="image" src="https://github.com/user-attachments/assets/58eda705-deeb-468c-af33-9edcec319619" />

despues fui preguntando que era lo que podiamos ir tachando de la lista de tareas me lo dio y le dije que lo ejecutara  

<img width="1342" height="1184" alt="image" src="https://github.com/user-attachments/assets/e4252519-ecf9-468f-9493-f448efbe5568" />

luego de estar experimentando tuve un problema con las partículas y esto me respondió  

<img width="1289" height="596" alt="image" src="https://github.com/user-attachments/assets/a17a20bd-fe37-4c97-8c2b-6572e247baa0" />

y ya despues de varios intentos logré sacar el código final  

<img width="1278" height="1110" alt="image" src="https://github.com/user-attachments/assets/b1a13b7c-9f52-4064-84fe-162721944c47" />  

main.js
```js
import * as THREE from 'three/webgpu';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import WebGPU from 'three/addons/capabilities/WebGPU.js';
import './styles.css';

import { createParameters } from './simulation/parameters.js';
import { createSimulation } from './simulation/createSimulation.js';
import { createLabPanel } from './ui/labPanel.js';

const PARTICLE_COUNT = 50000;

async function main() {
  const mount = document.querySelector('#app');

  if (!WebGPU.isAvailable()) {
    mount.appendChild(WebGPU.getErrorMessage());
    throw new Error('Este proyecto requiere WebGPU para ejecutar compute shaders.');
  }

  const scene = new THREE.Scene();
  scene.background = new THREE.Color('#050607');

  const camera = new THREE.PerspectiveCamera(50, innerWidth / innerHeight, 0.05, 100);
  camera.position.set(0, 0, 11);

  const renderer = new THREE.WebGPURenderer({ antialias: true });
  renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
  renderer.setSize(innerWidth, innerHeight);
  mount.appendChild(renderer.domElement);
  await renderer.init();

  const orbit = new OrbitControls(camera, renderer.domElement);
  orbit.enableDamping = true;
  orbit.target.set(0, 0, 0);

  // --- NUEVO: SISTEMA DE POSICIONES DE CÁMARA ---
  const savedCameraPositions = {};
  const savedTargetPositions = {};
  let targetCameraPos = null;
  let targetOrbitTarget = null;
  let isTransitioning = false;

  const saveCameraSlot = (slot) => {
    savedCameraPositions[slot] = camera.position.clone();
    savedTargetPositions[slot] = orbit.target.clone();
  };

  const moveToCameraSlot = (slot) => {
    if (savedCameraPositions[slot]) {
      targetCameraPos = savedCameraPositions[slot];
      targetOrbitTarget = savedTargetPositions[slot];
      isTransitioning = true;
    }
  };

  // --- NUEVO: GIROSCOPIO DE CÁMARA (3 EJES) ---
  const gyro = { enabled: false, speedX: 0, speedY: 0.3, speedZ: 0 };
  const gyroAxisX = new THREE.Vector3(1, 0, 0);
  const gyroAxisY = new THREE.Vector3(0, 1, 0);
  const gyroAxisZ = new THREE.Vector3(0, 0, 1);
  const gyroOffset = new THREE.Vector3();

  const params = createParameters();
  const simulation = createSimulation({ renderer, scene, params, count: PARTICLE_COUNT });

  let paused = false;
  let mode = 'LAB';
  let panel;

  const handleCreateCube = () => simulation.setCubeGrid(1);
  const handleDivideCube = () => simulation.setCubeGrid(params.cubeGridSize.value + 1);
  const handleMergeCube = () => simulation.setCubeGrid(params.cubeGridSize.value - 1);
  const handleCompactSphere = () => simulation.setCompactSphere();
  const handleClusterSphere = () => simulation.setClusterSphere();
  const handleToggleVoice = () => simulation.toggleVoiceOscillator();
  const handleLightUp = () => params.brightnessMultiplier.value = Math.min(5.0, params.brightnessMultiplier.value + 0.35);
  const handleLightDown = () => params.brightnessMultiplier.value = Math.max(0.1, params.brightnessMultiplier.value - 0.35);
  const handleColumnCone = () => simulation.setColumnCone();
  const handleToggleColumnWave = () => simulation.toggleColumnWave();

  let frozen = false;
  const handleToggleFreeze = () => {
    frozen = !frozen;
    if (frozen) {
      autoFlow = false;
      params.driftX.value = 0;
      params.driftY.value = 0;
      params.driftZ.value = 0;
      simulation.centerAndFreeze();
    } else {
      simulation.unfreeze();
    }
    panel?.refresh();
  };

  let autoFlow = false;
  let flowTime = 0;
  const handleToggleFlow = () => {
    autoFlow = !autoFlow;
    if (!autoFlow) {
      params.driftX.value = 0;
      params.driftY.value = 0;
      params.driftZ.value = 0;
      panel?.refresh();
    }
  };

  // --- NUEVA FUNCIÓN PARA EL RESET COMPLETO ---
  const handleReset = () => {
    simulation.reset();
    handleCompactSphere();              // Vuelve a hacer la forma de esfera
    params.voiceOscillator.value = 1.0; // Fuerza el encendido del palpitar
    
    // Apaga cualquier efecto secundario (como el Warp/Torbellino)
    autoFlow = false;
    params.driftX.value = 0;
    params.driftY.value = 0;
    params.driftZ.value = 0;
    params.flowSpeed.value = 3.0; 
    gyro.enabled = false;
    params.brightnessMultiplier.value = 1.0;
    
    panel?.refresh();
  };

  const applyPreset = (id) => {
    params.initialSpeed.value = 0.35;
    params.driftX.value = 0;
    params.driftY.value = 0;
    params.driftZ.value = 0;
    
    if (id === 'inertia') {
      params.initialSpeed.value = 0.8;
    } else if (id === 'warp') {
      // Efecto W: Torbellino explosivo tridimensional
      simulation.triggerBeat(); 
      autoFlow = true;          
      params.flowSpeed.value = 15.0; 
      gyro.enabled = true;      
      gyro.speedY = 1.2;        
      params.brightnessMultiplier.value = 2.5; 
    }
    
    panel?.refresh();
  };

  const setMode = (next) => {
    mode = next;
    const lab = mode === 'LAB';
    panel.setVisible(lab);
    hud.innerHTML = lab
      ? '<strong>LAB</strong> · 1: cuadro · D/X: dividir/juntar · 2: esfera · V: hablar · 3: esferas agrupadas · K/L: brillo · B: beat · R: reset · F: auto-flujo · I/W: presets · N: cono columnas · M: onda columnas · C: centrar y congelar · G: giroscopio cámara<br><strong>Cámara:</strong> Shift+4..7 (guardar) | 4..7 (viajar)'
      : '';
  };

  panel = createLabPanel({
    params,
    onReset: handleReset, // Ahora usa nuestro nuevo reset
    onModeChange: () => setMode(mode === 'LAB' ? 'PERFORMANCE' : 'LAB'),
    onPauseChange: () => paused = !paused,
    onBeat: () => simulation.triggerBeat(),
    onCreateCube: handleCreateCube,
    onDivideCube: handleDivideCube,
    onMergeCube: handleMergeCube,
    onCompactSphere: handleCompactSphere,
    onClusterSphere: handleClusterSphere,
    onToggleVoice: handleToggleVoice,
    onLightUp: handleLightUp,
    onLightDown: handleLightDown,
    onToggleFlow: handleToggleFlow,
    onToggleFreeze: handleToggleFreeze,
    onColumnCone: handleColumnCone,
    onToggleColumnWave: handleToggleColumnWave,
    onPresetInertia: () => applyPreset('inertia'),
    onPresetWind: () => applyPreset('warp'), // Vinculado a 'warp'
    onSaveCameraSlot: saveCameraSlot,
    onTravelCameraSlot: moveToCameraSlot,
    gyro
  });

  const hud = document.createElement('div');
  hud.className = 'hud';
  document.body.append(hud);
  setMode('LAB');

  addEventListener('keydown', (event) => {
    if (event.repeat) return;
    if (event.code === 'KeyP') setMode(mode === 'LAB' ? 'PERFORMANCE' : 'LAB');
    if (event.code === 'KeyR') handleReset(); // Tecla R llama a nuestro nuevo reset
    if (event.code === 'KeyB') simulation.triggerBeat();
    if (event.code === 'Digit1' || event.code === 'Numpad1' || event.code === 'Key1') handleCreateCube();
    if (event.code === 'KeyD') handleDivideCube();
    if (event.code === 'KeyX') handleMergeCube();
    if (event.code === 'Digit2' || event.code === 'Numpad2' || event.code === 'Key2') handleCompactSphere();
    if (event.code === 'KeyV') handleToggleVoice();
    if (event.code === 'Digit3' || event.code === 'Numpad3' || event.code === 'Key3') handleClusterSphere();
    if (event.code === 'KeyK') handleLightUp();
    if (event.code === 'KeyL') handleLightDown();
    if (event.code === 'KeyF') handleToggleFlow();

    if (event.shiftKey && (event.code === 'Digit4' || event.code === 'Numpad4' || event.code === 'Key4')) saveCameraSlot(4);
    if (event.shiftKey && (event.code === 'Digit5' || event.code === 'Numpad5' || event.code === 'Key5')) saveCameraSlot(5);
    if (event.shiftKey && (event.code === 'Digit6' || event.code === 'Numpad6' || event.code === 'Key6')) saveCameraSlot(6);
    if (event.shiftKey && (event.code === 'Digit7' || event.code === 'Numpad7' || event.code === 'Key7')) saveCameraSlot(7);

    if (!event.shiftKey && (event.code === 'Digit4' || event.code === 'Numpad4' || event.code === 'Key4')) moveToCameraSlot(4);
    if (!event.shiftKey && (event.code === 'Digit5' || event.code === 'Numpad5' || event.code === 'Key5')) moveToCameraSlot(5);
    if (!event.shiftKey && (event.code === 'Digit6' || event.code === 'Numpad6' || event.code === 'Key6')) moveToCameraSlot(6);
    if (!event.shiftKey && (event.code === 'Digit7' || event.code === 'Numpad7' || event.code === 'Key7')) moveToCameraSlot(7);

    if (event.code === 'KeyI') applyPreset('inertia');
    if (event.code === 'KeyW') applyPreset('warp'); // W llama a 'warp'
    if (event.code === 'KeyC') handleToggleFreeze();
    if (event.code === 'KeyN') handleColumnCone();
    if (event.code === 'KeyM') handleToggleColumnWave();
    if (event.code === 'KeyG') gyro.enabled = !gyro.enabled;
  });

  addEventListener('resize', () => {
    camera.aspect = innerWidth / innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(innerWidth, innerHeight);
  });

  // Iniciamos la app con nuestro reset maestro
  handleReset();

  let clock = new THREE.Clock();

  renderer.setAnimationLoop(() => {
    const delta = clock.getDelta();

    if (!paused) {
      params.time.value += delta * params.timeScale.value;

      if (isTransitioning && targetCameraPos && targetOrbitTarget) {
        camera.position.lerp(targetCameraPos, delta * 4.0);
        orbit.target.lerp(targetOrbitTarget, delta * 4.0);
        if (camera.position.distanceTo(targetCameraPos) < 0.01) isTransitioning = false;
      }

      if (gyro.enabled) {
        gyroOffset.copy(camera.position).sub(orbit.target);
        if (gyro.speedX) gyroOffset.applyAxisAngle(gyroAxisX, gyro.speedX * delta);
        if (gyro.speedY) gyroOffset.applyAxisAngle(gyroAxisY, gyro.speedY * delta);
        if (gyro.speedZ) gyroOffset.applyAxisAngle(gyroAxisZ, gyro.speedZ * delta);
        camera.position.copy(orbit.target).add(gyroOffset);
      }

      if (autoFlow) {
        flowTime += delta;
        const s = params.flowSpeed.value;
        params.driftX.value = Math.cos(flowTime * 0.31) * s;
        params.driftY.value = Math.sin(flowTime * 0.47) * s;
        params.driftZ.value = Math.sin(flowTime * 0.23) * Math.cos(flowTime * 0.19) * s * 0.6;
        panel?.refresh();
      }

      params.globalOffset.value.x += params.driftX.value * delta * 0.35;
      params.globalOffset.value.y += params.driftY.value * delta * 0.35;
      params.globalOffset.value.z += params.driftZ.value * delta * 0.35;

      simulation.stepSimulation();
    }

    if (params.beatIntensity.value > 0.001) {
      params.beatIntensity.value *= Math.exp(-7.5 * delta);
    } else {
      params.beatIntensity.value = 0.0;
    }

    orbit.update();
    renderer.render(scene, camera);
  });
}

main().catch((error) => {
  console.error(error);
  const pre = document.createElement('pre');
  pre.style.cssText = 'position:fixed;inset:16px;white-space:pre-wrap;color:#fff;z-index:50';
  pre.textContent = String(error?.stack || error);
  document.body.append(pre);
});
````

labPanel.js  
````js
function rangeRow(parent, label, object, key, min, max, step, onInput, getValue) {
  const wrap = document.createElement('div');
  wrap.className = 'row';
  const lab = document.createElement('label');
  const name = document.createElement('span');
  const value = document.createElement('span');
  value.className = 'value';
  name.textContent = label;
  lab.append(name, value);
  const input = document.createElement('input');
  input.type = 'range';
  input.min = String(min);
  input.max = String(max);
  input.step = String(step);
  input.value = String(object[key]);
  const refresh = () => {
    object[key] = Number(input.value);
    value.textContent = Number(input.value).toFixed(step < 0.01 ? 3 : 2);
    onInput?.(object[key]);
  };
  input.addEventListener('input', refresh);
  refresh();
  wrap.append(lab, input);
  parent.append(wrap);
  return {
    input,
    refresh() {
      if (getValue) {
        const next = Number(getValue());
        object[key] = next;
        input.value = String(next);
        value.textContent = next.toFixed(step < 0.01 ? 3 : 2);
      }
    }
  };
}

function button(parent, label, onClick) {
  const b = document.createElement('button');
  b.textContent = label;
  b.addEventListener('click', onClick);
  parent.append(b);
  return b;
}

export function createLabPanel({
  params,
  onReset,
  onModeChange,
  onPauseChange,
  onBeat,
  onCreateCube,
  onDivideCube,
  onMergeCube,
  onCompactSphere,
  onClusterSphere,
  onToggleVoice,
  onLightUp,
  onLightDown,
  onToggleFlow,
  onToggleFreeze,
  onColumnCone,
  onToggleColumnWave,
  onPresetInertia,
  onPresetWind,
  onSaveCameraSlot,
  onTravelCameraSlot,
  gyro
}) {
  const refreshers = [];
  const panel = document.createElement('aside');
  panel.className = 'panel';
  panel.innerHTML = `
    <h1>Partículas Libres</h1>
    <p>Teclas: <strong>1</strong> (cuadro), <strong>D/X</strong> (dividir/juntar), <strong>2</strong> (esfera), <strong>V</strong> (hablar), <strong>3</strong> (esferas agrupadas), <strong>K/L</strong> (brillo).</p>
  `;

  const sim = document.createElement('div');
  sim.className = 'group';
  sim.innerHTML = '<h2>Configuración</h2>';
  panel.append(sim);

  const state = {
    timeScale: params.timeScale.value,
    maxSpeed: params.maxSpeed.value,
    particleSize: params.particleSize.value,
    beatForce: params.beatForce.value,
    returnSpeed: params.returnSpeed.value,
    damping: params.damping.value,
    driftX: params.driftX.value,
    driftY: params.driftY.value,
    driftZ: params.driftZ.value,
    flowSpeed: params.flowSpeed.value,
    columnCount: params.columnCount.value,
    coneHeight: params.coneHeight.value,
    coneRadius: params.coneRadius.value,
    columnWaveAmplitude: params.columnWaveAmplitude.value,
    freezeRadius: params.freezeRadius.value
  };

  refreshers.push(rangeRow(sim, 'timeScale', state, 'timeScale', 0, 2, 0.01, (v) => params.timeScale.value = v, () => params.timeScale.value));
  refreshers.push(rangeRow(sim, 'maxSpeed', state, 'maxSpeed', 0.2, 12, 0.1, (v) => params.maxSpeed.value = v, () => params.maxSpeed.value));
  refreshers.push(rangeRow(sim, 'particleSize', state, 'particleSize', 0.005, 0.1, 0.001, (v) => params.particleSize.value = v, () => params.particleSize.value));
  refreshers.push(rangeRow(sim, 'fuerza Beat', state, 'beatForce', 0.2, 5.0, 0.1, (v) => params.beatForce.value = v, () => params.beatForce.value));
  refreshers.push(rangeRow(sim, 'retorno Respiro', state, 'returnSpeed', 5, 60, 1, (v) => params.returnSpeed.value = v, () => params.returnSpeed.value));
  refreshers.push(rangeRow(sim, 'amortiguación', state, 'damping', 0.80, 0.99, 0.01, (v) => params.damping.value = v, () => params.damping.value));

  // Grupo de flujo direccional
  const driftGroup = document.createElement('div');
  driftGroup.className = 'group';
  driftGroup.innerHTML = '<h2>Flujo Direccional</h2>';
  panel.append(driftGroup);

  refreshers.push(rangeRow(driftGroup, 'Deriva X →', state, 'driftX', -15, 15, 0.5, (v) => params.driftX.value = v, () => params.driftX.value));
  refreshers.push(rangeRow(driftGroup, 'Deriva Y ↑', state, 'driftY', -15, 15, 0.5, (v) => params.driftY.value = v, () => params.driftY.value));
  refreshers.push(rangeRow(driftGroup, 'Deriva Z ◎', state, 'driftZ', -15, 15, 0.5, (v) => params.driftZ.value = v, () => params.driftZ.value));

  refreshers.push(rangeRow(driftGroup, 'Velocidad Auto-Flujo', state, 'flowSpeed', 0.5, 12, 0.5, (v) => params.flowSpeed.value = v, () => params.flowSpeed.value));

  // Boton Auto-Flujo
  let flowBtnActive = false;
  const flowBtn = document.createElement('button');
  flowBtn.textContent = '🌀 Auto-Flujo (F)';
  flowBtn.className = 'btn-flow';
  flowBtn.style.marginTop = '6px';
  flowBtn.addEventListener('click', () => {
    flowBtnActive = !flowBtnActive;
    flowBtn.textContent = flowBtnActive ? '⏹️ Detener Flujo (F)' : '🌀 Auto-Flujo (F)';
    flowBtn.style.opacity = flowBtnActive ? '1' : '0.75';
    onToggleFlow?.();
  });
  driftGroup.append(flowBtn);

  const resetDriftBtn = document.createElement('button');
  resetDriftBtn.textContent = '⏹ Limpiar Deriva';
  resetDriftBtn.style.marginTop = '4px';
  resetDriftBtn.addEventListener('click', () => {
    params.driftX.value = 0;
    params.driftY.value = 0;
    params.driftZ.value = 0;
    state.driftX = 0; state.driftY = 0; state.driftZ = 0;
    for (const r of refreshers) r.refresh();
  });
  driftGroup.append(resetDriftBtn);

  const coneGroup = document.createElement('div');
  coneGroup.className = 'group';
  coneGroup.innerHTML = '<h2>Cono por Columnas</h2>';
  panel.append(coneGroup);

  refreshers.push(rangeRow(coneGroup, 'Columnas', state, 'columnCount', 4, 64, 1, (v) => params.columnCount.value = v, () => params.columnCount.value));
  refreshers.push(rangeRow(coneGroup, 'Altura Cono', state, 'coneHeight', 1, 15, 0.5, (v) => params.coneHeight.value = v, () => params.coneHeight.value));
  refreshers.push(rangeRow(coneGroup, 'Radio Cono', state, 'coneRadius', 0.5, 8, 0.25, (v) => params.coneRadius.value = v, () => params.coneRadius.value));
  refreshers.push(rangeRow(coneGroup, 'Amplitud Onda', state, 'columnWaveAmplitude', 0, 2, 0.05, (v) => params.columnWaveAmplitude.value = v, () => params.columnWaveAmplitude.value));

  const coneBtn = button(coneGroup, '🔺 Formar Cono por Columnas (N)', () => onColumnCone?.());
  coneBtn.className = 'btn-cube';
  coneBtn.style.marginTop = '6px';

  let columnWaveActive = false;
  const columnWaveBtn = document.createElement('button');
  columnWaveBtn.textContent = '🌊 Onda por Columna (M)';
  columnWaveBtn.className = 'btn-flow';
  columnWaveBtn.style.marginTop = '4px';
  columnWaveBtn.addEventListener('click', () => {
    columnWaveActive = !columnWaveActive;
    columnWaveBtn.textContent = columnWaveActive ? '⏹️ Detener Onda (M)' : '🌊 Onda por Columna (M)';
    columnWaveBtn.style.opacity = columnWaveActive ? '1' : '0.75';
    onToggleColumnWave?.();
  });
  coneGroup.append(columnWaveBtn);

  const sphereGroup = document.createElement('div');
  sphereGroup.className = 'group';
  sphereGroup.innerHTML = '<h2>Formaciones Esféricas & Voz</h2>';
  panel.append(sphereGroup);

  const compactBtn = button(sphereGroup, '🔮 Esfera Compacta (2)', () => onCompactSphere?.());
  compactBtn.className = 'btn-sphere';

  const voiceBtn = button(sphereGroup, '🗣️ Hablar / Oscilador (V)', () => onToggleVoice?.());
  voiceBtn.className = 'btn-voice';

  const clusterBtn = button(sphereGroup, '🪐 Esfera Agrupada (3)', () => onClusterSphere?.());
  clusterBtn.className = 'btn-cluster';

  const lightRow = document.createElement('div');
  lightRow.style.cssText = 'display:flex;gap:6px;margin-top:6px;';
  const lightUpBtn = document.createElement('button');
  lightUpBtn.textContent = '💡 Brillo + (K)';
  lightUpBtn.className = 'btn-sub';
  lightUpBtn.style.flex = '1';
  lightUpBtn.addEventListener('click', () => onLightUp?.());

  const lightDownBtn = document.createElement('button');
  lightDownBtn.textContent = '🌙 Brillo - (L)';
  lightDownBtn.className = 'btn-sub';
  lightDownBtn.style.flex = '1';
  lightDownBtn.addEventListener('click', () => onLightDown?.());

  lightRow.append(lightUpBtn, lightDownBtn);
  sphereGroup.append(lightRow);

  const actions = document.createElement('div');
  actions.className = 'group';
  actions.innerHTML = '<h2>Modo Cuadro & División</h2>';
  panel.append(actions);

  const cubeBtn = button(actions, '📦 Crear Cuadro (1)', () => onCreateCube?.());
  cubeBtn.className = 'btn-cube';

  const row = document.createElement('div');
  row.style.cssText = 'display:flex;gap:6px;';
  const divideBtn = document.createElement('button');
  divideBtn.textContent = '✂️ Dividir (D)';
  divideBtn.className = 'btn-sub';
  divideBtn.style.flex = '1';
  divideBtn.addEventListener('click', () => onDivideCube?.());

  const mergeBtn = document.createElement('button');
  mergeBtn.textContent = '🧩 Juntar (X)';
  mergeBtn.className = 'btn-sub';
  mergeBtn.style.flex = '1';
  mergeBtn.addEventListener('click', () => onMergeCube?.());

  row.append(divideBtn, mergeBtn);
  actions.append(row);

  const freezeGroup = document.createElement('div');
  freezeGroup.className = 'group';
  freezeGroup.innerHTML = '<h2>Centrar & Congelar</h2><p style="opacity:0.7;font-size:0.85em;">Colapsa suavemente en una mini esfera en el origen y silencia las fuerzas extra (deriva, voz, onda por columna) sin cortar el movimiento de golpe.</p>';
  panel.append(freezeGroup);

  refreshers.push(rangeRow(freezeGroup, 'Radio Mini Esfera', state, 'freezeRadius', 0.1, 2, 0.05, (v) => params.freezeRadius.value = v, () => params.freezeRadius.value));

  let freezeActive = false;
  const freezeBtn = document.createElement('button');
  freezeBtn.textContent = '❄️ Centrar y Congelar (C)';
  freezeBtn.className = 'btn-flow';
  freezeBtn.style.marginTop = '6px';
  freezeBtn.addEventListener('click', () => {
    freezeActive = !freezeActive;
    freezeBtn.textContent = freezeActive ? '▶️ Reanudar Movimiento (C)' : '❄️ Centrar y Congelar (C)';
    freezeBtn.style.opacity = freezeActive ? '1' : '0.75';
    onToggleFreeze?.();
  });
  freezeGroup.append(freezeBtn);

  const presetGroup = document.createElement('div');
  presetGroup.className = 'group';
  presetGroup.innerHTML = '<h2>Presets</h2>';
  panel.append(presetGroup);

  const presetRow = document.createElement('div');
  presetRow.style.cssText = 'display:flex;gap:6px;';
  const inertiaBtn = document.createElement('button');
  inertiaBtn.textContent = '🪨 Inercia (I)';
  inertiaBtn.className = 'btn-sub';
  inertiaBtn.style.flex = '1';
  inertiaBtn.addEventListener('click', () => onPresetInertia?.());

  const windBtn = document.createElement('button');
  windBtn.textContent = '🍃 Viento (W)';
  windBtn.className = 'btn-sub';
  windBtn.style.flex = '1';
  windBtn.addEventListener('click', () => onPresetWind?.());

  presetRow.append(inertiaBtn, windBtn);
  presetGroup.append(presetRow);

  const cameraGroup = document.createElement('div');
  cameraGroup.className = 'group';
  cameraGroup.innerHTML = '<h2>Cámara</h2>';
  panel.append(cameraGroup);

  [4, 5, 6, 7].forEach((slot, idx) => {
    const slotRow = document.createElement('div');
    slotRow.style.cssText = 'display:flex;gap:6px;margin-bottom:4px;';

    const saveBtn = document.createElement('button');
    saveBtn.textContent = `💾 Guardar Vista ${idx + 1} (Shift+${slot})`;
    saveBtn.className = 'btn-sub';
    saveBtn.style.flex = '1';
    saveBtn.addEventListener('click', () => onSaveCameraSlot?.(slot));

    const goBtn = document.createElement('button');
    goBtn.textContent = `📷 Ir a Vista ${idx + 1} (${slot})`;
    goBtn.className = 'btn-sub';
    goBtn.style.flex = '1';
    goBtn.addEventListener('click', () => onTravelCameraSlot?.(slot));

    slotRow.append(saveBtn, goBtn);
    cameraGroup.append(slotRow);
  });

  const gyroGroup = document.createElement('div');
  gyroGroup.className = 'group';
  gyroGroup.innerHTML = '<h2>Giroscopio de Cámara</h2><p style="opacity:0.7;font-size:0.85em;">Gira la cámara sobre los 3 ejes al mismo tiempo. La velocidad de cada eje se controla por separado (negativo invierte el sentido).</p>';
  panel.append(gyroGroup);

  if (gyro) {
    refreshers.push(rangeRow(gyroGroup, 'Velocidad Eje X', gyro, 'speedX', -2, 2, 0.05));
    refreshers.push(rangeRow(gyroGroup, 'Velocidad Eje Y', gyro, 'speedY', -2, 2, 0.05));
    refreshers.push(rangeRow(gyroGroup, 'Velocidad Eje Z', gyro, 'speedZ', -2, 2, 0.05));

    const gyroBtn = document.createElement('button');
    const setGyroLabel = () => {
      gyroBtn.textContent = gyro.enabled ? '⏹️ Detener Giroscopio (G)' : '🎡 Activar Giroscopio (G)';
      gyroBtn.style.opacity = gyro.enabled ? '1' : '0.75';
    };
    gyroBtn.className = 'btn-flow';
    gyroBtn.style.marginTop = '6px';
    setGyroLabel();
    gyroBtn.addEventListener('click', () => {
      gyro.enabled = !gyro.enabled;
      setGyroLabel();
    });
    gyroGroup.append(gyroBtn);
  }

  const extraActions = document.createElement('div');
  extraActions.className = 'group';
  extraActions.innerHTML = '<h2>Acciones</h2>';
  panel.append(extraActions);

  const beatBtn = button(extraActions, '✨ Mini Beat (B)', () => onBeat?.());
  beatBtn.className = 'btn-beat';

  button(extraActions, 'Reset', onReset);
  button(extraActions, 'Pausar / continuar', () => onPauseChange());
  button(extraActions, 'LAB / PERFORMANCE', () => onModeChange());

  document.body.append(panel);

  return {
    element: panel,
    setVisible(visible) { panel.classList.toggle('hidden', !visible); },
    refresh() { for (const item of refreshers) item.refresh(); }
  };
}
````
CreateSimulation.js
````js
import * as THREE from 'three/webgpu';
import {
  Fn,
  If,
  color,
  float, // Mantenemos float si se usa, o puedes quitarlo si no hay drag
  hash,
  instanceIndex,
  instancedArray,
  mix,
  mod,
  step,
  uint,
  uv,
  vec3,
  vec4
} from 'three/tsl';

export function createSimulation({ renderer, scene, params, count = 131072 }) {
  const positionBuffer = instancedArray(count, 'vec3');
  const velocityBuffer = instancedArray(count, 'vec3');
  const homePositionBuffer = instancedArray(count, 'vec3');

  const initParticles = Fn(() => {
    const i = instanceIndex;
    const p = positionBuffer.element(i);
    const v = velocityBuffer.element(i);
    const home = homePositionBuffer.element(i);

    const r1 = hash(i.add(uint(11)));
    const r2 = hash(i.add(uint(23)));
    const r3 = hash(i.add(uint(37)));
    const r4 = hash(i.add(uint(53)));
    const r5 = hash(i.add(uint(71)));
    const r6 = hash(i.add(uint(89)));

    const initPos = vec3(r1, r2, r3).sub(0.5).mul(params.boundsSize.mul(0.45));
    p.assign(initPos);
    home.assign(initPos);
    v.assign(vec3(r4, r5, r6).sub(0.5).mul(params.initialSpeed));
  })().compute(count).setName('Initialize Particles');

  const updateParticles = Fn(() => {
    const p = positionBuffer.element(instanceIndex);
    const v = velocityBuffer.element(instanceIndex);
    const home = homePositionBuffer.element(instanceIndex);

    const dt = params.dt.mul(params.timeScale);

    const localTarget = home.toVar();

    // Las modulaciones extra (voz, onda por columna) se silencian mientras
    // está "congelado", pero el resorte de retorno sigue activo siempre,
    // así el movimiento nunca se corta de golpe: simplemente se relaja
    // hacia el nuevo home (la mini esfera) con la misma física suave que
    // usan todas las demás formaciones.
    If(params.frozen.lessThan(0.5), () => {
      If(params.voiceOscillator.greaterThan(0.001), () => {
        const len = localTarget.length();
        If(len.greaterThan(0.001), () => {
          const dir = localTarget.div(len);
          const wave1 = params.time.mul(8.0).add(dir.x.mul(4.0)).sin();
          const wave2 = params.time.mul(6.0).add(dir.y.mul(5.0)).cos();
          const wave3 = params.time.mul(10.0).add(dir.z.mul(6.0)).sin();
          const bulge = wave1.add(wave2).add(wave3).mul(0.33).mul(params.voiceIntensity);
          localTarget.addAssign(dir.mul(bulge.mul(params.voiceOscillator)));
        });
      });

      // Efecto de cono por columnas: cada columna oscila con su propia
      // fase y frecuencia, generando un movimiento distinto por columna.
      If(params.columnWaveEnabled.greaterThan(0.5), () => {
        const colCountUint = uint(params.columnCount);
        const col = mod(instanceIndex, colCountUint).toFloat();
        const phase = col.mul(0.37);
        const freq = float(1.0).add(mod(col, float(5.0)).mul(0.35));

        const swayX = params.time.mul(freq).add(phase).sin().mul(params.columnWaveAmplitude);
        const bobY = params.time.mul(freq.mul(0.7)).add(phase.mul(1.3)).cos().mul(params.columnWaveAmplitude.mul(0.5));

        localTarget.addAssign(vec3(swayX, bobY, 0.0));
      });
    });

    const half = params.boundsSize.mul(0.5);
    const shiftedHome = localTarget.add(params.globalOffset);
    const targetHome = mod(shiftedHome.add(half), params.boundsSize).sub(half).toVar();

    const delta = targetHome.sub(p).toVar();
    const bounds = params.boundsSize;
    delta.assign(delta.sub(bounds.mul(delta.div(bounds).round())));

    const returnForce = delta.mul(params.returnSpeed);
    const force = returnForce.toVar();

    v.addAssign(force.mul(dt));
    v.assign(v.mul(params.damping));

    const speed = v.length();
    If(speed.greaterThan(params.maxSpeed), () => {
      v.assign(v.normalize().mul(params.maxSpeed));
    });

    p.addAssign(v.mul(dt));
    p.assign(mod(p.add(half), params.boundsSize).sub(half));
  })().compute(count).setName('Update Particles');

  const updateMiniSphereFormation = Fn(() => {
    const i = instanceIndex;
    const home = homePositionBuffer.element(i);

    const r1 = hash(i.add(uint(131)));
    const r2 = hash(i.add(uint(137)));
    const r3 = hash(i.add(uint(139)));

    const radius = r1.pow(0.333).mul(params.freezeRadius);
    const theta = r2.mul(Math.PI * 2.0);
    const cosPhi = r3.mul(2.0).sub(1.0);
    const sinPhi = cosPhi.mul(cosPhi).oneMinus().max(0.0).sqrt();

    const x = sinPhi.mul(theta.cos()).mul(radius);
    const y = sinPhi.mul(theta.sin()).mul(radius);
    const z = cosPhi.mul(radius);

    home.assign(vec3(x, y, z));
  })().compute(count).setName('Update Mini Sphere (Freeze)');

  const beatImpulse = Fn(() => {
    const p = positionBuffer.element(instanceIndex);
    const v = velocityBuffer.element(instanceIndex);
    const home = homePositionBuffer.element(instanceIndex);

    home.assign(p);

    const dir = p.normalize();
    const r1 = hash(instanceIndex.add(uint(101))).sub(0.5);
    const r2 = hash(instanceIndex.add(uint(103))).sub(0.5);
    const r3 = hash(instanceIndex.add(uint(107))).sub(0.5);
    const randDir = vec3(r1, r2, r3);

    v.assign(dir.mul(params.beatForce.mul(2.5)).add(randDir.mul(params.beatForce.mul(1.2))));
  })().compute(count).setName('Beat Impulse');

  const updateCubeFormation = Fn(() => {
    const i = instanceIndex;
    const home = homePositionBuffer.element(i);

    const gUint = uint(params.cubeGridSize);
    const totalCubes = gUint.mul(gUint).mul(gUint);

    const cubeIdx = mod(i, totalCubes);

    const gx = mod(cubeIdx, gUint).toFloat();
    const gy = mod(cubeIdx.div(gUint), gUint).toFloat();
    const gz = mod(cubeIdx.div(gUint.mul(gUint)), gUint).toFloat();

    const boxTotalSize = params.boundsSize.mul(0.65);
    const stepSize = boxTotalSize.div(params.cubeGridSize);
    const subBoxSize = stepSize.mul(0.75);

    const center = vec3(gx, gy, gz)
      .add(0.5)
      .sub(params.cubeGridSize.mul(0.5))
      .mul(stepSize);

    const r1 = hash(i.add(uint(17))).sub(0.5);
    const r2 = hash(i.add(uint(31))).sub(0.5);
    const r3 = hash(i.add(uint(47))).sub(0.5);
    const localOffset = vec3(r1, r2, r3).mul(subBoxSize);

    home.assign(center.add(localOffset));
  })().compute(count).setName('Update Cube Formation');

  const updateSphereFormation = Fn(() => {
    const i = instanceIndex;
    const home = homePositionBuffer.element(i);

    const r1 = hash(i.add(uint(101)));
    const r2 = hash(i.add(uint(103)));
    const r3 = hash(i.add(uint(107)));

    const radius = r1.pow(0.333).mul(2.2);
    const theta = r2.mul(Math.PI * 2.0);
    const cosPhi = r3.mul(2.0).sub(1.0);
    const sinPhi = cosPhi.mul(cosPhi).oneMinus().sqrt();

    const x = sinPhi.mul(theta.cos()).mul(radius);
    const y = sinPhi.mul(theta.sin()).mul(radius);
    const z = cosPhi.mul(radius);

    home.assign(vec3(x, y, z));
  })().compute(count).setName('Update Compact Sphere');

  const updateClusterSphereFormation = Fn(() => {
    const i = instanceIndex;
    const home = homePositionBuffer.element(i);

    const clusterIdx = mod(i, uint(16)).toFloat();

    const clusterTheta = clusterIdx.mul(2.399963);
    const clusterCosPhi = float(1.0).sub(clusterIdx.mul(2.0).add(1.0).div(16.0));
    const clusterSinPhi = clusterCosPhi.mul(clusterCosPhi).oneMinus().max(0.0).sqrt();

    const cx = clusterSinPhi.mul(clusterTheta.cos()).mul(3.8);
    const cy = clusterSinPhi.mul(clusterTheta.sin()).mul(3.8);
    const cz = clusterCosPhi.mul(3.8);
    const clusterCenter = vec3(cx, cy, cz);

    const r1 = hash(i.add(uint(211)));
    const r2 = hash(i.add(uint(213)));
    const r3 = hash(i.add(uint(217)));

    const subR = r1.pow(0.333).mul(0.9);
    const subTheta = r2.mul(6.2832);
    const subCosPhi = r3.mul(2.0).sub(1.0);
    const subSinPhi = subCosPhi.mul(subCosPhi).oneMinus().max(0.0).sqrt();

    const lx = subSinPhi.mul(subTheta.cos()).mul(subR);
    const ly = subSinPhi.mul(subTheta.sin()).mul(subR);
    const lz = subCosPhi.mul(subR);

    home.assign(clusterCenter.add(vec3(lx, ly, lz)));
  })().compute(count).setName('Update Cluster Sphere');

  const updateColumnConeFormation = Fn(() => {
    const i = instanceIndex;
    const home = homePositionBuffer.element(i);

    const colCountUint = uint(params.columnCount);
    const col = mod(i, colCountUint);
    const colFloat = col.toFloat();

    // Cuántas partículas le tocan a cada columna, y en qué posición
    // (altura) dentro de su columna cae esta partícula.
    const particlesPerColumn = float(count).div(params.columnCount);
    const indexInColumn = i.div(colCountUint).toFloat();
    const t = indexInColumn.div(particlesPerColumn).clamp(0.0, 1.0);

    const angle = colFloat.div(params.columnCount).mul(Math.PI * 2.0);
    const radiusAtHeight = params.coneRadius.mul(float(1.0).sub(t));

    const r1 = hash(i.add(uint(151))).sub(0.5);
    const jitter = r1.mul(0.15);

    const x = angle.cos().mul(radiusAtHeight.add(jitter));
    const z = angle.sin().mul(radiusAtHeight.add(jitter));
    const y = t.sub(0.5).mul(params.coneHeight);

    home.assign(vec3(x, y, z));
  })().compute(count).setName('Update Column Cone');

  const material = new THREE.SpriteNodeMaterial({
    blending: THREE.AdditiveBlending,
    depthWrite: false,
    transparent: true
  });

  material.positionNode = positionBuffer.toAttribute();

  const beatScaleFactor = params.beatIntensity.mul(0.85).add(1.0);
  material.scaleNode = params.particleSize.mul(beatScaleFactor);

  material.colorNode = Fn(() => {
    const speed = velocityBuffer.toAttribute().length();
    const t = speed.div(params.maxSpeed).clamp(0.0, 1.0);
    const slow = color('#46a6ff');
    const fast = color('#ffb35a');
    const baseColor = mix(slow, fast, t);

    const glowColor = color('#a6f3ff');
    const blended = mix(baseColor, glowColor, params.beatIntensity.mul(0.65));
    const brightnessBoost = params.beatIntensity.mul(2.0).add(1.0).mul(params.brightnessMultiplier);

    return vec4(blended.mul(brightnessBoost), 1.0);
  })();

  material.opacityNode = step(uv().xy.sub(0.5).length(), 0.5);

  const geometry = new THREE.PlaneGeometry(1, 1);
  const mesh = new THREE.InstancedMesh(geometry, material, count);
  mesh.frustumCulled = false;
  scene.add(mesh);

  function reset() {
    renderer.compute(initParticles);
  }

  function stepSimulation() {
    renderer.compute(updateParticles);
  }

  function triggerBeat() {
    params.beatIntensity.value = 1.0;
    renderer.compute(beatImpulse);
  }

  function setCubeGrid(gridSize) {
    const clamped = Math.max(1, Math.min(8, Math.round(gridSize)));
    params.cubeGridSize.value = clamped;
    renderer.compute(updateCubeFormation);
    params.beatIntensity.value = 0.75;
  }

  function setCompactSphere() {
    renderer.compute(updateSphereFormation);
    params.beatIntensity.value = 0.75;
  }

  function setClusterSphere() {
    renderer.compute(updateClusterSphereFormation);
    params.beatIntensity.value = 0.75;
  }

  function toggleVoiceOscillator() {
    params.voiceOscillator.value = params.voiceOscillator.value > 0.0 ? 0.0 : 1.0;
  }

  function centerAndFreezeSim() {
    params.frozen.value = 1.0;
    renderer.compute(updateMiniSphereFormation);
    params.beatIntensity.value = 0.4;
  }

  function unfreeze() {
    params.frozen.value = 0.0;
  }

  function setColumnCone() {
    renderer.compute(updateColumnConeFormation);
    params.beatIntensity.value = 0.75;
  }

  function toggleColumnWave() {
    params.columnWaveEnabled.value = params.columnWaveEnabled.value > 0.0 ? 0.0 : 1.0;
  }

  function dispose() {
    geometry.dispose();
    material.dispose();
    scene.remove(mesh);
  }

  return {
    count,
    positionBuffer,
    velocityBuffer,
    reset,
    stepSimulation,
    triggerBeat,
    setCubeGrid,
    setCompactSphere,
    setClusterSphere,
    toggleVoiceOscillator,
    centerAndFreeze: centerAndFreezeSim,
    unfreeze,
    setColumnCone,
    toggleColumnWave,
    dispose
  };
}
````
parameters.js  
````js
import * as THREE from 'three/webgpu';
import { uniform } from 'three/tsl';

export function createParameters() {
  return {
    dt: uniform(1 / 60),
    timeScale: uniform(1.0),
    initialSpeed: uniform(0.35),
    maxSpeed: uniform(5.0),
    boundsSize: uniform(10.0),
    particleSize: uniform(0.035),

    time: uniform(0.0),
    flashColor: uniform(new THREE.Color('#ffffff')),
    beatIntensity: uniform(0.0),
    beatForce: uniform(1.5),
    returnSpeed: uniform(25.0),
    damping: uniform(0.92),
    cubeGridSize: uniform(1.0),
    brightnessMultiplier: uniform(1.0),
    voiceOscillator: uniform(0.0),
    voiceIntensity: uniform(1.2),
    
    // Controles de Flujo / Viento
    driftX: uniform(0.0),
    driftY: uniform(0.0),
    driftZ: uniform(0.0),
    flowSpeed: uniform(3.0),
    
    globalOffset: uniform(new THREE.Vector3(0, 0, 0)),

    // Centrar / Congelar
    frozen: uniform(0.0),
    freezeRadius: uniform(0.5),

    // Cono por Columnas
    columnCount: uniform(24.0),
    coneHeight: uniform(6.0),
    coneRadius: uniform(3.0),
    columnWaveEnabled: uniform(0.0),
    columnWaveAmplitude: uniform(0.6)
  };
}
````

## Foto pruebas  
<img width="1191" height="828" alt="image" src="https://github.com/user-attachments/assets/3ee41d94-c5eb-41f3-90ba-8f671e36469d" />  
<img width="1173" height="1247" alt="image" src="https://github.com/user-attachments/assets/027fe20e-c156-4cc8-9543-67b9e28c7e66" />
<img width="1141" height="1079" alt="image" src="https://github.com/user-attachments/assets/53c7592d-9f05-4355-8f44-c188345eb29b" />
<img width="1739" height="1208" alt="image" src="https://github.com/user-attachments/assets/e3e4b75b-ab40-44d2-bd70-9e24107b32cc" />
<img width="1764" height="1022" alt="image" src="https://github.com/user-attachments/assets/f7e1567c-d3c0-42e9-b7ff-acc9a646405a" />










