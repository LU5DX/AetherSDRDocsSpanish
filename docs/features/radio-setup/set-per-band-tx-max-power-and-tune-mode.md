# Configurar la potencia TX máxima por banda y el modo de ajuste

Use esta página para limitar la potencia de transmisión y seleccionar el modo de ajuste para cada banda de radioaficionado en su radio Flex. Estas configuraciones permiten proteger amplificadores, antenas o hardware específico de banda contra condiciones de exceso de potencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña TX (tab) y el diálogo TX Band Settings solo están disponibles con una conexión de radio activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Para establecer un límite de potencia a nivel de radio que se aplique a todas las bandas, ajuste **Max Power:** (0–100 %).
4. Para seleccionar el comportamiento del botón de ajuste, elija una opción en el menú desplegable **Tune Mode:**.
5. Para configurar la potencia y el modo de ajuste por banda, haga clic en **TX Band Settings**. Esto abre el diálogo dedicado de potencia y ajuste por banda.
6. En el diálogo TX Band Settings, localice la fila de la banda que desea modificar y establezca los valores de potencia y ajuste para esa banda.
7. Cierre el diálogo TX Band Settings al terminar y, a continuación, cierre Radio Setup.

Alternativamente, abra el diálogo por banda directamente mediante `Settings > TX Band Settings...`.

## Qué hace cada control

| Control | Tipo | Rango válido | Comportamiento |
|---|---|---|---|
| **Max Power:** | Spinbox | 0–100 % | Establece un límite de potencia TX a nivel de radio aplicado a todas las bandas. |
| **Tune Mode:** | Combo box | Opciones definidas por el firmware del radio | Selecciona el comportamiento del botón de ajuste al activarse. |
| **TX Band Settings** | Botón | — | Abre el diálogo de potencia y ajuste por banda. |
| **Show TX in Waterfall:** | Interruptor | — | Dibuja la señal TX en la pantalla de cascada (waterfall). |
| **TX Follows Active Slice / Active Slice Follows TX** | Botón | Mutuamente excluyentes | Controla si la TX sigue al slice activo o el slice activo sigue a la TX. |

## Consejos

- **Max Power:** en la pestaña TX es un límite global. Los límites por banda establecidos en TX Band Settings operan dentro de ese límite.
- Puede acceder a TX Band Settings sin abrir Radio Setup usando `Settings > TX Band Settings...` directamente desde el menú.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Verificar el número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
