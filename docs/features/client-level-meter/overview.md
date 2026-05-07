# Resumen del medidor de nivel de salida

El medidor de nivel de salida es un medidor dB vertical que muestra el nivel pico suavizado post-procesamiento de una etapa de audio. Le proporciona una lectura visual y numérica continua de qué tan cerca está la señal de salida del recorte, para que pueda ajustar los niveles de excitación y salida sin tener que adivinar.

## Cómo funciona

El medidor recibe actualizaciones del nivel pico desde el motor de audio y aplica balística de ataque rápido / liberación lenta antes de mostrar el resultado. Cuando el nivel entrante aumenta, el factor de suavizado es 0.6 (ataque rápido), por lo que la barra reacciona rápidamente a los picos. Cuando el nivel disminuye, el factor de suavizado es 0.08 (liberación lenta), por lo que la barra decae gradualmente. Este comportamiento balístico coincidente se comparte con el medidor del fader de salida del ecualizador, por lo que todos los medidores en AetherSDR se sienten visualmente consistentes.

El medidor es visible dentro del editor sin marco del applet Tube, a la derecha de la curva de saturación. Ábralo haciendo doble clic en la etapa TUBE en el widget de la cadena. La misma balística también es utilizada por el medidor del fader de salida del editor del ecualizador.

No se guarda ninguna configuración para este widget. No tiene controles interactivos; todos los elementos son indicadores de solo lectura.

## Qué hace cada control

| Elemento | Descripción | Rango / Valores |
|---|---|---|
| Etiqueta del encabezado | Identifica qué está midiendo el medidor. El applet Tube lo establece en `OUT`. Una cadena vacía oculta el encabezado. | Cualquier cadena corta; valor predeterminado `OUT` |
| Barra de nivel | Barra vertical con relleno degradado que muestra el nivel pico suavizado. Se llena de abajo hacia arriba, proporcional al valor dB actual. | −60 dB (abajo) a 0 dB (arriba) |
| Marcas de la escala dB | Cuadrícula de referencia estática a la izquierda de la barra con marcas etiquetadas. | 0, −6, −12, −20, −40 dB |
| Lectura numérica | Muestra el pico suavizado como un valor dB con signo y un decimal, centrado debajo de la barra. Muestra `-inf` cuando el nivel está por debajo de aproximadamente −59.5 dB. | `-inf` o un valor en la forma `+/-XX.X dB` |

### Color de la barra de nivel

El color de relleno cambia con el nivel para dar una sensación inmediata del margen de potencia:

| Color | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Nivel de operación normal |
| Lima | −12 dB a −6 dB | Nivel moderado |
| Ámbar | −6 dB a −3 dB | Acercándose al recorte |
| Rojo | Por encima de −3 dB | 3 dB o menos del recorte |

## Consejos

- Observe el color ámbar o rojo en la barra de nivel mientras ajusta las perillas de Drive o Output del applet Tube. El rojo significa que tiene 3 dB o menos de margen de potencia antes del recorte.
- La balística de liberación lenta (alfa 0.08) significa que la barra mantiene lecturas elevadas brevemente después de un pico. Esto es intencional: le permite captar transitorios que de otro modo desaparecerían antes de que los note.

## Relacionado

- [Lea el medidor de nivel de salida en el applet Tube](read-the-output-level-meter-on-the-tube-applet.md)
