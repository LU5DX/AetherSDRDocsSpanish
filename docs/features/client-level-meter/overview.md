# Resumen del Medidor de Nivel de Salida

El Medidor de Nivel de Salida es un medidor vertical en dB que muestra el nivel pico suavizado post-procesamiento de una etapa de audio. Le proporciona una lectura visual y numérica continua de qué tan cerca está la señal de salida del recorte, permitiéndole ajustar los niveles de excitación y salida sin necesidad de adivinar.

## Cómo funciona

El medidor recibe actualizaciones del nivel pico del motor de audio y aplica una balística de ataque rápido / liberación lenta antes de mostrar el resultado. Cuando el nivel entrante aumenta, el factor de suavizado es 0.6 (ataque rápido), por lo que la barra reacciona rápidamente a los picos. Cuando el nivel disminuye, el factor de suavizado es 0.08 (liberación lenta), por lo que la barra decae gradualmente. Este comportamiento balístico coincidente se comparte con el medidor del fader de salida del ecualizador, por lo que todos los medidores en AetherSDR se sienten visualmente consistentes.

El medidor es visible dentro del editor sin marco del applet Tube, a la derecha de la curva de saturación. Ábralo haciendo doble clic en la etapa TUBE en el widget de cadena. La misma balística también es utilizada por el medidor del fader de salida del editor de EQ.

No se persiste ninguna configuración para este widget. No tiene controles interactivos; todos los elementos son indicadores de solo lectura.

### Limitación de la lectura numérica

La lectura numérica de dB debajo de la barra se actualiza a 10 Hz (intervalos de 100 ms), aunque la barra de nivel se anima en cada evento de pintado. Esto mantiene los dígitos estables y legibles mientras la barra continúa mostrando cambios de nivel suaves. La lectura muestra `-inf` cuando el nivel pico suavizado está por debajo de aproximadamente −59.5 dB, y se reformatea a un valor de dB con signo y un decimal en caso contrario.

### Soporte de temas

El color de relleno de la barra de nivel se obtiene del token de tema `color.meter.bar.fillGradient`. Cuando modifica este token en el Editor de Temas, el medidor se actualiza inmediatamente sin necesidad de reiniciar AetherSDR. El degradado es un degradado lineal de 5 paradas que se asigna desde la parte inferior hasta la superior de la tira completa de la barra. A medida que el nivel de la señal aumenta, el relleno visible crece hacia arriba a través del degradado, por lo que el color en la parte inferior del relleno siempre coincide con lo que esa posición en el degradado mostraría.

## Qué hace cada control

| Elemento | Descripción | Rango / Valores |
|---|---|---|
| Etiqueta de encabezado | Identifica qué está midiendo el medidor. El applet Tube lo establece en `OUT`. Una cadena vacía oculta el encabezado. | Cualquier cadena corta; predeterminado `OUT` |
| Barra de nivel | Barra vertical con relleno degradado que muestra el nivel pico suavizado. Se llena de abajo hacia arriba, proporcional al valor de dB actual. El degradado de relleno se define mediante el tema con `color.meter.bar.fillGradient`. | −60 dB (inferior) a 0 dB (superior) |
| Marcas de escala en dB | Cuadrícula de referencia estática a la izquierda de la barra con marcas etiquetadas. | 0, −6, −12, −20, −40 dB |
| Lectura numérica | Muestra el pico suavizado como un valor de dB con signo y un decimal, centrado debajo de la barra. Se actualiza a 10 Hz. Muestra `-inf` cuando el nivel está por debajo de aproximadamente −59.5 dB. | `-inf` o un valor en la forma `+/-XX.X dB` |

### Color de la barra de nivel

El color de relleno cambia con el nivel para proporcionar una sensación inmediata del margen de operación. Las paradas exactas del degradado se definen mediante el token de tema `color.meter.bar.fillGradient`. El degradado predeterminado produce:

| Color | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Nivel de operación normal |
| Lima | −12 dB a −6 dB | Nivel moderado |
| Ámbar | −6 dB a −3 dB | Acercándose al recorte |
| Rojo | Por encima de −3 dB | 3 dB o menos del recorte |

## Consejos

- Observe si aparece color ámbar o rojo en la barra de nivel mientras ajusta los mandos de Drive o Output del applet Tube. El color rojo significa que tiene 3 dB o menos de margen antes del recorte.
- La balística de liberación lenta (alfa 0.08) hace que la barra mantenga lecturas elevadas brevemente después de un pico. Esto es intencional: le permite captar transitorios que de otro modo desaparecerían antes de que pueda notarlos.
- La lectura numérica puede parecer que se "retrasa" con respecto a la barra de nivel hasta 100 ms. Esto es normal: la barra se anima suavemente mientras los dígitos se actualizan a una velocidad fija de 10 Hz para facilitar la lectura.
- Para cambiar los colores de relleno del medidor, edite el token `color.meter.bar.fillGradient` en el Editor de Temas. El medidor se vuelve a renderizar inmediatamente para mostrar sus cambios.

## Relacionado

- [Lea el medidor de nivel de salida en el applet Tube](read-the-output-level-meter-on-the-tube-applet.md)
