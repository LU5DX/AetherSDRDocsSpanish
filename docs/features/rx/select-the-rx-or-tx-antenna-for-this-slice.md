# Seleccionar la antena de RX o TX para este slice

El applet RX Controls le permite elegir qué puerto de antena utiliza el FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Úselo cuando tenga varias antenas conectadas y necesite enrutar un slice específico a un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos del propio radio. Confirme que sus antenas estén conectadas y reconocidas por el radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón de bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (de la A a la H) correspondiente al slice que desea cambiar.
3. **Para cambiar la antena de RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena de RX actual, p. ej., **ANT1**). Aparece un menú con todos los puertos de antena disponibles. Haga clic en el puerto deseado. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena de TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena de RX (también muestra la antena de TX actual, p. ej., **ANT1**). Aparece un menú con los puertos de antena compatibles con TX. Haga clic en el puerto deseado.

## Qué hace cada control

| Control                                   | Valor predeterminado | Valores válidos                                   |
|-------------------------------------------|----------------------|---------------------------------------------------|
| **ANT1** (antena de RX, etiqueta azul)    | ANT1                 | Puertos de antena de ant_list del radio           |
| **ANT1** (antena de TX, etiqueta roja)    | ANT1                 | Puertos compatibles con TX de ant_list del radio  |

## Consejos

- La etiqueta de la antena de RX se muestra en azul; la etiqueta de la antena de TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila de encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se excluyen del menú de antena de TX. Seguirán apareciendo en el menú de antena de RX.
- Cada slice tiene su propia asignación independiente de antena de RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- A partir de la versión v0.9.3, los botones de pestaña de slice y la insignia de slice utilizan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidores. Los colores no son configurables desde la página de controles de antena; se aplican a todo el applet.

## Comportamiento de las pestañas de slice

En la versión v0.9.5.1, la fila de pestañas de slice incorporó una gestión de ciclo de vida más robusta para corregir problemas observados durante reconexiones al radio (#2254).

- Cuando el radio reporta un número de slices diferente al que contiene la fila de pestañas actual, AetherSDR elimina todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura la insignia de slice estática. Este es también el estado que se muestra cuando el radio está desconectado.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea una sola vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados durante las reconexiones.

## Formato de almacenamiento de preajustes de filtro

A partir de la versión v0.9.5.1, los preajustes de filtro guardados mediante clic derecho en un botón **Filter width presets** pueden almacenar un ancho simple o un par de bordes de banda de paso específicos (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **ancho simple** se almacena como un entero único (p. ej., `2700`). Al aplicarse, el radio coloca la banda de paso de forma simétrica según el modo actual.
- Una entrada de **bordes lo:hi** se almacena como dos enteros separados por dos puntos (p. ej., `300:3000`). Al aplicarse, AetherSDR establece los bordes inferior y superior de la banda de paso exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes para un modo determinado. La clave de ajuste es `FilterPresets_<mode>` (p. ej., `FilterPresets_USB`). En el applet RX Controls se muestran hasta seis preajustes por modo.

Si una entrada guardada tiene un formato incorrecto o su borde superior no supera al borde inferior, AetherSDR omite esa entrada sin notificación al cargar los preajustes.

## Comportamiento del modo NT

NT es un modo digital añadido en la versión v0.9.3. Su comportamiento dentro del applet RX Controls coincide con el de otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Preajustes de filtro** — NT utiliza los mismos anchos de preajuste de filtro que DIGU y DIGL (100–2000 Hz).
- **Indicador de ancho de filtro** — El indicador de ancho de filtro deriva su valor del borde superior de la banda de paso, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Silenciador** — El botón **SQL** y el control deslizante del nivel de silenciador están desactivados en el modo NT. Si el silenciador estaba activo al cambiar al modo NT, AetherSDR lo desactiva automáticamente y lo restaura al cambiar a otro modo. Esto coincide con el comportamiento de DIGU y DIGL; el modo CW se gestiona de forma diferente porque el radio administra su estado de silenciador directamente.

## Resolución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de ant_list del radio. Verifique que el puerto esté configurado y reconocido en los ajustes del propio radio. AetherSDR no puede añadir puertos que el radio no haya reportado.
- **El menú de antena de TX no muestra un puerto que sí aparece en el menú de antena de RX** — Los puertos cuyos nombres comienzan con `RX` se excluyen intencionalmente del menú de antena de TX porque el radio los trata como exclusivos de recepción.
- **Ambas etiquetas aparecen atenuadas o no responden** — AetherSDR no está conectado al radio. Reconéctese mediante `Settings > Connect to Radio...`.
- **El botón SQL aparece atenuado después de cambiar al modo NT** — NT es un modo digital. AetherSDR desactiva el silenciador en todos los modos digitales (DIGU, DIGL, NT) porque el audio se enruta a través de DAX y el silenciador no tiene ningún efecto útil. Cambie a un modo no digital para volver a habilitar el silenciador.
- **La fila de pestañas de slice muestra pestañas incorrectas tras reconectar** — En versiones anteriores, la fila de pestañas se construía una sola vez y podía quedar desactualizada tras una reconexión. A partir de la versión v0.9.5.1, AetherSDR reconstruye la fila de pestañas cuando cambia el número de slices. Si la fila sigue apareciendo incorrecta, desconéctese y vuelva a conectarse mediante `Settings > Connect to Radio...`.
- **Un preajuste de filtro aplica una banda de paso diferente a la esperada** — Los preajustes guardados antes de la versión v0.9.5.1 se almacenan como anchos simples y siguen siendo válidos. Los preajustes guardados desde la versión v0.9.5.1 en adelante pueden almacenar bordes lo:hi exactos. Si un preajuste se comporta de forma inesperada, haga clic derecho en el botón de preajuste para sobrescribirlo con la banda de paso actual.

## Temas relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
