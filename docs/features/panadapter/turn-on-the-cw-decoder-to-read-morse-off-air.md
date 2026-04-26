# Activar el decodificador de CW para leer código Morse en el aire

El panel del decodificador de CW permite leer el código Morse entrante como texto directamente debajo del panadapter. Úselo cuando desee una decodificación visual de una señal CW sin software externo.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panadapter requiere una conexión de radio activa.
- Enrute el audio del PC desde la radio hacia AetherSDR. El panel de CW muestra el aviso "(requires PC Audio)" — el decodificador trabaja sobre la señal de audio, no sobre los datos RF en bruto.
- Sintonice el slice activo sobre una señal CW.

## Pasos

1. Localice el panadapter correspondiente al slice que desea decodificar. El slice se identifica en la barra de título (por ejemplo, "Slice A").
2. Haga clic derecho sobre el espectro o el waterfall del panadapter para abrir el menú contextual y seleccione **Show CW Decoder**. El panel de decodificación de CW aparece como una banda fija debajo del waterfall.
3. Observe el área **CW decode text** en la parte inferior del panel. Los caracteres decodificados aparecen en secuencia a medida que se reciben, con color según el nivel de confianza.
4. Revise la etiqueta **CW stats label** en la barra superior del panel. Muestra el tono detectado y la velocidad en el formato `<hz> Hz  <wpm> WPM` una vez que el decodificador está siguiendo una señal.
5. Si aparecen demasiados caracteres de ruido, arrastre el deslizador **Sens** hacia la derecha para elevar el umbral. Si se están suprimiendo caracteres válidos, arrástrelo hacia la izquierda.
6. Ajuste el deslizador **Lo** para establecer el tono mínimo que busca el decodificador (valor predeterminado 500 Hz, rango 300–1200 Hz), y el deslizador **Hi** para establecer el máximo (valor predeterminado 700 Hz, rango 300–1200 Hz). Configure ambos para encuadrar el tono de la estación que está copiando.
7. Para cerrar el panel cuando termine, haga clic en **✕** en la barra del panel de CW.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **CW stats label** | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad detectados. |
| **Sens** | 30 | 0–100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Valores más altos son más estrictos. Asigna 0–100 a un umbral de costo interno de 1.0–0.1. |
| **🔒P (Lock Pitch)** | desactivado | activado / desactivado | — | Fija el tono del decodificador a la frecuencia sintonizada actual. |
| **🔒S (Lock Speed)** | desactivado | activado / desactivado | — | Fija la velocidad del decodificador al WPM actual. |
| **Lo** | 500 Hz | 300–1200 Hz | — | Tono mínimo que busca el decodificador. Limitado a ≤ Hi. |
| **Hi** | 700 Hz | 300–1200 Hz | — | Tono máximo que busca el decodificador. Limitado a ≥ Lo. |
| **CPY ALL** | — | — | — | Copia el texto decodificado completo al portapapeles. |
| **CPY VIS** | — | — | — | Copia solo el texto visible actualmente en el área de desplazamiento. |
| **CLR** | — | — | — | Borra el búfer de decodificación de CW. |
| **✕** | — | — | — | Oculta el panel de decodificación de CW. |
| **CW decode text** | — | solo lectura | — | Visualización continua del CW decodificado. El texto se colorea según el nivel de confianza: verde (mayor) pasando por amarillo y naranja hasta rojo (menor). |

## Consejos

- El color del texto decodificado indica el nivel de confianza. Los caracteres verdes son de alta confianza; los amarillos y naranjas son marginales; los rojos son de baja confianza y son los primeros en desaparecer cuando se sube el valor de **Sens**.
- Si el tono de la estación está fuera del rango de tono predeterminado de 500–700 Hz, el decodificador no lo seguirá. Amplíe **Lo** y **Hi** antes de concluir que el decodificador no funciona.
- Una vez que la etiqueta **CW stats label** muestra una lectura estable de Hz y WPM, use **🔒P** y **🔒S** para evitar que el decodificador se desvíe si aparece QRM en una frecuencia adyacente. Consulte [Fijar el tono o la velocidad del decodificador de CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md).
- Use **CLR** antes de copiar al portapapeles para capturar solo el QSO actual en lugar del texto acumulado de momentos anteriores.

## Solución de problemas

- **El área CW decode text está en blanco a pesar de tener una señal CW fuerte** — El decodificador requiere enrutamiento de audio del PC. Confirme que el audio de la radio está llegando a AetherSDR. La etiqueta "(requires PC Audio)" en el panel es un recordatorio de este requisito.
- **Las decodificaciones están distorsionadas o llenas de caracteres de ruido** — Arrastre el deslizador **Sens** hacia la derecha para elevar el umbral de confianza. Verifique también que **Lo** y **Hi** encuadren el tono real de la señal que se muestra en la etiqueta **CW stats label**.
- **No aparece ningún valor de Hz o WPM en la etiqueta CW stats label** — El decodificador no está detectando ninguna señal. Verifique que la señal esté dentro del rango de tono **Lo**–**Hi** y que el modo del slice esté configurado en CW.

## Relacionados

- [Ajustar la sensibilidad del decodificador de CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador de CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto de CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
