# Cambiar el tipo de filtro de una banda haciendo clic en su ícono en la fila de íconos

Cada banda del Aetherial Parametric EQ tiene un tipo de filtro (campana de pico, shelving, pendiente HP, pendiente LP) que se muestra como un pequeño ícono sobre el lienzo del EQ. Al hacer clic en un ícono, esa banda avanza al siguiente tipo de filtro sin abrir ningún diálogo adicional.

## Antes de comenzar

- El editor flotante debe estar abierto. La fila de íconos solo está disponible en la ventana del editor sin marco "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX", no en el panel del applet acoplado.
- Si el editor no está abierto, haga doble clic en la etapa EQ del widget CHAIN en el lado TX o RX para abrirlo. Consulte [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Abra el editor flotante para el lado TX o RX según sea necesario.
2. Localice la fila de íconos de tipo de filtro en la parte superior del área del lienzo del editor. Hay un ícono por ranura de banda (hasta 8 íconos), cada uno dibujado en el color de paleta de esa banda y que muestra su forma de filtro actual.
3. Haga clic en el ícono de la banda cuyo tipo de filtro desea cambiar. Al hacer clic, esa banda avanza al siguiente tipo de filtro y simultáneamente la selecciona: su controlador en el lienzo queda resaltado y su columna en la fila de texto de parámetros en la parte inferior también queda resaltada.
4. Continúe haciendo clic en el mismo ícono para recorrer los tipos de filtro restantes hasta que se muestre el tipo deseado.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Fila de íconos de tipo de filtro | Una fila de hasta 8 íconos en la parte superior del lienzo del editor. Cada ícono dibuja la forma de filtro actual de su banda en el color de paleta de esa banda. Haga clic para cambiar el tipo de filtro; al hacer clic también se selecciona la banda. Los íconos se atenúan al 35% de opacidad cuando la banda está desactivada. | — | — |
| Fila de texto de parámetros | Una fila de hasta 8 columnas de texto debajo del lienzo que muestra los valores de Freq, Gain y Q de cada banda. Se actualiza en tiempo real durante los arrastres en el lienzo. Al hacer clic en una columna se selecciona esa banda. | — | — |

## Consejos

- El texto de sugerencia en la barra de encabezado del editor indica "click icon to cycle type" — esta es la única acción que admite la fila de íconos; no existe un menú contextual en los íconos individuales.
- Si un ícono aparece atenuado (35% de opacidad), esa banda está desactivada. Su tipo de filtro aún puede cambiarse, pero la banda no tendrá ningún efecto sobre la curva del EQ hasta que se reactive.
- La familia de filtros seleccionada en el combo Filter family (predeterminado: Butterworth) rige la matemática en cascada de HP y LP. Al cambiar una banda a un tipo HP o LP se utilizará la familia seleccionada en ese momento. Las bandas de campana de pico y shelving utilizan su propia topología fija de segundo orden independientemente del ajuste de Filter family.

## Solución de problemas

- **La fila de íconos no es visible** — La fila de íconos solo está presente en el editor flotante, no en el panel del applet acoplado "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa EQ del widget CHAIN.
- **Hacer clic en un ícono no tiene efecto sobre la curva del EQ** — Es posible que la banda esté desactivada (el ícono aparece atenuado al 35% de opacidad). Reactive la banda para escuchar el cambio de tipo de filtro reflejado en la curva sumada.

## Relacionados

- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elliptic)](change-the-hp-lp-filter-family-butterworth-chebyshev-bessel-elliptic.md)
- [Leer los valores exactos de freq, gain y Q en la fila de texto de parámetros](read-exact-freq-gain-q-values-in-the-parameter-text-row.md)
- [Descripción general del Aetherial Parametric EQ (TX / RX)](overview.md)
