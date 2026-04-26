# Descripción general de Phone

El applet Phone proporciona controles para la transmisión de voz en el FLEX-8600: nivel de portadora AM, transmisión activada por voz (VOX), puerta de ruido expansora descendente (DEXP) y frecuencias de corte del filtro de audio TX. Ábralo cuando necesite ajustar cómo AetherSDR procesa el audio transmitido.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet Phone siempre está presente en el Applet Panel (barra lateral derecha). Alterne su visibilidad con el botón de bandeja `PHNE` en la barra lateral derecha.

El applet está organizado en cuatro áreas funcionales:

**AM Carrier** establece el nivel de potencia de la portadora utilizada durante la transmisión AM. El valor actual se muestra como un número a la derecha del control deslizante.

**VOX** habilita la transmisión activada por voz. Cuando VOX está activo, el audio que supera el umbral del nivel VOX activa el transmisor. El control deslizante de nivel VOX establece ese umbral, y el control deslizante Delay controla el tiempo que el radio permanece en transmisión después de que el audio cae por debajo del umbral (tiempo de retención).

**DEXP** es un expansor descendente que actúa como puerta de ruido sobre el audio transmitido. El control deslizante de umbral DEXP establece el umbral de la puerta. Tanto `DEXP` como `DEXP threshold` conservan sus valores localmente en la configuración de AetherSDR. **Nota:** Debido a una limitación del firmware en v1.4.0.0, los controles DEXP no son funcionales: el radio devuelve un error cuando se envían estos comandos. Los controles están presentes en la interfaz, pero no tienen ningún efecto sobre el radio hasta que esto se resuelva.

**TX filter** establece los bordes de corte inferior y superior de la banda de paso del audio transmitido. Use los botones `<` y `>` a cada lado del valor de frecuencia mostrado, o desplace la rueda del ratón sobre el valor, para ajustar cada borde en incrementos de 50 Hz.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|---|
| AM Carrier | Deslizante | — | 0–100 | — |
| VOX | Botón de alternancia | — | On / Off | — |
| VOX level | Deslizante | — | 0–100 | — |
| Delay | Deslizante | — | 0–100 | — |
| DEXP | Botón de alternancia | — | On / Off | `DexpEnabled` |
| DEXP threshold | Deslizante | 0 | 0–100 | `DexpLevel` |
| Low Cut `<` / `>` | Spinbox | 50 Hz | 0 Hz a (corte superior − 50 Hz), paso 50 Hz | — |
| High Cut `<` / `>` | Spinbox | 3300 Hz | (corte inferior + 50 Hz) a 10000 Hz, paso 50 Hz | — |

## Consejos

- Los valores `DexpEnabled` y `DexpLevel` se guardan en la configuración local de AetherSDR aunque el radio rechace los comandos DEXP en el firmware v1.4.0.0. Su configuración se conservará para cuando se agregue compatibilidad en el firmware.
- El control deslizante Delay controla únicamente el tiempo de retención de VOX; no tiene efecto a menos que VOX esté habilitado.
- Low Cut y High Cut están vinculados: Low Cut no puede establecerse por encima de (High Cut − 50 Hz), y High Cut no puede establecerse por debajo de (Low Cut + 50 Hz).

## Solución de problemas

- **El botón de alternancia DEXP o el umbral no tienen efecto audible** — El firmware del radio v1.4.0.0 no admite el comando de protocolo DEXP y devuelve un error. Los controles son visibles pero no funcionales. No existe solución alternativa en esta versión del firmware.

## Relacionado

- [Ajustar la potencia de portadora AM para transmisión AM](adjust-am-carrier-power-for-am-transmit.md)
- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
