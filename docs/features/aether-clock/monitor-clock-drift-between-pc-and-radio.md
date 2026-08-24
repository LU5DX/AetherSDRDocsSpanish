# Supervisar la deriva del reloj entre el PC y la radio

El applet AetherClock muestra la deriva de reloj medida entre su PC y la base de tiempo disciplinada por GPS de la radio, lo que le permite supervisar la precisión de sincronización para el sellado de tiempo con precisión de muestra y diagnósticos.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a una radio FLEX-8600
- La radio debe tener capacidad GPS/GNSS para la supervisión de la deriva

## Pasos

1. Abra la bandeja del panel de applets.
2. Haga clic en el mosaico **AetherClock** (etiquetado como "CLK").
3. Lea el indicador **Clock drift** para ver la deriva medida en nanosegundos.
4. Si la deriva es alta o inconsistente, verifique el indicador de bloqueo GNSS: la supervisión de la deriva solo es válida cuando el receptor GPS de la radio tiene bloqueo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| GNSS lock indicator | Indicador | Muestra el estado de bloqueo GPS/GNSS de la radio: **Locked**, **Unlocked** o **Acquiring**. Los datos de deriva solo son significativos cuando hay bloqueo. |
| Clock drift | Indicador | Deriva medida entre el reloj GPS de la radio y el reloj local del PC, mostrada en nanosegundos. |
| Align Clock | Botón pulsador | Alinea el reloj local del PC con la referencia disciplinada por GPS de la radio para una sincronización con precisión de muestra. |

## Solución de problemas

- **La lectura de deriva de reloj es errática o muestra valores extremos** — Es posible que la radio no tenga bloqueo GPS/GNSS. Verifique el indicador de bloqueo GNSS; si muestra **Unlocked** o **Acquiring**, espere a que se establezca el bloqueo antes de confiar en la lectura de deriva.
- **No se ve ninguna lectura de deriva** — Verifique que la radio esté conectada y tenga capacidades GPS. El applet AetherClock requiere una conexión de radio activa.

## Relacionado

- [Descripción general de AetherClock](overview.md)
- [Alinear el reloj local con la base de tiempo GPS de la radio](align-the-local-clock-to-the-radio-s-gps-timebase.md)
- [Verificar el estado de bloqueo GPS/GNSS de la radio](check-the-radio-s-gps-gnss-lock-status.md)
