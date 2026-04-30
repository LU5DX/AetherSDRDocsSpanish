# Seleccione la antena RX o TX para esta slice

El applet RX Controls le permite elegir qué puerto de antena utiliza la FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Úselo cuando tenga múltiples antenas conectadas y necesite enrutar una slice específica a un puerto específico.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se completa a partir de la configuración de puertos de la radio. Confirme que sus antenas estén conectadas y reconocidas por la radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet RX Controls. Si no es visible, haga clic en el botón **RX** en la bandeja de la barra lateral derecha.
2. Si tiene más de una slice, haga clic en la pestaña de slice (A a H) correspondiente a la slice que desea cambiar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, por ejemplo **ANT1**). Aparece un menú que lista todos los puertos de antena disponibles. Haga clic en el puerto que desea. Una marca de verificación muestra la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, por ejemplo **ANT1**). Aparece un menú que lista los puertos de antena compatibles con TX. Haga clic en el puerto que desea.

## Qué hace cada control

| Control                                | Por defecto | Valores válidos                            |
|----------------------------------------|-------------|---------------------------------------------|
| **ANT1** (antena RX, etiqueta azul)    | ANT1        | Puertos de antena de la ant_list de la radio |
| **ANT1** (antena TX, etiqueta roja)    | ANT1        | Puertos compatibles con TX de la ant_list de la radio |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen lado a lado en la fila de encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en la slice A no afecta a la slice B.
- A partir de v0.9.3, los botones de pestaña de slice y el indicador de slice utilizan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en widgets de VFO y barras de medición. Los colores no son configurables desde la página de controles de antena; se aplican en todo el applet.

## Comportamiento en modo NT

NT es un modo digital añadido en v0.9.3. Su comportamiento dentro del applet RX Controls coincide con otros modos digitales (DIGU/DIGL) de las siguientes formas:

- **Preajustes de filtro** — NT utiliza los mismos anchos de preajuste de filtro que DIGU y DIGL (100–2000 Hz).
- **Visualización de ancho de filtro** — El indicador de ancho de filtro obtiene su valor del borde superior de la banda de paso, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Squelch** — El botón **SQL** y el control deslizante de nivel de squelch se deshabilitan en modo NT. Si el squelch estaba activo cuando cambió al modo NT, AetherSDR desactiva automáticamente el squelch y lo restaura cuando cambia de nuevo. Esto coincide con el comportamiento para DIGU y DIGL; el modo CW se maneja de forma diferente porque la radio gestiona directamente su estado de squelch.

## Solución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de la ant_list de la radio. Verifique que el puerto esté configurado y reconocido en los ajustes propios de la radio. AetherSDR no puede agregar puertos que la radio no haya reportado.
- **El menú de antena TX le falta un puerto que aparece en el menú de antena RX** — Los puertos cuyos nombres comienzan con `RX` se excluyen intencionalmente del menú de antena TX porque la radio los trata como solo recepción.
- **Ambas etiquetas están atenuadas o no responden** — AetherSDR no está conectado a la radio. Reconecte a través de `Settings > Connect to Radio...`.
- **El botón SQL está atenuado después de cambiar al modo NT** — NT es un modo digital. AetherSDR deshabilita el squelch en todos los modos digitales (DIGU, DIGL, NT) porque el audio se enruta a través de DAX y el squelch no tiene efecto significativo. Cambie a un modo no digital para volver a habilitar el squelch.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender slices y VFOs](../../getting-started/concepts/understanding-slices.md)
