# Activar el decodificador CW para leer Morse en el aire

El panel de decodificación CW muestra el texto Morse decodificado directamente debajo de un panadapter. Úselo para leer CW en el aire sin necesidad de una aplicación separada.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El decodificador CW requiere una conexión de radio activa.
- El audio de PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio — la decodificación no funcionará sin una fuente de audio.
- El slice activo debe estar en modo CW para que el radio pase el audio apropiado.

## Pasos

1. Localice el panadapter correspondiente al slice que desea decodificar.
2. Haga clic derecho en el área del espectro o del waterfall de ese panadapter para abrir el menú contextual y seleccione **CW Decoder**. El panel de decodificación CW aparece como una franja debajo del waterfall.
3. Confirme que el panel es visible. Muestra la etiqueta **CW** y la indicación **(requires PC Audio)** a la izquierda, seguida de los controles **Sens**, 🔒P, 🔒S, **Lo**, **Hi**, **CPY ALL**, **CPY VIS**, **CLR** y ✕.
4. Sintonice una señal CW. El texto decodificado aparece en la pantalla deslizante en la parte inferior del panel, con colores según el nivel de confianza.
5. Si no aparece texto, ajuste los controles deslizantes **Lo** y **Hi** para delimitar el tono de la señal. El rango de búsqueda predeterminado es de 500 Hz (**Lo**) a 700 Hz (**Hi**).
6. Observe la etiqueta de estadísticas CW — muestra el tono detectado y la velocidad en el formato `<hz> Hz  <wpm> WPM` una vez que el decodificador se sincroniza.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Sens** | 30 | 0–100 | `CwDecoderSensitivity` | Filtra decodificaciones de baja confianza. Valores más altos rechazan caracteres más inciertos. Asigna 0–100 a un umbral de costo de 1.0–0.1. |
| **🔒P (Lock Pitch)** | Off | On / Off | — | Fija el decodificador al tono detectado actualmente para que deje de escanear. |
| **🔒S (Lock Speed)** | Off | On / Off | — | Fija el decodificador a los WPM detectados actualmente. |
| **Lo** | 500 Hz | 300–1200 Hz | — | Límite inferior del rango de tono en el que busca el decodificador. Limitado a ≤ **Hi**. |
| **Hi** | 700 Hz | 300–1200 Hz | — | Límite superior del rango de tono en el que busca el decodificador. Limitado a ≥ **Lo**. |
| **CPY ALL** | — | — | — | Copia el contenido completo del búfer de texto decodificado al portapapeles. |
| **CPY VIS** | — | — | — | Copia únicamente el texto visible en el área de desplazamiento al portapapeles. |
| **CLR** | — | — | — | Borra el búfer de texto decodificado. |
| **✕** | — | — | — | Oculta el panel de decodificación CW. |
| Etiqueta de estadísticas CW | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad que ha detectado el decodificador. |
| Texto decodificado CW | — | — | — | Pantalla deslizante de solo lectura. El texto aparece en verde (mayor confianza), pasando por amarillo, naranja y rojo (menor confianza). |

## Consejos

- Comience con el rango predeterminado **Lo** / **Hi** de 500–700 Hz. La mayoría de los operadores CW utilizan un tono lateral en este rango. Amplíe la ventana solo si sabe que la señal está fuera de ella.
- Una vez que la etiqueta de estadísticas muestre un tono y una velocidad estables, presione **🔒P** y **🔒S** para evitar que el decodificador derive hacia el ruido.
- Aumente **Sens** si aparecen caracteres erróneos en el texto. Reducirlo admite una salida más incierta, lo que puede ayudar con señales débiles a costa de más errores.
- Use **CLR** antes de un nuevo QSO para mantener la pantalla de texto ordenada y, luego, **CPY ALL** para guardar el intercambio en el portapapeles.

## Solución de problemas

- **No aparece texto a pesar de una señal CW fuerte** — El decodificador requiere enrutamiento de audio de PC. Verifique que el audio del radio esté llegando a AetherSDR. La indicación "(requires PC Audio)" en el panel confirma esta dependencia.
- **El texto decodificado es mayormente incorrecto** — Suba el control deslizante **Sens** hacia 100 para rechazar caracteres de baja confianza y estreche el rango **Lo**/**Hi** para rodear únicamente el tono real de la señal que muestra la etiqueta de estadísticas.
- **La etiqueta de estadísticas no muestra tono ni velocidad** — El tono de la señal probablemente está fuera de la ventana de búsqueda **Lo**–**Hi**. Amplíe la ventana o ajuste **Lo** y **Hi** para delimitar la frecuencia de tono audible.
- **El panel CW ha desaparecido** — Fue cerrado con ✕. Ábralo nuevamente desde el menú contextual del panadapter.

## Relacionado

- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
