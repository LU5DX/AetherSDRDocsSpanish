# Activar el decodificador de CW para leer Morse en la banda

El panel de decodificación de CW aparece debajo del panadapter y muestra el código Morse entrante como texto legible en tiempo real. Úselo para copiar CW en la banda sin necesidad de un programa de decodificación separado.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El audio de la PC debe estar enrutado a AetherSDR. El panel muestra el recordatorio "(requires PC Audio)" — la decodificación no funcionará sin él.
- Sintonice una señal de CW y establezca el modo a CW en el slice activo.

## Pasos

1. En la barra de título del panadapter, confirme que el slice correcto se muestra en la etiqueta de título "Slice" (por ejemplo, "Slice A").
2. Abra el panel de decodificación de CW. El panel aparece debajo del área de espectro/waterfall y está oculto por defecto — busque un botón de control o modo de CW que lo exponga para el slice activo. Una vez visible, el panel muestra la etiqueta **CW** en azul junto con la indicación **(requires PC Audio)**.
3. Observe el área de **CW decode text** en la parte inferior del panel. Cuando el decodificador rastrea la señal, los caracteres decodificados aparecen y se colorean según la confianza: verde (alta), amarillo, naranja o rojo (baja).
4. Verifique la **CW stats label** encima del área de texto. Muestra el tono y la velocidad detectados en el formato `<Hz>  <WPM>`, por ejemplo `600 Hz  20 WPM`. Confirme que estos coincidan con la señal que está escuchando antes de confiar en la decodificación.

## Qué hace cada control

| Control                    | Qué hace                                                                                                                                                                | Por defecto |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **Sens** slider            | Filtra caracteres de baja confianza. Valores más altos rechazan más decodificaciones inciertas.                                                                                             | 30      |
| **🔒P (Lock Pitch)** toggle | Bloquea el decodificador al tono detectado actualmente para que deje de buscar.                                                                                                      | Off     |
| **🔒S (Lock Speed)** toggle | Bloquea el decodificador a la velocidad detectada actualmente (WPM).                                                                                                                      | Off     |
| **Lo** slider              | Tono mínimo que el decodificador busca. Se limita a ser ≤ **Hi**.                                                                                                                 | 500 Hz  |
| **Hi** slider              | Tono máximo que el decodificador busca. Se limita a ser ≥ **Lo**.                                                                                                                 | 700 Hz  |
| **CPY ALL**                | Copia todo el búfer de texto decodificado al portapapeles.                                                                                                                     | —       |
| **CPY VIS**                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                                                                                                                 | —       |
| **CLR**                    | Borra el búfer de decodificación de CW.                                                                                                                                                | —       |
| **× (close CW)**           | Oculta el panel de decodificación de CW.                                                                                                                                  | —       |
| **CW stats label**         | Indicador que muestra el tono y la velocidad detectados. Solo lectura.                                                                                                                      | —       |
| **CW decode text**         | Pantalla de desplazamiento de solo lectura de caracteres decodificados, coloreada según la confianza. Hacer clic derecho abre un menú contextual con una opción **Clear** además de las acciones de texto estándar. | —       |

## Consejos

- Si el área de texto se llena con caracteres de baja confianza (naranja o rojo), aumente **Sens** para filtrarlos. Comience alrededor de 50 y aumente hasta que desaparezcan los caracteres de ruido.
- Estreche el rango de búsqueda de tono con **Lo** y **Hi** para que coincida con el tono de referencia de la estación que está copiando. Esto reduce disparos falsos de señales cercanas.
- Una vez que la **CW stats label** se estabilice en un tono y una velocidad estables, active **🔒P (Lock Pitch)** y **🔒S (Lock Speed)** para evitar que el decodificador se desvíe hacia otra señal.
- Use **CLR** antes de un nuevo QSO para mantener el área de texto legible. También puede hacer clic derecho en el área de **CW decode text** y elegir **Clear** del menú contextual.

## Solución de problemas

- **No aparece texto en el área de decodificación** — Verifique que el audio de la PC esté enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio. Sin él, el decodificador no recibe audio y no produce salida.
- **El texto de decodificación es principalmente rojo u naranja** — La confianza de la señal es baja. Aumente **Sens**, o estreche el rango de tono **Lo**/**Hi** para que coincida con la frecuencia de tono de referencia actual que se muestra en la **CW stats label**.
- **Tono o velocidad incorrectos mostrados en CW stats label** — No active **🔒P (Lock Pitch)** o **🔒S (Lock Speed)** hasta que la etiqueta de estadísticas se haya estabilizado en la señal objetivo.

## Relacionado

- [Ajustar la sensibilidad del decodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador de CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto de CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
- [Descripción general del panadapter](overview.md)
