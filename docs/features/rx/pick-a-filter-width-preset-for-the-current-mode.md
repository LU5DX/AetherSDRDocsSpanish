# Seleccione un ancho de filtro predefinido para el modo actual

Use los botones de ancho de filtro predefinido en el applet Controles RX para aplicar rápidamente un ancho de banda de paso estándar para el modo activo. Los valores predefinidos se guardan por modo en `FilterPresets`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles RX requiere una conexión de radio activa.
- Seleccione el segmento que desea ajustar usando las pestañas de segmento (A..H) si hay más de un segmento activo.
- Configure primero el modo del segmento. Los valores predefinidos difieren según el modo y no se muestran valores predefinidos para los modos FM, NFM o DFM.

## Pasos

1. Abra el applet Controles RX. Si no está visible, haga clic en el botón de la bandeja RX en la barra lateral derecha.
2. Si la fila de pestañas de segmento está visible, haga clic en la pestaña (A a la H) para el segmento que desea ajustar.
3. Confirme que el modo mostrado en el combo Modo sea el correcto. Los valores predefinidos de filtro cambian cuando cambia el modo.
4. Haga clic en cualquiera de los botones de ancho de filtro predefinido para aplicar ese ancho de banda inmediatamente. El ancho de filtro actual mostrado en la etiqueta de ancho de filtro (por ejemplo, `2.7K`) se actualiza para reflejar el valor predefinido aplicado.
5. Para guardar el ancho de banda de paso del filtro actual como valor predefinido, haga clic derecho en cualquier botón de ancho de filtro predefinido y elija guardar el ancho actual. El valor se almacena en `FilterPresets`.

## Función de cada control

