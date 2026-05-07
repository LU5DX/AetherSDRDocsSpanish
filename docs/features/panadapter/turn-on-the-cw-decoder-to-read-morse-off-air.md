# Activar el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW en el aire sin un programa de decodificación aparte.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El audio de la PC debe estar enrutado hacia AetherSDR. El propio panel muestra el recordatorio "(requires PC Audio)" — la decodificación no funcionará sin esto.
- Sintonice una señal CW y configure el modo en CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto se muestra en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto por defecto — busque un control CW o un botón de modo que lo exponga para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la indicación "(requires PC Audio)".
3. Observe el área de **texto de decodificación CW** en la parte inferior del panel. A medida que el decodificador sigue la señal, los caracteres decodificados aparecen y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja).
4. Verifique la **etiqueta de estadísticas CW** sobre el área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que coincidan con la señal que está escuchando antes de confiar en la decodificación.

## Función de cada control

| Control                    | Qué hace                                                                                                                                                                   | Valor predet. |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| Control deslizante **Sens** | Filtra caracteres de baja confianza. Los valores más altos rechazan más decodificaciones inciertas.                                                                         | 30            |
| Alternar **🔒P (Lock Pitch)** | Bloquea el decodificador al tono detectado actual para que deje de buscar.                                                                                                | Apagado       |
| Alternar **🔒S (Lock Speed)** | Bloquea el decodificador a la velocidad detectada actual (WPM).                                                                                                           | Apagado       |
| Control deslizante **Lo**   | Tono mínimo que busca el decodificador. Limitado a ser ≤ **Hi**.                                                                                                           | 500 Hz        |
| Control deslizante **Hi**   | Tono máximo que busca el decodificador. Limitado a ser ≥ **Lo**.                                                                                                           | 700 Hz        |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles.                                                                                                                | —             |
| **CPY VIS**                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                                                                                      | —             |
| **CLR**                    | Limpia el búfer de decodificación CW.                                                                                                                                      | —             |
| **× (cerrar CW)**          | Oculta el panel de decodificación CW.                                                                                                                                      | —             |
| **Etiqueta de estadísticas CW** | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                   | —             |
| **Texto de decodificación CW** | Visualización rodante de solo lectura de caracteres decodificados, coloreados por confianza. El clic derecho abre un menú contextual con una opción **Clear** además de las acciones de texto estándar. | —             |

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojos), aumente **Sens** para filtrarlos. Comience alrededor de 50 y súbalo hasta que desaparezcan los caracteres de ruido.
- Reduzca el rango de búsqueda de tono con **Lo** y **Hi** para que coincida con el tono de la estación que está copiando. Esto reduce las falsas activaciones de señales cercanas.
- Una vez que la **etiqueta de estadísticas CW** se estabilice en un tono y velocidad estables, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área de **texto de decodificación CW** y elegir **Clear** en el menú contextual.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin esto, el decodificador no recibe audio y no produce salida.
- **El texto decodificado es mayormente rojo o naranja** — La confianza de la señal es baja. Aumente **Sens**, o reduzca el rango de tono **Lo**/**Hi** para que coincida con la frecuencia de tono real mostrada en la **etiqueta de estadísticas CW**.
- **Tono o velocidad incorrectos en la etiqueta de estadísticas CW** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.

## Relacionados

- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
- [Panadapter overview](overview.md)
