# Asignar acciones de pulsación y doble pulsación a la rueda

Configure lo que sucede cuando pulsa (un toque) o pulsa dos veces la rueda física del FlexControl o la rueda virtual del cuadro de diálogo AetherControl.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: **Settings > AetherControl...**
- Si usa un FlexControl físico, asegúrese de que esté conectado (consulte [Configure el controlador de hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)).

## Pasos

1. En el cuadro de diálogo AetherControl, localice el cuadro combinado **Push (action)** cerca de la visualización de la rueda.
2. Haga clic en el cuadro combinado y seleccione una acción de la lista.
3. En el cuadro combinado **Double-tap (action)** que se encuentra justo debajo, seleccione una segunda acción.
4. Cierre el cuadro de diálogo. Las nuevas acciones surten efecto de inmediato.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|---------------------|----------------------|----------------|
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción que se activa con una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción que se activa con dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |

Ambos cuadros combinados comparten la misma lista de acciones disponibles. Consulte el fragmento de código fuente para ver la lista completa de entradas `FlexActionDef`, que incluyen todas las etiquetas mostradas anteriormente.

## Relacionado

- [Configure las acciones de pulsación simple y doble para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
