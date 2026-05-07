# Aplicar un ancho de filtro predefinido desde el panel VFO

Los botones de preselección de filtro le permiten cambiar el ancho del filtro de recepción de una franja con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes — por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO de la franja objetivo debe estar abierto y expandido. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte para expandirlo primero.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectro de la franja que desea ajustar. El panel VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de preselección de filtro que corresponda al ancho de banda que desea. La radio aplica inmediatamente ese ancho de filtro a la franja.

Para guardar el ancho de filtro actual en una ranura de preselección:

1. Ajuste el filtro al ancho de banda que desea guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic con el botón derecho en la ranura del botón de preselección que desea sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                   |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Botones de preselección de filtro (pestaña Mode) | Cada botón aplica una preselección de ancho de filtro guardada a la franja. Haga clic izquierdo para aplicar; clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro inferior y superior personalizados se pueden almacenar por ranura mediante clic derecho. | —                                                                                                                     |
| Etiqueta de ancho de filtro       | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Usa RxApplet::formatFilterWidth como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |                                                                                                                       |
| Botón ADSP (pestaña DSP)          | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8).                                                                      | Con estilo similar a un conmutador DSP del lado de la radio pero sin posibilidad de marcado. Al hacer clic, abre y enfoca el cuadro de diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP)   | Activa o desactiva Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8).                                                                                                                                               | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes de menú/cadena para la tira.                 |

## Cambios en la pestaña DSP en v0.9.8

La pestaña **DSP** ahora solo muestra los botones de reducción de ruido del lado de la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2**
- **RN2**
- **BNR**
- **NR4**
- **MNR**
- **DFNR**

Estos módulos DSP del lado del cliente ahora se acceden a través del menú superpuesto del espectro y del applet AetherDSP. Actívelos o desactívelos desde allí en lugar de desde el panel VFO.

Los botones que permanecen en la pestaña DSP están organizados en una cuadrícula de cuatro columnas, seguida por los botones lanzadores ADSP y AetherVoice:

| Posición | Botón |
|---|---|
| Fila 1, col 1 | NR |
| Fila 1, col 2 | NB |
| Fila 1, col 3 | ANF |
| Fila 1, col 4 | APF (visible solo en modo CW) |
| Fila 2, col 1 | NRL |
| Fila 2, col 2 | NRS |
| Fila 2, col 3 | RNN |
| Fila 2, col 4 | NRF |
| Fila 3, col 1 | ANFL |
| Fila 3, col 2 | ANFT |
| Fila 4, col 1 | ADSP |
| Fila 4, cols 2–3 | AetherVoice |

Una fila compartida de **control deslizante de nivel DSP** aparece debajo de la cuadrícula de botones. El control deslizante se reorienta automáticamente al botón DSP con nivel que se activó más recientemente. En v0.9.8, cuando llega un cambio de estado de nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR activado al inicio), el control deslizante aparece inmediatamente sin necesidad de reactivarlo manualmente. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del control deslizante muestra el nivel actual numéricamente. Cuando no hay ningún algoritmo DSP con nivel activo — o cuando solo están activados RNN, ANFT o APF — la fila del control deslizante está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo correspondiente de reducción de ruido o filtrado del lado de la radio para esta franja. APF es visible solo en modo CW. | desactivado | — |
| Control deslizante de nivel DSP (pestaña DSP) | Establece el nivel de procesamiento para el algoritmo DSP con nivel activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP con nivel activado. Oculto (atenuado) cuando no hay ningún algoritmo con nivel activo. | — | — |
| Botón ADSP (pestaña DSP) | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador sin posibilidad de marcado. | — | — |
| Botón AetherVoice (pestaña DSP) | Abre Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Botón pulsador sin posibilidad de marcado. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. | — | — |

## Consejos

- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda activo en todo momento. Haga clic directamente en ella para recorrer los botones de preselección sin cambiar a la pestaña Mode primero.
- Las ranuras de preselección se comparten entre todas las franjas y modos. Sobrescribir una ranura afecta a cada franja que la use.
- Las líneas de borde de filtro en el panadapter del espectro reflejan el ancho de filtro activo. Si las líneas están ocultas, actívelas con el botón Filter edges en el panel VFO. Consulte [Ocultar o mostrar líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md).
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic con el botón derecho en la superposición del espectro o abra el applet AetherDSP.
- El control deslizante de nivel DSP ahora aparece inmediatamente al inicio para cualquier DSP con nivel que se haya guardado en el perfil de la radio, sin necesidad de activarlo manualmente.

## Relacionados

- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Cambiar modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Ocultar o mostrar líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Descripción general del panel VFO](overview.md)
