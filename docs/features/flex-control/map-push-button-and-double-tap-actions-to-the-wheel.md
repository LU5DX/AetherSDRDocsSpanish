# Asignar acciones de pulsación y doble pulsación a la rueda

Configure qué sucede cuando pulsa (toque simple) o toca dos veces la rueda física del FlexControl o la rueda virtual en el diálogo de AetherControl.

## Antes de comenzar

- Abra el diálogo AetherControl: **Settings > AetherControl...**
- Si usa un FlexControl físico, asegúrese de que esté conectado (consulte [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)).

## Pasos

1. En el diálogo AetherControl, localice el cuadro combinado **Push (action)** cerca de la visualización de la rueda.
2. Haga clic en el cuadro combinado y seleccione una acción de la lista.
3. En el cuadro combinado **Double-tap (action)** directamente debajo, seleccione una segunda acción.
4. Cierre el diálogo. Las nuevas acciones surten efecto de inmediato.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|----------------------|------------------------|----------------|
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción activada por una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción activada por dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |

Ambos cuadros combinados comparten la misma lista de acciones disponibles. Consulte el fragmento de código fuente para la lista completa de entradas `FlexActionDef`, que incluyen todas las etiquetas mostradas arriba.

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)

# Configure el controlador de hardware AetherControl / FlexControl

Configure la rueda virtual de AetherControl y administre un dispositivo FlexControl físico.

## Antes de comenzar

- Abra el diálogo AetherControl: **Settings > AetherControl...**

## Pasos

1. En el diálogo AetherControl, el indicador **Wheel** muestra la rueda de sintonización virtual. Haga doble clic para capturar la entrada del mouse para sintonización circular. Vuelva a hacer doble clic para liberar. Presione Escape como vía de liberación secundaria.
2. El indicador **Physical** muestra el estado de conexión de un FlexControl físico. Haga clic en **Detect** para encontrar el dispositivo, o en **Close** para desconectarlo.
3. Use el botón de alternancia **Compact** para cambiar a una interfaz de usuario mínima que muestra solo la rueda y la lectura de frecuencia.
4. Active **External Spin** para permitir arrastrar en el panadapter y activar gestos de sintonización de giro de rueda.
5. Active **Reverse** para invertir la dirección de sintonización de la rueda.
6. Ajuste **Wheel Tightness** con el control deslizante para controlar el arrastre de inercia de la rueda virtual. 0 = apretado (parada rápida), 100 = suelto (inercia larga). Afecta principalmente el comportamiento del trackpad.
7. Ajuste **Mouse Sensitivity** con el control deslizante para controlar cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Afecta principalmente el comportamiento del trackpad.
8. Configure los **Aux buttons (1-5)** haciendo clic en un botón para seleccionarlo, luego:
   - Seleccione una acción de toque simple del **Aux single-tap combo**.
   - Seleccione una acción de doble toque del **Aux double-tap combo**.
   El estado activo del botón se indica mediante un punto auxiliar.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|----------------------|------------------------|----------------|
| Indicador Wheel | – | – | Rueda virtual de FlexControl. Haga doble clic para capturar la entrada del mouse/táctil; vuelva a hacer doble clic para liberar. Muestra la frecuencia y el modo. |
| Indicador Physical | – | – | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Los botones Detect/Close administran el dispositivo. |
| Alternancia Compact | – | – | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz de usuario mínima. |
| Alternancia External Spin | – | – | Activa la sintonización de giro de rueda externa: arrastrar en el panadapter activa gestos de sintonización de giro de rueda. |
| Alternancia Reverse | – | – | Invierte la dirección de sintonización de la rueda. |
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción activada por una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción activada por dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |
| Control deslizante Wheel Tightness | 45 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta el arrastre de inercia de la rueda virtual; 0 = apretado (parada rápida), 100 = suelto (inercia larga). Principalmente para trackpads; no afecta al FlexControl físico. |
| Control deslizante Mouse Sensitivity | 50 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| Aux buttons (1-5) | – | – | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción de toque simple y doble toque. Etiquetados con puntos auxiliares para indicar la selección activa. |
| Aux single-tap combo | – | – | Asigna una acción al toque simple del botón auxiliar seleccionado. Configuración por botón auxiliar. |
| Aux double-tap combo | – | – | Asigna una acción al doble toque del botón auxiliar seleccionado. Configuración por botón auxiliar. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| Lectura de Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y modo. |

## Notas sobre el FlexControl físico

Cuando un dispositivo FlexControl físico está conectado y envía un comando de reinicio (por ejemplo, `F0304;`), AetherSDR reemite automáticamente el estado LED almacenado en caché para restaurar las luces indicadoras del hardware al modo de rueda activo de la aplicación. Esto soluciona una condición de carrera donde el reinicio por encendido del dispositivo podría borrar los LEDs antes de que AetherSDR tuviera la oportunidad de programarlos.

## Soporte de temas

El diálogo FlexControl utiliza colores que reconocen el tema para los controles deslizantes. El fondo de la ranura usa `color.slider.background`, la porción rellena y el borde del control usan `color.accent.success`, y el control usa `color.slider.handle`. Estos colores se actualizan automáticamente al alternar entre los temas Default Dark y Default Light.

## Relacionado

- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
