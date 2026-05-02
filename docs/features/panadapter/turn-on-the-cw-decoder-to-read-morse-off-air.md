# Activar el decodificador de CW para leer Morse en el aire

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW del aire sin necesidad de un programa de decodificación independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El audio del PC debe estar enrutado hacia AetherSDR. El propio panel muestra el aviso "(requires PC Audio)" — la decodificación no funcionará sin él.
- Sintonice una señal de CW y establezca el modo CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto aparece en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto de forma predeterminada — busque un control de CW o un botón de modo que lo muestre para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto al aviso **(requires PC Audio)**.
3. Observe el área **CW decode text** en la parte inferior del panel. A medida que el decodificador rastrea la señal, los caracteres decodificados aparecen en secuencia y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja).
4. Compruebe la etiqueta **CW stats label** sobre el área de texto. Muestra el tono detectado y la velocidad en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que estos valores corresponden a la señal que está escuchando antes de confiar en la decodificación.

## Qué hace cada control

| Control                     | Función                                                                                                                                                                                | Valor predeterminado |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Control deslizante **Sens** | Filtra los caracteres de baja confianza. Los valores más altos rechazan más decodificaciones inciertas.                                                                                | 30                   |
| Palanca **🔒P (Lock Pitch)** | Bloquea el decodificador en el tono detectado actual para que deje de buscarlo.                                                                                                        | Off                  |
| Palanca **🔒S (Lock Speed)** | Bloquea el decodificador en la velocidad detectada actual (WPM).                                                                                                                       | Off                  |
| Control deslizante **Lo**   | Tono mínimo en el que busca el decodificador. Limitado para ser ≤ **Hi**.                                                                                                              | 500 Hz               |
| Control deslizante **Hi**   | Tono máximo en el que busca el decodificador. Limitado para ser ≥ **Lo**.                                                                                                              | 700 Hz               |
| **CPY ALL**                 | Copia todo el buffer de texto decodificado al portapapeles.                                                                                                                            | —                    |
| **CPY VIS**                 | Copia únicamente el texto visible en ese momento en el área de desplazamiento al portapapeles.                                                                                         | —                    |
| **CLR**                     | Borra el buffer de decodificación de CW.                                                                                                                                               | —                    |
| **× (close CW)**            | Oculta el panel de decodificación de CW.                                                                                                                                               | —                    |
| Etiqueta **CW stats label** | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                                 | —                    |
| **CW decode text**          | Visualización continua de solo lectura de los caracteres decodificados, coloreados según la confianza. Al hacer clic derecho se abre un menú contextual con la opción **Clear**, además de las acciones de texto estándar. | —     |

## Consejos

- Si el área de texto se llena de caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience en torno a 50 y súbalo hasta que desaparezcan los caracteres de ruido.
- Reduzca el rango de búsqueda de tono con **Lo** y **Hi** para que coincida con el sidetone de la estación que está copiando. Esto reduce las activaciones falsas provocadas por señales cercanas.
- Una vez que la etiqueta **CW stats label** se estabilice en un tono y velocidad constantes, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador derive hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área **CW decode text** y elegir **Clear** en el menú contextual.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio del PC esté enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin él, el decodificador no recibe audio y no produce ninguna salida.
- **El texto decodificado es mayoritariamente rojo o naranja** — La confianza de la señal es baja. Aumente **Sens** o reduzca el rango de tono **Lo**/**Hi** para que coincida con la frecuencia real del sidetone que se muestra en la etiqueta **CW stats label**.
- **El tono o la velocidad mostrados en CW stats label son incorrectos** — No active **🔒P (Lock Pitch)** ni **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.

## Relacionado

- [Ajustar la sensibilidad del decodificador de CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador de CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto de CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
