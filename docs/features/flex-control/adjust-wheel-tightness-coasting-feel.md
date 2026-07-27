# Ajustar la rigidez de la rueda (sensación de deslizamiento)

Configure cuánto tiempo continúa girando la rueda de sintonización virtual (deslizamiento) después de dejar de mover el mouse o trackpad. Un ajuste más firme la detiene más rápido; uno más suave desliza por más tiempo.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Busque el control deslizante **Wheel Tightness** en el diálogo.
2. Arrastre el control deslizante a la sensación de deslizamiento que prefiera:
   - **0** (Tight) — la rueda se detiene casi inmediatamente al dejar de moverse.
   - **100** (Loose) — la rueda desliza por un largo tiempo después de detenerse.
   - **45** — valor predeterminado.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

> **Nota:** Este ajuste afecta únicamente a la rueda virtual (sintonización con mouse/trackpad). No afecta a un dispositivo físico FlexControl.

## Función de cada control

| Control | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|----------------|-------|------------------------|----------------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) | Ajusta la fricción de deslizamiento de la rueda virtual. 0 = firme (parada rápida), 100 = suave (deslizamiento largo). |
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) | Ajusta cuánto movimiento capturado del mouse/trackpad hace girar la rueda virtual. El punto medio (50) produce una escala 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |

## Relacionado

- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)

---

# Acción de rueda para volumen de audio de slice

La acción **Slice Audio Volume** le permite ajustar el volumen de audio del slice activo usando la rueda de AetherControl.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el diálogo, localice el cuadro combinado **Push (action)** o **Double-tap (action)**, o uno de los cuadros combinados **Aux** de toque único o doble toque.
2. Haga clic en el cuadro combinado y seleccione **Slice Audio Volume** de la lista.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

Cuando presione el botón asignado o active el doble toque, la rueda de sintonización cambia a controlar el volumen de audio del slice. Girar la rueda en el sentido de las agujas del reloj aumenta el volumen; en sentido contrario lo disminuye.

> **Nota:** Esta acción se añadió en AetherSDR v26.6.3.

---

# Comportamiento del área de desplazamiento y modo compacto

El diálogo AetherControl incluye un área de desplazamiento que garantiza que todos los controles sigan siendo accesibles incluso en pantallas pequeñas o con escalado DPI.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Cómo funciona

- El diálogo utiliza un área de desplazamiento interna (`QScrollArea`) para contener todos los controles de configuración de AetherControl.
- Cuando no está en modo compacto, el diálogo tiene una altura mínima de 610 píxeles y un ancho mínimo de 430 píxeles.
- Si la altura disponible de la pantalla es menor que el tamaño natural del contenido, la altura del diálogo se ajusta para adaptarse al espacio de trabajo y el contenido se vuelve desplazable.
- La barra de desplazamiento horizontal siempre está oculta; el ancho mínimo asegura que no haya recorte horizontal.
- En modo compacto (use el botón de alternancia **Compact**), el diálogo se reduce para mostrar solo la rueda y el indicador de frecuencia. Los botones auxiliares están ocultos.

## Modo compacto

Haga clic en **Compact** en el encabezado del diálogo AetherControl. El diálogo se redimensiona inmediatamente a su tamaño mínimo. Haga clic en **Compact** nuevamente para restaurar el diseño completo de controles.

## Ajuste a la pantalla

El diálogo verifica automáticamente la altura disponible de la pantalla (excluyendo barras de tareas y paneles acoplados) al entrar en modo no compacto. Nunca se abre más alto que el espacio de trabajo y el contenido se desplaza verticalmente si es necesario. Esto evita que el diálogo exceda la pantalla incluso con muchos botones auxiliares o escalado DPI alto.

> **Nota:** Este comportamiento del área de desplazamiento se añadió en AetherSDR v26.7.4 para solucionar los problemas #3662 y #4365.

---

# Referencia de controles del diálogo AetherControl

| Control | Tipo | Predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|------|----------------|-------|------------------------|----------------|
| **Wheel** | indicador | — | — | — | Rueda virtual FlexControl: gire con el mouse/toque para sintonizar el slice activo. Muestra la frecuencia y el modo. |
| **Physical** | indicador | — | — | — | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Botones Detectar/Cerrar para gestionar el dispositivo físico. |
| **Compact** | botón de alternancia | — | — | — | Activa/desactiva el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz mínima. |
| **External Spin** | botón de alternancia | — | — | — | Habilita la sintonización con giro externo: arrastrar sobre el panadapter activa gestos de sintonización con giro de rueda. |
| **Reverse** | botón de alternancia | — | — | — | Invierte la dirección de sintonización de la rueda. |
| **Push (action)** | cuadro combinado | — | — | `FlexControlButtonAction_*` | Asigna una acción al presionar la rueda (toque único). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, banda arriba/abajo y más. |
| **Double-tap (action)** | cuadro combinado | — | — | — | Asigna una acción al doble toque en la rueda. |
| **Wheel Tightness** | control deslizante | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta la fricción de deslizamiento de la rueda virtual; 0 = firme (parada rápida), 100 = suave (deslizamiento largo). Principalmente para trackpads; no afecta al FlexControl físico. |
| **Mouse Sensitivity** | control deslizante | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del mouse/trackpad hace girar la rueda virtual. El punto medio (50) produce una escala 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| **Aux buttons (1-5)** | botón pulsador | — | 5 botones | — | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción para toque único y doble toque. |
| **Aux single-tap combo** | cuadro combinado | — | — | — | Asigna una acción al toque único en el botón auxiliar seleccionado. |
| **Aux double-tap combo** | cuadro combinado | — | — | — | Asigna una acción al doble toque en el botón auxiliar seleccionado. |
