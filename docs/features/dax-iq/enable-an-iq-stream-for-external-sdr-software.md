# Habilitar un flujo IQ para software SDR externo

El applet DAX IQ le permite activar uno o más de los cuatro flujos IQ en su FLEX-8600 para que el software SDR externo pueda recibir datos IQ en bruto desde la radio. Cada flujo puede habilitarse de forma independiente con su propia tasa de muestreo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los flujos IQ no están disponibles sin una conexión activa a la radio.
- El applet DAX IQ está oculto de forma predeterminada. Debe abrirlo antes de poder habilitar un flujo.

## Pasos

1. Haga clic en el botón de la bandeja **IQ** en la barra lateral derecha para mostrar el applet DAX IQ.
2. En la fila del canal que desee (IQ 1 a IQ 4), seleccione una tasa de muestreo en el cuadro combinado de tasa. El valor predeterminado es **48k**. Las tasas disponibles son **24k**, **48k**, **96k** y **192k**.
3. Haga clic en el botón **Off** en la fila de ese canal. La etiqueta del botón cambia a **On** y el estilo del botón cambia para indicar que el flujo está activo.
4. Configure su software SDR externo para conectarse al canal DAX IQ correspondiente.

## Función de cada control

| Control | Predeterminado | Valores válidos | Clave persistida |
|---|---|---|---|
| Cuadro combinado de tasa (IQ 1–4) | `48k` | `24k` (24000), `48k` (48000), `96k` (96000), `192k` (192000) | Ninguna |
| Conmutador Off/On (IQ 1–4) | `Off` | `Off`, `On` | `DaxIqEnabled1` – `DaxIqEnabled4` |
| Medidor de nivel (IQ 1–4) | 0 | 0–100 (escalado desde RMS × 200) | — |

## Consejos

- Su estado de habilitación se conserva entre sesiones. Cuando se reconecte a la radio, AetherSDR espera brevemente a que la sesión se estabilice antes de volver a habilitar cualquier flujo que estuviera activo en la sesión anterior.
- El cuadro combinado de tasa se sincroniza con la tasa informada por la radio solo cuando un flujo está activo y no se encuentra en un estado de estabilización de tasa. Si selecciona una tasa mientras el flujo está desactivado y luego lo habilita, su selección se aplica al flujo recién creado en lugar de perderse debido al valor predeterminado de 48k de la radio.
- Al habilitar un flujo con una tasa no predeterminada, la radio informa brevemente 48k mientras se estabiliza. El cuadro combinado evita sincronizarse con ese valor transitorio, preservando su selección prevista.
- El medidor de nivel se restablece a 0 cada vez que se deshabilita un flujo, el flujo no está vinculado a un pan (el ID de pan está vacío o es `0x0`), o la radio se desconecta.

## Solución de problemas

- **El botón de la bandeja IQ no es visible** — El panel del applet puede estar oculto. Vaya a `View > Applet Panel` para mostrarlo, luego haga clic en el botón de la bandeja **IQ**.
- **El botón cambia a On pero no llegan datos al software externo** — Es posible que la solicitud de flujo se haya enviado antes de que la radio estuviera lista. Deshabilite el flujo haciendo clic en **On** para volver a **Off**, espere un momento, luego haga clic en **Off** nuevamente para volver a habilitarlo.
- **El cuadro combinado de tasa vuelve al valor anterior después de habilitar** — Si el flujo aún está en un estado de estabilización de tasa, el cuadro combinado espera la tasa final. En casos raros donde la radio anula su selección después de la estabilización, el cuadro se sincronizará con el valor de la radio.
- **Los flujos no se restauran después de reconectar** — Esto puede ocurrir si el applet se carga después de que la conexión a la radio ya está completa. AetherSDR ahora verifica si hay una radio ya conectada al iniciar y restaura los flujos persistidos de inmediato.

## Relacionados

- [Resumen de DAX IQ](overview.md)
- [Seleccionar la tasa de muestreo IQ (24k/48k/96k/192k)](pick-the-iq-sample-rate-24k-48k-96k-192k.md)
- [Monitorear el nivel RMS de cada flujo IQ](monitor-the-rms-level-of-each-iq-stream.md)
- [Deshabilitar un flujo IQ para liberar ancho de banda](disable-an-iq-stream-to-free-bandwidth.md)
