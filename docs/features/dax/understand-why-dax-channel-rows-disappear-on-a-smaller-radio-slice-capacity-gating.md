# Comprenda por qué desaparecen las filas de canales DAX en una radio más pequeña (limitación por capacidad de slices)

Esta página explica por qué el applet DAX oculta ciertas filas de canales DAX cuando se conecta a radios con menos slices disponibles, para que sepa que las filas faltantes son un comportamiento esperado y no una falla.

## Antes de comenzar

- Conectado a una FLEX-8600 u otra radio compatible con SmartSDR.
- Applet DAX visible (actívelo con el botón de la bandeja `DAO` en la barra lateral derecha si está oculto).

## Pasos

No se requiere ninguna acción — esto es informativo. El applet DAX oculta automáticamente las filas de canales RX que exceden la capacidad de slices de la radio conectada. Por ejemplo:

- Una radio de 2 slices (como una FLEX-6300/6400) solo muestra las filas DAX 1–2.
- Una radio de 4 slices (como una FLEX-6600/8600) solo muestra las filas DAX 1–4.
- Una radio de 8 slices muestra todas las filas DAX 1–8.

Las filas ocultas no se destruyen; su visibilidad se alterna según el valor `maxSlices` de la radio. Esto evita controles deslizantes de ganancia muertos que de otro modo no tendrían destino.

## Qué hace cada control

| Control | Comportamiento | Configuración persistida |
| --- | --- | --- |
| Ganancia+medidor DAX 1–4 | Siempre visible. Arrastre para establecer la ganancia RX en los canales DAX 1–4. | `DaxRxGain1`–`DaxRxGain4` (predeterminado `0.5`, rango `0.0`–`1.0`) |
| Ganancia+medidor DAX 5 | Visible solo cuando la radio conectada admite al menos 5 slices. | `DaxRxGain5` (predeterminado `0.5`, rango `0.0`–`1.0`) |
| Ganancia+medidor DAX 6 | Visible solo cuando la radio conectada admite al menos 6 slices. | `DaxRxGain6` (predeterminado `0.5`, rango `0.0`–`1.0`) |
| Ganancia+medidor DAX 7 | Visible solo cuando la radio conectada admite al menos 7 slices. | `DaxRxGain7` (predeterminado `0.5`, rango `0.0`–`1.0`) |
| Ganancia+medidor DAX 8 | Visible solo en una radio con capacidad de 8 slices. | `DaxRxGain8` (predeterminado `0.5`, rango `0.0`–`1.0`) |

El interruptor DAX Enable, la ganancia+medidor TX y los indicadores de estado de asignación de slices no se ven afectados por la limitación de capacidad de slices — permanecen visibles en todas las radios.

## Consejos

- Si espera una fila DAX (p. ej., DAX 5) pero falta, verifique el límite de slices de su radio. El applet oculta filas para mantener la interfaz coherente, no por un error.
- Las configuraciones `DaxChannel_Slice{letter}` persisten las asignaciones de canales DAX por slice; no están vinculadas a la visibilidad de las filas.

## Solución de problemas

- **Falta una fila de canal DAX que espero** — La radio conectada no admite suficientes slices. Verifique la capacidad de slices del modelo de radio (p. ej., FLEX-6300 = 2 slices, FLEX-6600 = 4, FLEX-8600 = 4). Si está en una radio con capacidad de 8 slices y aún ve menos filas, vuelva a verificar la conexión de la radio.

## Relacionado

- [Descripción general de audio DAX](overview.md)
- [Habilite DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Vea qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Comprenda por qué el applet DAX solo muestra una nota en Windows (sin controlador integrado)](understand-why-the-dax-applet-shows-only-a-note-on-windows-no-built-in-driver.md)
