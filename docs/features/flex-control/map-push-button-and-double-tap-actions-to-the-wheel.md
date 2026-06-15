# Asignar acciones de pulsación y doble pulsación a la rueda

Configure las acciones que se ejecutan al pulsar (un solo toque) o hacer doble pulsación en la rueda física del FlexControl o en la rueda virtual del cuadro de diálogo AetherControl.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: **Settings > AetherControl...**
- Si utiliza un FlexControl físico, asegúrese de que esté conectado (consulte [Configure el controlador de hardware AetherControl / FlexControl](#configure-the-aethercontrol-flexcontrol-hardware-controller)).

## Pasos

1. En el cuadro de diálogo AetherControl, localice el cuadro combinado **Push (action)** cerca de la visualización de la rueda.
2. Haga clic en el cuadro combinado y seleccione una acción de la lista.
3. En el cuadro combinado **Double-tap (action)**, situado justo debajo, seleccione una segunda acción.
4. Cierre el cuadro de diálogo. Las nuevas acciones se aplican de inmediato.

## Función de cada control

| Control | Predeterminado | Clave de configuración | Comportamiento |
|---------|---------|-------------|----------|
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción que se activa con una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción que se activa con dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |

Ambos cuadros combinados comparten la misma lista de acciones disponibles. Consulte el fragmento de código fuente para obtener la lista completa de entradas `FlexActionDef`, que incluye todas las etiquetas mostradas anteriormente.

## Relacionado

- [Configure las acciones de pulsación y doble pulsación para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)

# Configurar el controlador de hardware AetherControl / FlexControl

Configure la rueda virtual de AetherControl y administre un dispositivo FlexControl físico.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: **Settings > AetherControl...**

## Pasos

1. En el cuadro de diálogo AetherControl, el indicador **Wheel** muestra la rueda de sintonización virtual. Haga doble clic en él para capturar la entrada del ratón para la sintonización circular. Vuelva a hacer doble clic para liberarla. Presione Escape como ruta de liberación secundaria.
2. El indicador **Physical** muestra el estado de conexión de un FlexControl físico. Haga clic en **Detect** para encontrar el dispositivo, o en **Close** para desconectarlo.
3. Use el botón de alternancia **Compact** para cambiar a una interfaz de usuario mínima que muestre solo la rueda y la lectura de frecuencia.
4. Active **External Spin** para permitir que arrastrar en el panadapter active gestos de sintonización con la rueda giratoria.
5. Active **Reverse** para invertir la dirección de sintonización de la rueda.
6. Ajuste **Wheel Tightness** con el control deslizante para controlar el arrastre de desaceleración de la rueda virtual. 0 = ajustado (parada rápida), 100 = suelto (desaceleración larga). Afecta principalmente al comportamiento del trackpad.
7. Ajuste **Mouse Sensitivity** con el control deslizante para controlar cuánto movimiento capturado del ratón/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Afecta principalmente al comportamiento del trackpad.
8. Configure los **Aux buttons (1-5)** haciendo clic en un botón para seleccionarlo y luego:
   - Seleccione una acción de un solo toque del **Aux single-tap combo**.
   - Seleccione una acción de doble pulsación del **Aux double-tap combo**.
   El estado activo del botón se indica mediante un punto auxiliar.

## Función de cada control

| Control | Predeterminado | Clave de configuración | Comportamiento |
|---------|---------|-------------|----------|
| Indicador Wheel | – | – | Rueda virtual del FlexControl. Haga doble clic para capturar la entrada del ratón/táctil; vuelva a hacer doble clic para liberarla. Muestra la lectura de frecuencia y modo. |
| Indicador Physical | – | – | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close administran el dispositivo. |
| Botón de alternancia Compact | – | – | Activa el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz de usuario mínima. |
| Botón de alternancia External Spin | – | – | Activa la sintonización de rueda con giro externo: arrastrar en el panadapter activa gestos de sintonización con la rueda giratoria. |
| Botón de alternancia Reverse | – | – | Invierte la dirección de sintonización de la rueda. |
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción que se activa con una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción que se activa con dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |
| Control deslizante Wheel Tightness | 45 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta el arrastre de desaceleración de la rueda virtual; 0 = ajustado (parada rápida), 100 = suelto (desaceleración larga). Principalmente para trackpads; no afecta al FlexControl físico. |
| Control deslizante Mouse Sensitivity | 50 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del ratón/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| Botones auxiliares (1-5) | – | – | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción de un solo toque y de doble pulsación. Etiquetados con puntos auxiliares para indicar la selección activa. |
| Cuadro combinado Aux single-tap | – | – | Asigna una acción a la pulsación simple del botón auxiliar seleccionado. Configuración por botón auxiliar. |
| Cuadro combinado Aux double-tap | – | – | Asigna una acción a la doble pulsación del botón auxiliar seleccionado. Configuración por botón auxiliar. |

## Indicadores

| Indicador | Significado |
|-----------|---------|
| Lectura de Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y modo. |

## Notas sobre el FlexControl físico

Cuando un dispositivo FlexControl físico está conectado y envía un comando de reinicio (por ejemplo, `F0304;`), AetherSDR reemite automáticamente el estado de LED almacenado en caché para restaurar las luces indicadoras del hardware de modo que coincidan con el botón de modo de rueda activo de la aplicación. Esto corrige una condición de carrera en la que el reinicio de encendido del dispositivo podría borrar los LED antes de que AetherSDR tuviera la oportunidad de programarlos.

## Soporte de temas

El cuadro de diálogo FlexControl utiliza colores adaptables al tema para los controles deslizantes. El fondo de la ranura usa `color.slider.background`, la porción rellena y el borde del controlador usan `color.accent.success`, y el controlador usa `color.slider.handle`. Estos colores se actualizan automáticamente al cambiar entre los temas Default Dark y Default Light.

## Relacionado

- [Asigne acciones de pulsación y doble pulsación a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configure las acciones de pulsación y doble pulsación para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
