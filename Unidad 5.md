[Link](https://ayepes2402.github.io/R5/)  

## Concepto Central:Un ecosistema vivo y persistente inspirado en las redes de micelio (hongos), diseñado para interpretar el guion institucional mediante relaciones estructurales y movimiento, rechazando el modelo tradicional de partículas efímeras.

## Desarrollo de Concepto
* **Rechazo del modelo clásico:** Desde el inicio se descartó el enfoque de partículas que se destruyen y reaparecen. El relevo generacional no se entiende como borrar lo viejo e imponer lo nuevo, sino como un proceso de coexistencia y transformación mutua del entorno.
* **Inspiración biológica (Micelio):** Se construyó un ecosistema fijo de **140 agentes persistentes** que nunca desaparecen ni se reinician con los cambios de diapositiva:
  * **40% Experiencia:** Elementos más gruesos y lentos encargados de sostener la red estructural.
  * **60% Jóvenes:** Elementos delgados y rápidos orientados a la exploración.



## Registro de Pruebas y Descartes  
**Movimiento Orgánico (Curl Noise 2D):**  
   * *Problema inicial:* El código base posicionaba las partículas usando geometrías demasiado estrictas y forzadas.
   * *Solución:* Se programó un campo de flujo mediante *Curl Noise 2D*, logrando un movimiento natural que asemeja a microorganismos expandiéndose orgánicamente.
     
**Control de Rastros y Legibilidad:**  
   * *Problema inicial:* Al hacer que los agentes dejaran un rastro permanente para simular crecimiento, la pantalla se saturaba rápidamente y arruinaba la legibilidad del texto.
   * *Solución:* Se aplicaron tres medidas técnicas: un desvanecimiento ultra lento usando `destination-out`, un gradiente oscuro fijo detrás del texto, y una fuerza de repulsión que obliga a los agentes a esquivar literalmente el bloque de texto.
     
**Inmersión y Profundidad (Parallax y Cursor):**  
   * Se implementó un efecto *parallax* (cálculo de la posición del mouse mediante `lerp`) para dividir la escena en tres planos de profundidad (fondo, texto y partículas).
   * Se añadió una fuerza de repulsión volumétrica al cursor para demostrar que el ecosistema está vivo: las partículas se apartan de forma natural sin romper los resortes que las unen.


## Matriz de Parámetros y Gramática Visual  
Los parámetros físicos se derivaron directamente de la narrativa del guion institucional:  
* **`gravity` (Convocatoria):** El Fórum actúa como fuerza de atracción (*steering*) hacia el centro o hacia tres polos específicos cuando se aborda el bloque de *Academia + Industria + Ciudad*.  
* **`clumping` (Aislamiento):** Separa a los agentes en masas diferenciadas según su pertenencia generacional.
* **`elasticity` (Confianza):** Define el umbral de conexión, la rigidez del resorte entre partículas y el número máximo de enlaces soportados por agente.  
* **`exploration` (Rutas nuevas):** Mide la capacidad de búsqueda (las nuevas generaciones operan al 100% y la experiencia al 45%, generando dinámicas de movimiento contrastadas).  
* **`intensity` (Energía):** Controla la velocidad global de la simulación.  

---

## El Argumento Central en Código (`buildLinks()`)  
El núcleo conceptual del proyecto se demuestra directamente en la función `buildLinks()`:  
* Con una confianza de `0.00`, no existe ningún enlace.  
* Con una confianza de `0.10`, comienzan a aparecer conexiones, pero el **100% ocurren entre generaciones distintas** (cero enlaces entre iguales).  
* Solo a partir de un umbral de `0.48` se empiezan a tejer enlaces entre agentes de la misma generación.  
* **Tesis visual:** *La confianza y el tejido social se construyen primero en la diversidad.*  


## Demostración y Panel de Debug
* **Panel de Debug (Tecla `D`):** Herramienta integrada para visualizar en tiempo real los cinco parámetros físicos, los FPS y la comparativa de enlaces cruzados frente a normales. Esto permite justificar durante la sustentación que el comportamiento responde estrictamente a modelos matemáticos y físicos, y no a una animación pregrabada.
* **Interacción con el Cursor:** Un auditorio estéril no reacciona; una comunidad viva sí. El estímulo externo del mouse demuestra cómo el sistema se reorganiza y adapta orgánicamente sin perder su cohesión estructural.  
