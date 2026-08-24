# Descripción general de Asignación de Ulanzi Dial

El diálogo de Asignación de Ulanzi Dial le permite mapear visualmente los botones físicos y el control rotatorio de su Ulanzi Dial a acciones de AetherSDR. Un dial estilizado con etiquetas de llamada muestra la vinculación actual de cada control; puede reasignar cualquier control a una acción diferente desde una lista, o aprender una nueva firma de control presionando el control físico.

## Cómo funciona

El diálogo muestra una imagen estilizada del Ulanzi Dial con etiquetas de llamada codificadas por color ancladas a cada control físico. Cada etiqueta corresponde a un control de hardware específico: los tres botones superiores, la pulsación del dial, las cuatro pestañas laterales y la perilla rotatoria. La asignación firma-a-etiqueta es una propiedad fija del firmware del dial y no se puede cambiar; solo la acción vinculada a cada control es configurable.

Para cada etiqueta, seleccione una acción del menú desplegable para vincular ese control físico a una función de AetherSDR. Al hacer clic en una etiqueta sin acción vinculada se ingresa al modo de aprendizaje, donde presiona el control físico correspondiente para capturar su firma y vincularlo. El control rotatorio tiene su propio menú desplegable dedicado para acciones relacionadas con la sintonía.

El diálogo muestra el estado de la conexión, el último evento de entrada recibido y le permite restablecer todas las vinculaciones a sus valores predeterminados.

## Controles

| Control | Descripción |
|---------|-------------|
| **Etiquetas de llamada** | Haga clic en una etiqueta para ingresar al modo de aprendizaje para ese control, luego presione el botón o la perilla física del dial para vincularlo. |
| **Menú desplegable de sintonía** | Asigna la perilla rotatoria a una de 15 acciones: Frequency (Tune Slice), Filter Bandwidth, Slice Audio Volume, Master Volume, Headphone Volume, Panadapter Zoom, Band Zoom, Segment Zoom, RIT, XIT, AGC-T, RF Gain, APF, CW Speed o RF Power. Predeterminado: Frequency (Tune Slice). |
| **Reset to Defaults** | Restaura cada etiqueta y el menú desplegable rotatorio a sus acciones predeterminadas. |
| **Grant access** (solo Linux) | Aparece cuando se detecta un dial pero no se puede abrir su nodo de entrada. Instala una regla udev (con aprobación del administrador) para que AetherSDR pueda leer la entrada del dial. Requerido una vez por máquina. |
| **Last event** | Muestra el evento de entrada más reciente capturado del dial. |
| **Close** | Cierra el diálogo. |

## Vinculaciones predeterminadas de botones

| Control físico | Acción predeterminada |
|---|---|
| Superior izquierdo | MOX toggle |
| Superior central | RIT toggle |
| Superior derecho | Tune toggle |
| Izquierdo superior | None |
| Izquierdo inferior | None |
| Derecho superior | Next slice |
| Derecho inferior | None |
| Pulsación del dial | Mute toggle |

## Relacionados

- [Aprenda una firma de control de Ulanzi Dial](learn-a-ulanzi-dial-control-signature.md)
- [Asigne un botón de Ulanzi Dial a una acción de AetherSDR](map-a-ulanzi-dial-button-to-an-aethersdr-action.md)
