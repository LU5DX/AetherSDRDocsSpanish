# Seleccionar un ajuste preestablecido de ancho de filtro para el modo actual

Use los botones de ajuste preestablecido de ancho de filtro en el applet RX Controls para aplicar rápidamente un ancho de banda de paso estándar para el modo activo. Los ajustes preestablecidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) si hay más de un slice activo.
- Configure el modo del slice primero. Los valores preestablecidos varían según el modo, y los preestablecidos no se muestran para los modos FM, NFM ni DFM.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón RX tray en la barra lateral derecha.
2. Si la fila de pestañas de slice está visible, haga clic en la pestaña (A hasta H) del slice que desea ajustar.
3. Confirme que el modo mostrado en el combo Mode es correcto. Los ajustes preestablecidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquier botón de ajuste preestablecido de ancho de filtro para aplicar ese ancho de banda de inmediato. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el preestablecido aplicado.
5. Para guardar el paso de banda de filtro actual como preestablecido, haga clic derecho en cualquier botón de ajuste preestablecido de ancho de filtro y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Qué hace cada control

| Control                        | Comportamiento                                                                                                                                                                                        | Preestablecidos predeterminados por modo |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| Preestablecidos de ancho de filtro | Haga clic para aplicar un ancho de banda preestablecido al slice actual. Haga clic derecho para guardar el ancho de filtro actual como preestablecido. Oculto en los modos FM, NFM y DFM.         | Ver tabla a continuación                 |
| Etiqueta de ancho de filtro    | Indicador de solo lectura que muestra el ancho de banda de filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un preestablecido o cuando se arrastran los bordes del paso de banda. | —                                        |
| Widget de paso de banda de filtro | Arrastre el borde inferior o superior para establecer un paso de banda personalizado. Use los preestablecidos para anchos estándar.                                                               | —                                        |
| Modo                           | Anchos preestablecidos (Hz)                                                                                                                                                                           |                                          |
| ---                            | ---                                                                                                                                                                                                   |                                          |
| USB, LSB                       | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                    |                                          |
| AM, SAM                        | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                 |                                          |
| CW                             | 50, 100, 250, 400                                                                                                                                                                                     |                                          |
| DIGU, DIGL, NT                 | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                       |                                          |
| RTTY                           | 250, 300, 350, 400, 500, 1000                                                                                                                                                                         |                                          |
| FM, NFM, DFM                   | Sin preestablecidos (botones ocultos)                                                                                                                                                                 |                                          |

## Formato de almacenamiento de preestablecidos de filtro (v0.9.5.1)

A partir de v0.9.5.1, los preestablecidos de filtro almacenados en `FilterPresets` pueden representar ya sea un ancho de banda simple o un paso de banda completamente especificado con desplazamientos explícitos de borde inferior y superior. Ambos formatos se aceptan al cargar preestablecidos guardados.

- **Formato solo ancho** — Un único entero que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarse, la radio posiciona el paso de banda simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos enteros separados por dos puntos que representan los desplazamientos de borde inferior y superior del paso de banda en Hz (por ejemplo, `300:3000`). El ancho se calcula como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo`, o la entrada se ignora.

Las entradas en cualquiera de los formatos pueden aparecer en la misma lista de preestablecidos guardados para un modo dado. La lista está separada por comas. Se cargan hasta seis entradas para el applet RX Controls (correspondiente al número máximo de botones de preestablecido mostrados).

Si una lista de preestablecidos guardados se modifica externamente, o si una reconexión hace que la radio informe un número diferente de slices, los botones de preestablecido se reconstruyen automáticamente para reflejar los valores almacenados.

## Visibilidad de los botones de reducción de ruido y filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP son visibles según la serie de radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|-------|------------|---------------------------|---------------|
| NR    | Sí         | Sí                        | Modo FM       |
| NR2   | Sí         | Sí                        | Modo FM       |
| NB    | Sí         | Sí                        | Modo FM       |
| NRL   | Sí         | Sí                        | Modo FM       |
| NRS   | No         | Sí                        | Modo FM       |
| RNN   | No         | Sí                        | Modo CW o FM  |
| NRF   | No         | Sí                        | Modo FM       |

Antes de V0.9.4, el botón NRL solo se mostraba en radios de la serie 8000 (DSP extendido). A partir de V0.9.4, NRL también está disponible en radios de la serie 6000. NRS, RNN y NRF siguen siendo exclusivos de la serie 8000.

## Colores de pestañas y distintivos de slice (v0.9.3)

A partir de v0.9.3, los botones de pestaña de slice y el distintivo de slice usan colores por slice gestionados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo del distintivo reflejan el color asignado a ese slice. Los colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidores. No se requiere ninguna acción; los colores se actualizan automáticamente cuando se conecta un slice.

## Comportamiento de la fila de pestañas de slice al reconectar (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se vuelve a conectar, o cuando cambia el número de slices disponibles, la fila de pestañas de slice se reconstruye correctamente. En concreto:

- Si el número de slices informado por la radio difiere del número de botones de pestaña actualmente mostrados, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está desmantelada, el distintivo estático de slice se restaura para que el applet continúe mostrando cuál slice está vinculado.
- Las conexiones de señal de los botones de pestaña al manejador de activación de slice se establecen solo una vez por instancia del applet, evitando que se acumulen manejadores duplicados a través de reconexiones.

No se requiere ninguna acción del usuario. Si el número de slices cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Consejos

- Si necesita un ancho que no coincida con ningún preestablecido, arrastre los bordes del widget de paso de banda de filtro para establecer un valor arbitrario; luego haga clic derecho en un botón de preestablecido para guardar ese ancho para uso futuro.
- Al guardar un preestablecido haciendo clic derecho en un botón de preestablecido, el paso de banda se almacena en formato lo:hi si los bordes del paso de banda actual se han establecido explícitamente, o en formato solo ancho en caso contrario. Ambos formatos se cargan correctamente en todas las sesiones posteriores.
- Los preestablecidos son por modo. Cambiar de modo modifica la forma del filtro y muestra los botones de preestablecido para el nuevo modo.
- El modo NT usa los mismos preestablecidos de filtro y el mismo comportamiento de squelch que DIGU y DIGL. El squelch está deshabilitado en el modo NT y se envía automáticamente a la radio la orden de squelch desactivado si el squelch estaba habilitado previamente.

## Solución de problemas

- **Los botones de preestablecido no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen preestablecidos de filtro. Cambie el modo usando el combo Mode a un modo que admita preestablecidos (por ejemplo, USB o CW).
- **El clic derecho en un botón de preestablecido no produce ningún efecto visible** — Confirme que el slice está conectado a la radio. El applet RX requiere una conexión de radio activa para guardar valores preestablecidos.
- **El botón NRL no es visible en una radio de la serie 6000** — Confirme que está ejecutando V0.9.4 o posterior. Las versiones anteriores restringían NRL únicamente a radios de la serie 8000.
- **Los controles de squelch están deshabilitados** — El modo activo es DIGU, DIGL, NT, CW o CWL. El squelch está deshabilitado en estos modos. En los modos digitales (incluido NT) el squelch se desactiva automáticamente; en los modos CW la radio gestiona el estado del squelch directamente.
- **La fila de pestañas de slice está en blanco después de reconectar** — Esto podría ocurrir en versiones anteriores a v0.9.5.1. Actualice a v0.9.5.1 o posterior. La fila de pestañas ahora se reconstruye automáticamente cuando cambia el número de slices al reconectar.

## Relacionados

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
<!-- docmesh:llm version=v0.9.5.1 date=2026-05-01 -->
