# Habilitar un flujo IQ para software SDR externo

El applet DAX IQ le permite activar uno o más de los cuatro flujos IQ en su FLEX-8600 para que un software SDR externo pueda recibir datos IQ en bruto desde la radio. Cada flujo puede habilitarse de forma independiente con su propia frecuencia de muestreo.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los flujos IQ no están disponibles sin una conexión activa a la radio.
- El applet DAX IQ está oculto por defecto. Debe abrirlo antes de poder habilitar un flujo.

## Pasos

1. Haga clic en el botón de bandeja **IQ** en la barra lateral derecha para mostrar el applet DAX IQ.
2. En la fila del canal que desee (IQ 1 a IQ 4), seleccione una frecuencia de muestreo en el cuadro combinado de tasa. El valor predeterminado es **48k**. Las tasas disponibles son **24k**, **48k**, **96k** y **192k**.
3. Haga clic en el botón **Off** en la fila de ese canal. La etiqueta del botón cambia a **On** y el estilo del botón cambia para indicar que el flujo está activo.
4. Configure su software SDR externo para que se conecte al canal DAX IQ correspondiente.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | `48k` | `24k` (24000), `48k` (48000), `96k` (96000), `192k` (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Alternador Off/On (IQ 1–4) | `Off` | `Off`, `On` | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor de nivel (IQ 1–4) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- Su selección de frecuencia de muestreo se conserva entre sesiones. Cuando se reconecte a la radio, AetherSDR espera brevemente a que la sesión se estabilice antes de re-habilitar cualquier flujo que estuviera activo en la sesión anterior.
- El cuadro combinado de tasa se sincroniza con la tasa reportada por la radio una vez que un flujo está activo. Si la radio invalida su selección, el cuadro combinado reflejará el valor de la radio.
- El medidor de nivel se restablece a 0 cada vez que se deshabilita un flujo o la radio se desconecta.

## Solución de problemas

- **El botón de bandeja IQ no es visible** — El panel del applet puede estar oculto. Vaya a `View > Applet Panel` para mostrarlo, luego haga clic en el botón de bandeja **IQ**.
- **El botón cambia a On pero no llegan datos al software externo** — La solicitud de flujo puede haberse enviado antes de que la radio estuviera lista. Deshabilite el flujo haciendo clic en **On** para devolverlo a **Off**, espere un momento, luego haga clic en **Off** nuevamente para re-habilitarlo.
- **El cuadro combinado de tasa se revierte después de habilitar** — La radio ha reportado una frecuencia de muestreo diferente para el flujo activo. El cuadro combinado se sincroniza con el valor reportado por la radio; seleccione su tasa preferida antes de habilitar el flujo.

## Relacionados

- [DAX IQ overview](overview.md)
- [Pick the IQ sample rate (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitor the RMS level of each IQ stream](monitor-the-rms-level-of-each-iq-stream.md)
- [Disable an IQ stream to free bandwidth](disable-an-iq-stream-to-free-bandwidth.md)
