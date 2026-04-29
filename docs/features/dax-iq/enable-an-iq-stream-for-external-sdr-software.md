# Activar un flujo IQ para software SDR externo

El applet DAX IQ permite activar uno o más de los cuatro flujos IQ de su FLEX-8600 para que el software SDR externo pueda recibir datos IQ sin procesar desde el radio. Cada flujo puede habilitarse de forma independiente con su propia tasa de muestreo.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Los flujos IQ no están disponibles sin una conexión de radio activa.
- El applet DAX IQ está oculto de forma predeterminada. Debe abrirlo antes de poder habilitar un flujo.

## Pasos

1. Haga clic en el botón de bandeja **IQ** de la barra lateral derecha para mostrar el applet DAX IQ.
2. En la fila del canal que desee (IQ 1 a IQ 4), seleccione una tasa de muestreo en el cuadro combinado de tasa. El valor predeterminado es **48k**. Las tasas disponibles son **24k**, **48k**, **96k** y **192k**.
3. Haga clic en el botón **Off** de la fila de ese canal. La etiqueta del botón cambia a **On** y el estilo del botón cambia para indicar que el flujo está activo.
4. Configure su software SDR externo para conectarse al canal DAX IQ correspondiente.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | `48k` | `24k` (24000), `48k` (48000), `96k` (96000), `192k` (192000) | `DaxIqRate1` – `DaxIqRate4` |
| Alternador Off/On (IQ 1–4) | `Off` | `Off`, `On` | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor de nivel (IQ 1–4) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- La selección de la tasa de muestreo se conserva entre sesiones. Al reconectarse al radio, AetherSDR espera brevemente a que la sesión se estabilice antes de volver a habilitar los flujos que estaban activos en la sesión anterior.
- El cuadro combinado de tasa se sincroniza con la tasa reportada por el radio una vez que un flujo está activo. Si el radio anula su selección, el cuadro combinado reflejará el valor del radio.
- El medidor de nivel se restablece a 0 cada vez que se deshabilita un flujo o el radio se desconecta.

## Solución de problemas

- **El botón de bandeja IQ no es visible** — El panel del applet puede estar oculto. Vaya a `View > Applet Panel` para mostrarlo y, a continuación, haga clic en el botón de bandeja **IQ**.
- **El botón cambia a On pero no llegan datos al software externo** — Es posible que la solicitud del flujo se haya enviado antes de que el radio estuviera listo. Deshabilite el flujo haciendo clic en **On** para devolverlo a **Off**, espere un momento y, luego, haga clic en **Off** de nuevo para volver a habilitarlo.
- **El cuadro combinado de tasa revierte tras la habilitación** — El radio ha reportado una tasa de muestreo diferente para el flujo activo. El cuadro combinado se sincroniza con el valor reportado por el radio; seleccione la tasa preferida antes de habilitar el flujo.

## Temas relacionados

- [Descripción general de DAX IQ](overview.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Supervisar el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