| Control                | Comportamiento                                                                                                                                                                                                                                                                    | Valores predefinidos por defecto por modo                                                                                                                                                                                                                                                                                                                |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Valores predefinidos de ancho de filtro | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como valor predefinido.                                                                                                                                                     | Botones ocultos para modos FM/NFM/DFM; los valores predefinidos son por modo. El indicador de ancho (compartido con VfoWidget mediante `RxApplet::formatFilterWidth`) usa lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método `stepFilterWidth(direction)` recorre la lista de valores predefinidos por modo para ampliar/reducir según el modo (#2208). |
| Etiqueta de ancho de filtro | Indicador de solo lectura que muestra el ancho de banda del filtro actual (por ejemplo, `2.7K`, `500`, `6.0K`). Se actualiza cuando se aplica un valor predefinido o cuando se arrastran los bordes de la banda de paso.                                                          | —                                                                                                                                                                                                                                                                                                                                                        |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. Use valores predefinidos para anchos estándar.                                                                                                                                             | —                                                                                                                                                                                                                                                                                                                                                        |
| Modo                   | Anchos predefinidos (Hz)                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                          |
| ---                    | ---                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                          |
| USB, LSB               | 1800, 2100, 2400, 2700, 2900, 3300                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                          |
| AM, SAM                | 5600, 6000, 8000, 10000, 12000, 14000                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                          |
| CW                     | 50, 100, 250, 400                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                          |
| DIGU, DIGL, NT         | 100, 300, 600, 1000, 1500, 2000                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                          |
| RTTY                   | 250, 300, 350, 400, 500, 1000                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                          |
| FM, NFM, DFM           | Sin valores predefinidos (botones ocultos)                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                          |

## Reducción y ampliación de la banda de paso del filtro mediante pasos

El método `stepFilterWidth(direction)` permite recorrer la lista de valores predefinidos por modo desde cualquier acceso directo de la aplicación o enlace de tecla. Pase `+1` para ampliar la banda de paso al siguiente valor predefinido más grande, o `-1` para reducirla al siguiente valor predefinido más pequeño. Debido a que `stepFilterWidth` se enruta a través de `applyFilterPreset`, todos los modos (incluyendo LSB, CWL, DIGL, RTTY, AM y CW) usan la geometría de borde correcta para ese modo en lugar de una suposición simétrica.

Internamente, el método encuentra el valor predefinido cuyo ancho está más cerca de la banda de paso del segmento actual, luego pasa a la siguiente o anterior entrada en la lista (limitada a límites válidos). Si el ancho actual ya es igual al valor predefinido más cercano y el paso excedería la lista, la operación se ignora.

## Formato de almacenamiento de valores predefinidos de filtro (v0.9.5.1)

A partir de la v0.9.5.1, los valores predefinidos de filtro almacenados en `FilterPresets` pueden representar un ancho de banda simple o una banda de paso completamente especificada con desplazamientos explícitos de borde inferior y superior. Ambos formatos son aceptados al cargar valores predefinidos guardados.

- **Formato solo de ancho** — Un número entero único que representa el ancho de banda en Hz (por ejemplo, `2700`). Al aplicarse, la radio posiciona la banda de paso simétricamente alrededor de la portadora según las reglas de desplazamiento predeterminadas del modo.
- **Formato Lo:Hi** — Dos números enteros separados por dos puntos que representan los desplazamientos de borde inferior y superior de la banda de paso en Hz (por ejemplo, `300:3000`). El ancho se deriva como `hi − lo`. El valor `hi` debe ser mayor que el valor `lo` o la entrada se ignora.

Las entradas en cualquier formato pueden aparecer en la misma lista de valores predefinidos guardados para un modo dado. La lista está separada por comas. Se cargan hasta seis entradas para el applet Controles RX (coincidiendo con el número máximo de botones de valor predefinido mostrados).

Si una lista de valores predefinidos guardados se modifica externamente o una reconexión hace que la radio informe un número diferente de segmentos, los botones de valor predefinido se reconstruyen automáticamente para reflejar los valores almacenados.

## Visibilidad del botón de reducción de ruido (NR) y filtro DSP

La siguiente tabla resume qué botones de reducción de ruido y filtro DSP son visibles según la serie de la radio y el modo.

| Botón | Serie 6000 | Serie 8000 (DSP extendido) | Oculto cuando |
|--------|-------------|---------------------------|-------------|
| NR     | Sí          | Sí                        | Modo FM     |
| NR2    | Sí          | Sí                        | Modo FM     |
| NB     | Sí          | Sí                        | Modo FM     |
| NRL    | Sí          | Sí                        | Modo FM     |
| NRS    | No          | Sí                        | Modo FM     |
| RNN    | No          | Sí                        | Modo CW o FM |
| NRF    | No          | Sí                        | Modo FM     |

Antes de la V0.9.4, el botón NRL solo se mostraba en radios de la serie 8000 (DSP extendido). A partir de la V0.9.4, NRL también está disponible en radios de la serie 6000. NRS, RNN y NRF siguen siendo exclusivos de la serie 8000.

## Colores de pestaña de segmento e insignia (v0.9.3)

A partir de la v0.9.3, los botones de pestaña de segmento y la insignia de segmento usan colores por segmento administrados por el singleton `SliceColorManager` en lugar de una tabla de colores fija. El borde activo, el resaltado de fondo en los botones de pestaña y el fondo de la insignia reflejan el color asignado a ese segmento. Los colores persisten entre sesiones y también se reflejan en los widgets de VFO y las barras de medidor. No se requiere ninguna acción; los colores se actualizan automáticamente cuando se conecta un segmento.

## Comportamiento de la pestaña de segmento al reconectar (v0.9.5.1)

Cuando AetherSDR se desconecta de la radio y se reconecta, o cuando cambia el número de segmentos disponibles, la fila de pestañas de segmento se reconstruye correctamente. Específicamente:

- Si el número de segmentos informado por la radio difiere del número de botones de pestaña mostrados actualmente, `clearSliceButtons()` elimina todos los botones de pestaña existentes y la fila se reconstruye desde cero.
- Mientras la fila de pestañas está eliminada, se restaura la insignia de segmento estática para que el applet continúe mostrando qué segmento está vinculado.
- Las conexiones de señal desde los botones de pestaña al manejador de activación de segmento se establecen solo una vez por instancia del applet, evitando la acumulación de manejadores duplicados a través de reconexiones.

No se requiere ninguna acción del usuario. Si el recuento de segmentos cambia (por ejemplo, después de un ciclo de desconexión y reconexión), la fila de pestañas se actualiza automáticamente.

## Consejos

- Si necesita un ancho que no coincida con ningún valor predefinido, arrastre los bordes del widget de banda de paso del filtro para establecer un valor arbitrario, luego haga clic derecho en un botón de valor predefinido para guardar ese ancho para uso futuro.
- Al guardar un valor predefinido haciendo clic derecho en un botón de valor predefinido, la banda de paso se almacena en formato lo:hi si los bordes de la banda de paso actual se han establecido explícitamente, o en formato solo de ancho en caso contrario. Ambos formatos se cargan correctamente en todas las sesiones posteriores.
- Los valores predefinidos son por modo. Cambiar de modo remodela el filtro y muestra los botones de valor predefinido para el nuevo modo.
- El modo NT usa los mismos valores predefinidos de filtro y comportamiento de silenciador que DIGU y DIGL. El silenciador está deshabilitado en modo NT y el estado de silenciador desactivado se envía a la radio automáticamente si el silenciador estaba previamente habilitado.
- Use el método `stepFilterWidth` desde enlaces de teclas o scripts de macros para ampliar y reducir la banda de paso del filtro sin hacer clic directamente en los botones de valor predefinido. El método siempre se posiciona en un valor predefinido apropiado para el modo.

## Solución de problemas

- **Los botones de valor predefinido no son visibles** — El modo activo es FM, NFM o DFM. Estos modos no exponen valores predefinidos de filtro. Cambie el modo usando el combo Modo a un modo que admita valores predefinidos (por ejemplo, USB o CW).
- **Hacer clic derecho en un botón de valor predefinido no hace nada visible** — Confirme que el segmento esté conectado a la radio. El applet RX requiere una conexión de radio activa para guardar valores predefinidos.
- **El botón NRL no es visible en una radio de la serie 6000** — Confirme que está ejecutando V0.9.4 o posterior. Las versiones anteriores restringían NRL solo a radios de la serie 8000.
- **Los controles de silenciador están atenuados** — El modo activo es DIGU, DIGL, NT, CW o CWL. El silenciador está deshabilitado en estos modos. En modos digitales (incluyendo NT) el silenciador se desactiva automáticamente; en modos CW la radio gestiona el estado del silenciador directamente.
- **La fila de pestañas de segmento aparece en blanco después de reconectar** — Esto podría ocurrir en versiones anteriores a la v0.9.5.1. Actualice a v0.9.5.1 o posterior. La fila de pestañas ahora se reconstruye automáticamente cuando el número de segmentos cambia al reconectar.

## Relacionado

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Descripción general de Controles RX](overview.md)
- [Cambiar entre múltiples segmentos usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
<!-- docmesh:llm version=v0.9.8 date=2026-05-01 -->
