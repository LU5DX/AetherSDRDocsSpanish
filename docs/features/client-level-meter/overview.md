# Descripción general del medidor de nivel de salida

El medidor de nivel de salida es un medidor vertical en dB que muestra el nivel de pico posprocesado y suavizado de una etapa de audio. Proporciona una lectura visual y numérica continua de qué tan cerca está la señal de salida del recorte (clipping), para que pueda ajustar los niveles de ganancia y salida sin necesidad de adivinar.

## Cómo funciona

El medidor recibe actualizaciones del nivel de pico desde el motor de audio y aplica una dinámica de ataque rápido / liberación lenta antes de mostrar el resultado. Cuando el nivel de entrada sube, el factor de suavizado es 0.6 (ataque rápido), por lo que la barra reacciona rápidamente a los picos. Cuando el nivel baja, el factor de suavizado es 0.08 (liberación lenta), por lo que la barra decae gradualmente. Este comportamiento dinámico compartido también lo utiliza el medidor del fader de salida del EQ, de modo que todos los medidores en AetherSDR tienen una apariencia visual coherente.

El medidor es visible dentro del editor sin marco del applet Tube, a la derecha de la curva de saturación. Ábralo haciendo doble clic en la etapa TUBE en el widget de cadena. Las mismas dinámicas también son utilizadas por el medidor del Output Fader del editor de EQ.

No se guardan ajustes para este widget. No tiene controles interactivos; todos los elementos son indicadores de solo lectura.

## Qué hace cada control

| Elemento | Descripción | Rango / Valores |
|---|---|---|
| Etiqueta de encabezado | Identifica qué está midiendo el medidor. El applet Tube la establece como `OUT`. Una cadena vacía oculta el encabezado. | Cualquier cadena corta; valor predeterminado `OUT` |
| Barra de nivel | Barra vertical con relleno degradado que muestra el nivel de pico suavizado. Se llena de abajo hacia arriba, en proporción al valor actual en dB. | −60 dB (abajo) a 0 dB (arriba) |
| Marcas de escala dB | Cuadrícula de referencia estática a la izquierda de la barra con marcas etiquetadas. | 0, −6, −12, −20, −40 dB |
| Lectura numérica | Muestra el pico suavizado como un valor en dB con signo y un decimal, centrado debajo de la barra. Muestra `-inf` cuando el nivel está por debajo de aproximadamente −59.5 dB. | `-inf` o un valor en la forma `+/-XX.X dB` |

### Color de la barra de nivel

El color de relleno cambia con el nivel para dar una indicación inmediata del margen de headroom disponible:

| Color | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Nivel de operación normal |
| Verde lima | −12 dB a −6 dB | Nivel moderado |
| Ámbar | −6 dB a −3 dB | Aproximándose al recorte |
| Rojo | Por encima de −3 dB | A 3 dB o menos del recorte |

## Consejos

- Observe si aparecen los colores ámbar o rojo en la barra de nivel mientras ajusta los controles Drive o Output del applet Tube. El color rojo indica que tiene 3 dB o menos de headroom antes del recorte.
- La dinámica de liberación lenta (alpha 0.08) hace que la barra mantenga lecturas elevadas brevemente después de un pico. Esto es intencional: permite capturar transitorios que de otro modo desaparecerían antes de que usted los note.

## Relacionado

- [Leer el medidor de nivel de salida en el applet Tube](read-the-output-level-meter-on-the-tube-applet.md)
