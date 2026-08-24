# Asignar acciones de pulsación y doble pulsación a la rueda

Configure qué sucede cuando pulsa (toca una vez) o toca dos veces la rueda física FlexControl o la rueda virtual en el diálogo AetherControl.

## Antes de comenzar

- Abra el diálogo AetherControl: **Settings > AetherControl...**
- Si utiliza un FlexControl físico, asegúrese de que esté conectado (consulte [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)).

## Pasos

1. En el diálogo AetherControl, localice el cuadro combinado **Push (action)** cerca de la pantalla de la rueda.
2. Haga clic en el cuadro combinado y seleccione una acción de la lista.
3. En el cuadro combinado **Double-tap (action)**, directamente debajo, seleccione una segunda acción.
4. Cierre el diálogo. Las nuevas acciones se aplican de inmediato.

## Qué hace cada control

| Control | Predeterminado | Clave de configuración | Comportamiento |
|---------|---------|-------------|----------|
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción activada por una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción activada por dos pulsaciones rápidas de la rueda. Mismas opciones de acción que Push. |

Ambos cuadros combinados comparten la misma lista de acciones disponibles. Consulte el fragmento de código fuente para la lista completa de entradas `FlexActionDef`, que incluyen todas las etiquetas mostradas arriba.

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)

# Configurar el controlador de hardware AetherControl / FlexControl

Configure la rueda virtual AetherControl y administre un dispositivo FlexControl físico.

## Antes de comenzar

- Abra el diálogo AetherControl: **Settings > AetherControl...**

## Pasos

1. En el diálogo AetherControl, el indicador **Wheel** muestra la rueda de sintonización virtual. Haga doble clic en él para capturar la entrada del mouse y realizar la sintonización circular. Haga doble clic nuevamente para liberarlo. Presione Escape como ruta de liberación secundaria.
2. El indicador **Physical** muestra el estado de conexión de un FlexControl físico. Haga clic en **Detect** para encontrar el dispositivo, o en **Close** para desconectarlo.
3. Use el botón de alternancia **Compact** para cambiar a una interfaz mínima que muestre solo la rueda y la lectura de frecuencia.
4. Active **External Spin** para permitir que el arrastre sobre el panadapter active gestos de sintonización tipo rueda giratoria.
5. Active **Reverse** para invertir la dirección de sintonización de la rueda.
6. Ajuste **Wheel Tightness** con el control deslizante para controlar el arrastre de inercia de la rueda virtual. 0 = ajustado (parada rápida), 100 = suelto (inercia larga). Afecta principalmente el comportamiento del trackpad.
7. Ajuste **Mouse Sensitivity** con el control deslizante para controlar cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Afecta principalmente el comportamiento del trackpad.
8. Configure los **Aux buttons (1-5)** haciendo clic en un botón para seleccionarlo y luego:
   - Seleccione una acción de pulsación simple en el **Aux single-tap combo**.
   - Seleccione una acción de doble pulsación en el **Aux double-tap combo**.
   El estado activo del botón se indica mediante un punto auxiliar.

## Qué hace cada control

| Control | Predeterminado | Clave de configuración | Comportamiento |
|---------|---------|-------------|----------|
| Indicador Wheel | – | – | Rueda virtual FlexControl. Haga doble clic para capturar la entrada del mouse/táctil; haga doble clic nuevamente para liberar. Muestra la lectura de frecuencia y modo. |
| Indicador Physical | – | – | Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Los botones Detect/Close administran el dispositivo. |
| Alternancia Compact | – | – | Activa el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. |
| Alternancia External Spin | – | – | Activa la sintonización externa tipo rueda giratoria: el arrastre sobre el panadapter activa gestos de sintonización. |
| Alternancia Reverse | – | – | Invierte la dirección de sintonización de la rueda. |
| Cuadro combinado Push (action) | – | `FlexControlButtonAction_*` | Selecciona la acción activada por una sola pulsación de la rueda. Las opciones incluyen: Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Slice Audio Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macros 1-12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down y None. |
| Cuadro combinado Double-tap (action) | – | – | Selecciona la acción activada por dos pulsaciones rápidas de la rueda. Mismas opciones de acción que Push. |
| Control deslizante Wheel Tightness | 45 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta el arrastre de inercia de la rueda virtual; 0 = ajustado (parada rápida), 100 = suelto (inercia larga). Principalmente para trackpads; no afecta al FlexControl físico. |
| Control deslizante Mouse Sensitivity | 50 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| Aux buttons (1-5) | – | – | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción de pulsación simple y de doble pulsación. Marcados con puntos auxiliares para indicar la selección activa. |
| Aux single-tap combo | – | – | Asigna una acción a la pulsación simple del botón auxiliar seleccionado. Configuración por botón auxiliar. |
| Aux double-tap combo | – | – | Asigna una acción a la doble pulsación del botón auxiliar seleccionado. Configuración por botón auxiliar. |

## Indicadores

| Indicador | Significado |
|-----------|---------|
| Lectura de Slice / Frecuencia / Modo | Muestra qué slice está vinculado, su frecuencia actual y su modo. |

## Notas sobre el tamaño de la ventana

El diálogo AetherControl utiliza un área de desplazamiento para su contenido cuando no está en modo compacto. El controlador completo puede ser más alto que su pantalla; el área de contenido se desplaza verticalmente según sea necesario. El diálogo no se abrirá más alto que el espacio de trabajo disponible en pantalla (teniendo en cuenta las barras de tareas). El ancho mínimo en modo no compacto es de 430 píxeles; el diálogo no se puede redimensionar a un ancho menor del que requiere su contenido.

## Notas sobre el FlexControl físico

Cuando un dispositivo FlexControl físico está conectado y envía un comando de reinicio (por ejemplo, `F0304;`), AetherSDR reemite automáticamente el estado de LED almacenado en caché para restaurar las luces indicadoras del hardware y que coincidan con el botón de modo de rueda activo de la aplicación. Esto corrige una condición de carrera donde el reinicio de encendido del dispositivo podría borrar los LED antes de que AetherSDR tuviera la oportunidad de programarlos.

## Notas sobre la reconexión automática

Si un FlexControl físico conectado deja de estar disponible — por ejemplo, si se desconecta el cable USB o el dispositivo se vuelve a enumerar — AetherSDR reintenta la conexión automáticamente. Los reintentos comienzan cada 2 segundos y retroceden exponencialmente hasta un máximo de 30 segundos. Durante los reintentos, el dispositivo se vuelve a detectar en lugar de reutilizar el nombre de puerto anterior, porque una re-enumeración USB puede asignar un puerto COM diferente. AetherSDR continúa reintentando hasta que se encuentra el dispositivo o usted cierra la conexión explícitamente; se registra una advertencia una vez por interrupción, no en cada intento de reintento. Una vez que el dispositivo se reconecta, su estado de LED se vuelve a aplicar automáticamente.

## Soporte de temas

El diálogo FlexControl utiliza colores conscientes del tema para los controles deslizantes. El fondo de la ranura usa `color.slider.background`, la porción rellena y el borde del control usan `color.accent.success`, y el control usa `color.slider.handle`. Estos colores se actualizan automáticamente al alternar entre los temas Default Dark y Default Light.

## Relacionado

- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
