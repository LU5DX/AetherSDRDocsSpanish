# Activar el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW se encuentra debajo del espectro y la cascada (waterfall) del panadapter y muestra en tiempo real el texto Morse decodificado. Úselo para leer estaciones en CW sin necesidad de una aplicación de decodificación independiente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El decodificador de CW requiere una conexión de radio activa.
- El audio del PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio — la decodificación no funcionará sin él.
- Sintonice una señal CW y establezca el modo del slice en CW.

## Pasos

1. Localice el panadapter que contiene el slice que desea decodificar.
2. Haga clic derecho sobre el área del espectro o la cascada del panadapter para abrir el menú contextual y seleccione **Show CW Decoder**. El panel de decodificación de CW aparece debajo de la cascada.
3. Confirme que el panel es visible: muestra la etiqueta **CW**, el aviso **(requires PC Audio)**, un control deslizante **Sens** y un área de texto con desplazamiento.
4. Ajuste el control deslizante **Lo** para establecer el tono mínimo que buscará el decodificador (valor predeterminado 500 Hz, rango 300–1200 Hz).
5. Ajuste el control deslizante **Hi** para establecer el tono máximo (valor predeterminado 700 Hz, rango 300–1200 Hz). **Lo** se limita automáticamente a un valor ≤ **Hi**.
6. Observe el área de texto **CW decode text**. Los caracteres decodificados aparecen con colores según el nivel de confianza: verde (más alto), amarillo, naranja o rojo (más bajo).
7. La etiqueta **CW stats label** que aparece sobre el área de texto muestra el tono y la velocidad detectados en el formato `<hz> Hz  <wpm> WPM` una vez que el decodificador está siguiendo una señal.
8. Para cerrar el panel al terminar, haga clic en **✕** (close CW) en el extremo derecho de la barra de controles.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango / valores | Clave de configuración |
|---|---|---|---|---|
| Control deslizante **Sens** | Filtra las decodificaciones de baja confianza. Valores más altos rechazan más ruido. | 30 | 0–100 | `CwDecoderSensitivity` |
| **🔒P (Lock Pitch)** | Fija el tono del decodificador en la frecuencia sintonizada actualmente. | Off | On / Off | — |
| **🔒S (Lock Speed)** | Fija la velocidad del decodificador en el valor WPM actual. | Off | On / Off | — |
| Control deslizante **Lo** | Tono mínimo que busca el decodificador (Hz). Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz | — |
| Control deslizante **Hi** | Tono máximo que busca el decodificador (Hz). Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz | — |
| **CW stats label** | Muestra el tono y la velocidad detectados. | — | `<hz> Hz  <wpm> WPM` | — |
| **CW decode text** | Pantalla deslizante de solo lectura de los caracteres decodificados, con colores según el nivel de confianza. | — | — | — |
| **CPY ALL** | Copia el buffer completo de texto decodificado al portapapeles. | — | — | — |
| **CPY VIS** | Copia al portapapeles únicamente el texto visible actualmente en el área de desplazamiento. | — | — | — |
| **CLR** | Borra el buffer de decodificación de CW. | — | — | — |
| **✕ (close CW)** | Oculta el panel de decodificación de CW. | — | — | — |

## Consejos

- Colores de confianza del texto: verde = costo < 0.15 (mejor), amarillo = < 0.35, naranja = < 0.60, rojo = ≥ 0.60. Aumente **Sens** para suprimir los caracteres naranja y rojo cuando la banda esté ruidosa.
- Si conoce el tono de la estación, reduzca el rango entre **Lo** y **Hi** alrededor de ese tono y active **🔒P (Lock Pitch)** para evitar que el decodificador se desvíe hacia interferencias.
- Una vez que el decodificador siga la velocidad de forma confiable, haga clic en **🔒S (Lock Speed)** para estabilizarla frente al QSB.
- El valor de `CwDecoderSensitivity` (0–100) se guarda automáticamente cada vez que mueve el control deslizante **Sens** y persiste entre sesiones.

## Solución de problemas

- **No aparece texto a pesar de una señal CW fuerte** — Verifique que el audio del PC esté enrutado hacia AetherSDR. El aviso "(requires PC Audio)" en el panel indica que se requiere audio para la decodificación.
- **Solo aparece texto rojo o naranja** — El nivel de confianza de la señal es bajo. Reduzca el control deslizante **Sens** hacia 0 para mostrar más salida, o verifique que **Lo** y **Hi** encuadren el tono CW real indicado en la **CW stats label**.
- **La etiqueta de estadísticas permanece en blanco** — El decodificador no ha enganchado ninguna señal. Amplíe el rango **Lo**/**Hi** y asegúrese de que el slice esté sintonizado en una señal CW con un nivel de audio suficiente.

## Temas relacionados

- [Ajustar la sensibilidad del decodificador de CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador de CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
