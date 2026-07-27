# Asignar acciones de pulsación y doble toque a la rueda

Configure qué sucede cuando pulsa (un solo toque) o da un doble toque en la rueda física FlexControl o en la rueda virtual del cuadro de diálogo AetherControl.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: **Settings > AetherControl...**
- Si usa un FlexControl físico, asegúrese de que esté conectado (consulte [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)).

## Pasos

1. En el cuadro de diálogo AetherControl, localice el cuadro combinado **Push (action)** cerca de la visualización de la rueda.
2. Haga clic en el cuadro combinado y seleccione una acción de la lista.
3. En el cuadro combinado **Double-tap (action)** situado justo debajo, seleccione una segunda acción.
4. Cierre el cuadro de diálogo. Las nuevas acciones surten efecto de inmediato.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|----------------------|------------------------|----------------|
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción que se activa con una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción que se activa con dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |

Ambos cuadros combinados comparten la misma lista de acciones disponibles. Consulte el fragmento de código fuente para obtener la lista completa de entradas `FlexActionDef`, que incluyen todas las etiquetas mostradas anteriormente.

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)

# Configurar el controlador de hardware AetherControl / FlexControl

Configure la rueda virtual de AetherControl y administre un dispositivo FlexControl físico.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl: **Settings > AetherControl...**

## Pasos

1. En el cuadro de diálogo AetherControl, el indicador **Wheel** muestra la rueda de sintonización virtual. Haga doble clic en ella para capturar la entrada del mouse para la sintonización circular. Vuelva a hacer doble clic para liberarla. Presione Escape como método de liberación secundario.
2. El indicador **Physical** muestra el estado de conexión de un FlexControl físico. Haga clic en **Detect** para encontrar el dispositivo o en **Close** para desconectarlo.
3. Use el botón de alternancia **Compact** para cambiar a una interfaz de usuario mínima que muestre solo la rueda y la lectura de frecuencia.
4. Active **External Spin** para permitir que al arrastrar sobre el panadapter se activen gestos de sintonización con la rueda giratoria.
5. Active **Reverse** para invertir la dirección de sintonización de la rueda.
6. Ajuste el control deslizante **Wheel Tightness** para controlar la resistencia al giro de la rueda virtual. 0 = ajustado (parada rápida), 100 = suelto (giro largo). Afecta principalmente al comportamiento del trackpad.
7. Ajuste el control deslizante **Mouse Sensitivity** para controlar cuánto movimiento capturado del mouse o trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Afecta principalmente al comportamiento del trackpad.
8. Configure los **Aux buttons (1-5)** haciendo clic en un botón para seleccionarlo y luego:
   - Seleccione una acción de un solo toque en el **Aux single-tap combo**.
   - Seleccione una acción de doble toque en el **Aux double-tap combo**.
   El estado activo del botón se indica mediante un punto auxiliar.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|----------------------|------------------------|----------------|
| Indicador Wheel | – | – | Rueda virtual de FlexControl. Haga doble clic para capturar la entrada del mouse o táctil; vuelva a hacer doble clic para liberarla. Muestra la lectura de frecuencia y modo. |
| Indicador Physical | – | – | Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Los botones Detect/Close administran el dispositivo. |
| Botón de alternancia Compact | – | – | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz de usuario mínima. |
| Botón de alternancia External Spin | – | – | Habilita la sintonización externa con la rueda giratoria: al arrastrar sobre el panadapter se activan gestos de sintonización con la rueda giratoria. |
| Botón de alternancia Reverse | – | – | Invierte la dirección de sintonización de la rueda. |
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción que se activa con una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción que se activa con dos pulsaciones rápidas de la rueda. Las mismas opciones de acción que Push. |
| Control deslizante Wheel Tightness | 45 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta la resistencia al giro de la rueda virtual; 0 = ajustado (parada rápida), 100 = suelto (giro largo). Principalmente para trackpads; no afecta al FlexControl físico. |
| Control deslizante Mouse Sensitivity | 50 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| Botones auxiliares (1-5) | – | – | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción de un solo toque y doble toque. Etiquetados con puntos auxiliares para indicar la selección activa. |
| Aux single-tap combo | – | – | Asigna una acción al toque único del botón auxiliar seleccionado. Configuración por botón auxiliar. |
| Aux double-tap combo | – | – | Asigna una acción al doble toque del botón auxiliar seleccionado. Configuración por botón auxiliar. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| Lectura de Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y modo. |

## Notas sobre el tamaño de la ventana

El cuadro de diálogo AetherControl utiliza un área de desplazamiento para su contenido cuando no está en modo compacto. El controlador completo puede ser más alto que su pantalla; el área de contenido se desplaza verticalmente según sea necesario. El cuadro de diálogo no se abrirá más alto que el espacio de trabajo de la pantalla disponible (teniendo en cuenta las barras de tareas). El ancho mínimo no compacto es 430 píxeles; el cuadro de diálogo no se puede redimensionar a un ancho menor del que requiere su contenido.

## Notas sobre el FlexControl físico

Cuando un dispositivo FlexControl físico está conectado y envía un comando de reinicio (por ejemplo, `F0304;`), AetherSDR vuelve a emitir automáticamente el estado de LED almacenado en caché para restaurar las luces indicadoras del hardware y que coincidan con el botón de modo de rueda activo de la aplicación. Esto soluciona una condición de carrera donde el reinicio al encender el dispositivo podría, de otro modo, borrar los LEDs antes de que AetherSDR tuviera la oportunidad de programarlos.

## Soporte de temas

El cuadro de diálogo FlexControl utiliza colores adaptables al tema para los controles deslizantes. El fondo de la ranura usa `color.slider.background`, la parte rellena y el borde del control usan `color.accent.success`, y el control usa `color.slider.handle`. Estos colores se actualizan automáticamente al cambiar entre los temas Default Dark y Default Light.

## Relacionado

- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
