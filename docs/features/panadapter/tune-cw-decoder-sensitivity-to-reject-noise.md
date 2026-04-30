# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El regulador **Sens** controla cuán estrictamente el decodificador CW filtra descodificaciones de caracteres inciertas. Aumentarla suprime la salida distorsionada causada por ruido o señales débiles; reducirla muestra más caracteres al costo de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no es visible, ábralo primero.
- El audio de PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Encuentre la etiqueta **Sens:** y el regulador horizontal corto inmediatamente a su derecha.
3. Arrastre el regulador **Sens** hacia la izquierda para aceptar más descodificaciones (umbral más bajo) o hacia la derecha para rechazar descodificaciones de baja confianza (umbral más alto).
4. Observe el área "CW decode text". Los caracteres coloreados en rojo o naranja indican baja confianza; redúzcalos moviendo el regulador hacia la derecha.
5. Suelte el regulador. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control         | Predeterminado | Rango                |
|-----------------|----------------|----------------------|
| Regulador **Sens** | 30      | 0–100                |
| CW decode text  | —       | —                    |
| CW stats label  | —       | `<hz> Hz  <wpm> WPM` |

## Consejos

- Comience con el valor predeterminado de 30 y aumente el regulador gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto descodificado.
- El color del carácter es un indicador rápido de confianza: si la mayoría de la salida es verde, la sensibilidad actual está bien adaptada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el regulador está configurado demasiado alto — muévalo hacia la izquierda hasta que reaparezcan los caracteres.
- Los reguladores de tono **Lo** y **Hi** (predeterminado 500 Hz y 700 Hz, rango 300–1200 Hz) restringen qué tonos busca el decodificador. Estrechar ese rango para que coincida con el tono lateral de la señal recibida puede reducir activaciones falsas independientemente de **Sens**.
- Hacer clic derecho en el área de texto CW decode también da acceso a las acciones de texto estándar (Select All, Copy, etc.) junto con la opción **Clear**.

## Solución de problemas

- **El texto descodificado desaparece completamente después de aumentar Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el regulador hasta que reaparezca la salida, luego aumente más lentamente.
- **La salida sigue siendo ruidosa incluso en Sens 100** — la señal puede estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta CW stats para el tono informado y ajuste **Lo** e **Hi** para abarcarlo.
- **Sens se reinicia a 30 después de reiniciar** — si `CwDecoderSensitivity` falta de la configuración guardada, AetherSDR utiliza el valor predeterminado de 30. Mueva el regulador una vez para escribir el valor; luego se guarda en cada cambio.

## Relacionado

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
