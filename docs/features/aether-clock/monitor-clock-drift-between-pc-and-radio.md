# Monitorizar la deriva del reloj entre el PC y la radio

El applet AetherClock muestra la deriva del reloj medida entre su PC y la base de tiempo disciplinada por GPS de la radio, permitiéndole supervisar la precisión de temporización para el sellado de tiempo exacto por muestra y el diagnóstico.

## Antes de comenzar

- Asegúrese de que AetherSDR está conectado a una radio FLEX-8600
- La radio debe tener capacidad GPS/GNSS para la monitorización de la deriva

## Pasos

1. Abra la bandeja del Panel de Applets.
2. Haga clic en el mosaico **AetherClock** (etiquetado "CLK").
3. Lea el indicador **Clock drift** para ver la deriva medida en nanosegundos.
4. Si la deriva es alta o inconsistente, verifique el **GNSS lock indicator** — la monitorización de la deriva solo es válida cuando el receptor GPS de la radio tiene bloqueo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| GNSS lock indicator | Indicador | Muestra el estado de bloqueo GPS/GNSS de la radio: **Locked**, **Unlocked** o **Acquiring**. Los datos de deriva solo son significativos cuando está bloqueado. |
| Clock drift | Indicador | Deriva medida entre el reloj GPS de la radio y el reloj local del PC, mostrada en nanosegundos. |
| Align Clock | Botón pulsador | Alinea el reloj local del PC con la referencia disciplinada por GPS de la radio para una temporización exacta por muestra. |

## Solución de problemas

- **La lectura de deriva del reloj es errática o muestra valores extremos** — Es posible que la radio no tenga bloqueo GPS/GNSS. Verifique el GNSS lock indicator; si muestra **Unlocked** o **Acquiring**, espere a obtener bloqueo antes de confiar en la lectura de deriva.
- **No se ve ninguna lectura de deriva** — Verifique que la radio esté conectada y tenga capacidad GPS. El applet AetherClock requiere una conexión activa con la radio.

## Relacionado

- [AetherClock overview](overview.md)
- [Align the local clock to the radio's GPS timebase](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Check the radio's GPS/GNSS lock status](check-the-radio-s-gps-gnss-lock-status.md)
