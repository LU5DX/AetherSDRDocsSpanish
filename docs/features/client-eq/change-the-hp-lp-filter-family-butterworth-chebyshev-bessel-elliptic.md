# Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elíptico)

El selector **Filter family** controla la matemática utilizada para las bandas de filtro HP y LP en el EQ del cliente. Cambiarlo permite equilibrar la pendiente de corte, la planitud de la banda de paso y la linealidad de fase según sus objetivos de audio.

## Antes de comenzar

- El bloque EQ del camino que desea modificar (TX o RX) debe estar habilitado. Consulte [Omitir el bloque EQ en la cadena](bypass-the-eq-stage-from-the-chain.md).
- El editor flotante debe estar abierto. El selector **Filter family** solo está disponible en el editor sin marco, no en el panel de applet acoplado. Consulte [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).
- Al menos una banda debe estar configurada como filtro HP o LP. El ajuste no produce ningún efecto audible si solo hay bandas de pico y shelving.

## Pasos

1. Abra el editor flotante del camino que desea modificar: haga doble clic en el bloque EQ del widget CHAIN en el lado TX o RX. El título de la ventana mostrará "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice el cuadro combinado **Filter family** en la barra de encabezado del editor, a la derecha del botón **Peak Hold**.
3. Haga clic en el cuadro combinado y seleccione una de las cuatro opciones: **Butterworth**, **Chebyshev**, **Bessel** o **Elliptic**.
4. La curva del EQ en el lienzo se actualiza de inmediato. Si hay bandas HP o LP presentes, sus pendientes se redibujarán para reflejar la nueva familia.

La selección se guarda automáticamente. Se almacena de forma independiente para cada camino: `ClientEqTxFilterFamily` para el editor TX y `ClientEqRxFilterFamily` para el editor RX.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Filter family** (editor TX) | Butterworth | Butterworth, Chebyshev, Bessel, Elliptic | `ClientEqTxFilterFamily` |
| **Filter family** (editor RX) | Butterworth | Butterworth, Chebyshev, Bessel, Elliptic | `ClientEqRxFilterFamily` |

**Butterworth** — banda de paso maximalmente plana; sin ondulación en la banda de paso ni en la banda de rechazo. La opción predeterminada para uso general.

**Chebyshev** — banda de transición más pronunciada que Butterworth, con 1 dB de ondulación en la banda de paso.

**Bessel** — respuesta de fase lineal y la caída más suave de las cuatro familias. Preserva la forma de los transitorios.

**Elliptic** — transición más pronunciada de las cuatro opciones, con ondulación tanto en la banda de paso como en la banda de rechazo.

Estas opciones se aplican únicamente a los tipos de banda HP y LP. Las bandas de pico y shelving utilizan su propia topología fija de segundo orden, independientemente de este ajuste.

## Consejos

- Si no hay bandas HP o LP en el EQ actual, cambiar la familia de filtros no produce ningún efecto audible. Agregue primero una banda HP o LP mediante la fila de iconos de tipo de filtro.
- La familia de filtros se configura de forma independiente para TX y RX. Cambiarla en el editor TX no afecta al editor RX, y viceversa.
- Al hacer clic en **Reset** en la barra de encabezado del editor, la familia de filtros vuelve a **Butterworth**, junto con todos los parámetros de banda.

## Solución de problemas

- **El cuadro combinado Filter family no es visible** — El cuadro combinado solo está presente en el editor flotante, no en el panel de applet acoplado. Haga doble clic en el bloque EQ del widget CHAIN para abrir el editor.
- **Cambiar la familia no tiene efecto en la curva** — No hay bandas HP o LP activas. El ajuste solo afecta a la matemática en cascada de HP y LP. Verifique el tipo de cada banda mediante la fila de iconos de tipo de filtro.

## Relacionados

- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en ambos lados](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar el tipo de filtro de una banda haciendo clic en su icono en la fila de iconos](change-a-band-s-filter-type-by-clicking-its-icon-in-the-icon-row.md)
- [Restablecer todas las bandas del EQ a la plantilla predeterminada de 10 bandas](reset-all-eq-bands-to-the-default-10-band-template.md)
- [Omitir el bloque EQ en la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
