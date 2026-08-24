# Ajustar la rigidez de la rueda (sensación de inercia)

Configure cuánto tiempo continúa girando la rueda de sintonización virtual (inercia) después de dejar de mover el mouse o el trackpad. Un ajuste más firme detiene la rueda más rápido; un ajuste más suelto permite que gire por más tiempo.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. Busque el control deslizante **Wheel Tightness** en el diálogo.
2. Arrastre el control deslizante hasta la sensación de inercia que prefiera:
   - **0** (Tight) — la rueda se detiene casi inmediatamente cuando deja de mover el mouse.
   - **100** (Loose) — la rueda continúa girando durante mucho tiempo después de detenerse.
   - **45** — valor predeterminado.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

> **Nota:** Este ajuste afecta únicamente a la rueda virtual (sintonización con mouse/trackpad). No afecta a un dispositivo físico FlexControl.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|---------|-------|-------------|----------|
| Control deslizante Wheel Tightness | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `looseness`) | Ajusta la inercia de giro de la rueda virtual. 0 = firme (detención rápida), 100 = suelto (inercia larga). |
| Control deslizante Mouse Sensitivity | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo `sensitivity`) | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |

## Relacionado

- [Ajustar la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)

---

# Acción de rueda Slice Audio Volume

La acción **Slice Audio Volume** le permite ajustar el volumen de audio del slice activo usando la rueda de AetherControl.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el diálogo, localice el cuadro combinado **Push (action)** o **Double-tap (action)**, o uno de los cuadros combinados **Aux** de toque simple o doble toque.
2. Haga clic en el cuadro combinado y seleccione **Slice Audio Volume** de la lista.
3. Cierre el diálogo. Los cambios se guardan automáticamente.

Cuando presiona el botón asignado o activa el doble toque, la rueda de sintonización cambia a controlar el volumen de audio del slice. Girar la rueda en el sentido de las agujas del reloj aumenta el volumen; girarla en sentido contrario lo disminuye.

> **Nota:** Esta acción se agregó en AetherSDR v26.6.3.

---

# Área de desplazamiento y comportamiento del modo compacto

El diálogo AetherControl incluye un área de desplazamiento que garantiza que todos los controles sigan siendo accesibles incluso en pantallas cortas o con escala DPI.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Cómo funciona

- El diálogo utiliza un área de desplazamiento interna (`QScrollArea`) para contener todos los controles de configuración de AetherControl.
- Cuando no está en modo compacto, el diálogo tiene una altura mínima de 610 píxeles y un ancho mínimo de 430 píxeles.
- Si la altura disponible de la pantalla es menor que el tamaño natural del contenido, la altura del diálogo se limita para ajustarse al espacio de trabajo y el contenido se vuelve desplazable.
- La barra de desplazamiento horizontal está siempre oculta; el ancho mínimo garantiza que no haya recorte horizontal.
- En modo compacto (use el botón de alternancia **Compact**), el diálogo se reduce para mostrar solo la rueda y la lectura de frecuencia. Los botones auxiliares quedan ocultos.

## Modo compacto

Haga clic en **Compact** en el encabezado del diálogo AetherControl. El diálogo se redimensiona inmediatamente a su tamaño mínimo. Haga clic en **Compact** nuevamente para restaurar el diseño completo de controles.

## Ajuste a la pantalla

El diálogo verifica automáticamente la altura disponible de la pantalla (excluyendo barras de tareas y paneles acoplados) al entrar en modo no compacto. Nunca se abre más alto que el espacio de trabajo, y el contenido se desplaza verticalmente si es necesario. Esto evita que el diálogo exceda la pantalla incluso con muchos botones auxiliares o una escala DPI alta.

> **Nota:** Este comportamiento del área de desplazamiento se agregó en AetherSDR v26.7.4 para resolver los problemas #3662 y #4365.

---

# Recuperación de conexión del FlexControl físico

AetherSDR reintenta automáticamente la conexión con el dispositivo físico FlexControl cuando se pierde la conexión o el dispositivo no está disponible temporalmente.

## Cómo funciona

- Cuando falla un intento de conexión, AetherSDR sigue reintentando en lugar de rendirse inmediatamente.
- Los reintentos comienzan con intervalos de 2 segundos y aumentan gradualmente hasta un máximo de 30 segundos entre intentos.
- El puerto del dispositivo se vuelve a detectar en cada reintento, por lo que una re-enumeración USB que asigne un nombre de puerto diferente se maneja automáticamente.
- Si el dispositivo se desconecta y se vuelve a conectar, AetherSDR se reconecta en el nuevo puerto sin requerir intervención manual.
- El indicador **Physical** en el diálogo AetherControl muestra el estado actual de la conexión.

## Cuándo aplica

- El dispositivo se desconecta y se vuelve a conectar.
- El puerto USB es re-enumerado por el sistema operativo.
- Otro proceso mantiene temporalmente el puerto.
- El dispositivo está en medio de la enumeración cuando AetherSDR se inicia.

> **Nota:** La reconexión automática se agregó en AetherSDR v26.8.4 para resolver el problema #4574.

---

# Referencia de controles del diálogo AetherControl

| Control | Tipo | Predeterminado | Rango | Clave de ajuste | Comportamiento |
|---------|------|---------|-------|-------------|----------|
| **Wheel** | indicador | — | — | — | Rueda virtual FlexControl: gire con el mouse/táctil para sintonizar el slice activo. Muestra la frecuencia y el modo. |
| **Physical** | indicador | — | — | — | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Botones Detect/Close para gestionar el dispositivo físico. |
| **Compact** | botón de alternancia | — | — | — | Alterna el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. |
| **External Spin** | botón de alternancia | — | — | — | Habilita la sintonización con giro externo de rueda: arrastrar sobre el panadapter activa gestos de sintonización por giro de rueda. |
| **Reverse** | botón de alternancia | — | — | — | Invierte la dirección de sintonización de la rueda. |
| **Push (action)** | cuadro combinado | — | — | `FlexControlButtonAction_*` | Asigna una acción al presionar la rueda (toque simple). Las opciones incluyen ciclo de modo, zoom por pasos, reinicio de zoom, banda arriba/abajo y más. |
| **Double-tap (action)** | cuadro combinado | — | — | — | Asigna una acción al doble toque en la rueda. |
| **Wheel Tightness** | control deslizante | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) | Ajusta la inercia de giro de la rueda virtual; 0 = firme (detención rápida), 100 = suelto (inercia larga). Principalmente para trackpads; no afecta al FlexControl físico. |
| **Mouse Sensitivity** | control deslizante | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. |
| **Aux buttons (1-5)** | botón pulsador | — | 5 botones | — | Cinco botones auxiliares configurables; cada uno tiene un cuadro combinado de acción para toque simple y doble toque. |
| **Aux single-tap combo** | cuadro combinado | — | — | — | Asigna una acción al toque simple en el botón auxiliar seleccionado. |
| **Aux double-tap combo** | cuadro combinado | — | — | — | Asigna una acción al doble toque en el botón auxiliar seleccionado. |
