# Cambiar el tipo de filtro de una banda haciendo clic en su icono en la fila de iconos

Cada banda en el Ecualizador Paramétrico Aetherial tiene un tipo de filtro (campana pico, estante, pendiente HP, pendiente LP) que se muestra como un pequeño icono sobre el lienzo del ecualizador. Al hacer clic en un icono, se alterna esa banda al siguiente tipo de filtro sin abrir ningún cuadro de diálogo adicional.

## Antes de comenzar

- El editor flotante debe estar abierto. La fila de iconos solo está disponible en la ventana del editor sin marco "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX", no en el mosaico acoplado del applet.
- Si el editor no está abierto, haga doble clic en la etapa EQ en el widget CHAIN del lado TX o RX para abrirlo. Consulte [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Abra el editor flotante para el lado TX o RX según sea necesario.
2. Localice la fila de iconos de tipo de filtro en la parte superior del área del lienzo del editor. Hay un icono por ranura de banda (hasta 8 iconos), cada uno dibujado en el color de paleta de esa banda mostrando su forma de filtro actual.
3. Haga clic en el icono de la banda cuyo tipo de filtro desea cambiar. Al hacer clic, la banda alterna al siguiente tipo de filtro y selecciona la banda simultáneamente: su controlador en el lienzo se resalta y su columna en la fila de texto de parámetros en la parte inferior se resalta.
4. Continúe haciendo clic en el mismo icono para recorrer los tipos de filtro restantes hasta que se muestre el tipo deseado.

## Función de cada control

| Control                             | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                               | Valor predeterminado                                                                                                                                                                                                                                                              |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fila de iconos de tipo de filtro    | Una fila de hasta 8 iconos en la parte superior del lienzo del editor. Cada icono dibuja la forma de filtro actual de su banda en el color de paleta de esa banda. Haga clic para alternar el tipo de filtro; al hacer clic también se selecciona la banda. Los iconos se atenúan al 35% de opacidad cuando la banda está desviada.                                                                                           | —                                                                                                                                                                                                                                                                                 |
| Fila de texto de parámetros         | Una fila de hasta 8 columnas de texto debajo del lienzo que muestra los valores de Frecuencia, Ganancia y Q de cada banda. Se actualiza en vivo durante los arrastres en el lienzo. Al hacer clic en una columna, se selecciona esa banda. En v0.9.7, el fondo de la fila es transparente, por lo que ya no sangra un relleno oscuro sobre la tira del plan de bandas en la parte inferior del lienzo; las etiquetas permanecen alineadas en la parte inferior dentro de cada columna. | —                                                                                                                                                                                                                                                                                 |
| Suavizado                           | Aplica un promediado de potencia por fracción de octava a la traza del analizador para su visualización; no afecta el cálculo matemático del ecualizador. Una fracción más baja = más suavizado (1/3 es el más suavizado; 1/96 está efectivamente desactivado). Compartido entre los editores TX y RX.                                                                                                                         | Información emergente: 'Suavizado por fracción de octava aplicado a la traza del analizador. Fracción más baja = más suavizado (1/3 = máximo, 1/96 = desactivado). Afecta solo la visualización; el cálculo del ecualizador no cambia.' Ubicado en la tira del encabezado del editor (solo editor flotante). |
| Líneas guía de corte de filtro (TX/RX) | Líneas verticales amarillas discontinuas superpuestas en el lienzo en los límites de corte de filtro TX bajo/alto actuales de la radio (mosaico TX) o en los bordes de la banda pasante RX (mosaico RX). Al pasar el cursor cerca de una línea, el cursor cambia a una flecha de redimensionamiento horizontal. Arrastrar una línea en el editor mueve el corte de filtro correspondiente de la radio en tiempo real.          | Arrastrar las guías de corte TX emite cutoffsDragRequested(Tx, lo, hi), que MainWindow reenvía a TransmitModel. Arrastrar las guías RX escribe en el SliceModel activo. Pase 0 para un borde para suprimir esa guía.                                                          |

## Consejos

- El texto de sugerencia en la tira del encabezado del editor dice "haga clic en el icono para alternar tipo"; esta es la única acción que admite la fila de iconos; no hay menú de clic derecho en los iconos individuales.
- Si un icono aparece atenuado (35% de opacidad), esa banda está desviada. Aún se puede alternar su tipo de filtro, pero la banda no tendrá efecto en la curva del ecualizador hasta que se reactive.
- La familia de filtros seleccionada en el combo Familia de filtros (predeterminado: Butterworth) rige las matemáticas en cascada HP y LP. Si cambia una banda a un tipo HP o LP, se utilizará la familia actualmente seleccionada. Las bandas de pico y estante utilizan su propia topología fija de segundo orden, independientemente de la configuración de Familia de filtros.

## Solución de problemas

- **La fila de iconos no es visible** — La fila de iconos solo está presente en el editor flotante, no en el mosaico acoplado del applet "Aetherial TX EQ" o "Aetherial RX EQ". Abra el editor flotante haciendo doble clic en la etapa EQ en el widget CHAIN.
- **Hacer clic en un icono no tiene efecto en la curva del ecualizador** — Es posible que la banda esté desviada (el icono está atenuado al 35% de opacidad). Vuelva a habilitar la banda para que el cambio de tipo de filtro se refleje en la curva sumada.
- **La fila de texto de parámetros parece superponerse a la tira del plan de bandas** — Este era un problema de visualización en versiones anteriores a v0.9.7 donde el fondo oscuro de la fila se extendía hacia arriba sobre la tira del plan de bandas en la parte inferior del lienzo. Actualice a v0.9.7 o posterior para resolverlo.

## Relacionado

- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Cambiar la familia de filtros HP/LP (Butterworth, Chebyshev, Bessel, Elliptic)](change-the-hp-lp-filter-family-butterworth-chebyshev-bessel-elliptic.md)
- [Leer valores exactos de frecuencia/ganancia/Q en la fila de texto de parámetros](read-exact-freq-gain-q-values-in-the-parameter-text-row.md)
- [Descripción general del Ecualizador Paramétrico Aetherial (TX/RX)](overview.md)
