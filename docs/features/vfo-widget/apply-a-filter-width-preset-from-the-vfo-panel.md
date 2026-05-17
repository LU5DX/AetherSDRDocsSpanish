# Aplicar un ancho de filtro predefinido desde el panel VFO

Los botones de preselección de filtro le permiten cambiar el ancho del filtro de recepción para un segmento (slice) con un solo clic. Úselos para moverse rápidamente entre anchos de banda comunes —por ejemplo, entre un filtro SSB ancho de 3 kHz y un filtro CW estrecho de 500 Hz— sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El panel VFO del segmento (slice) deseado debe estar abierto y expandido. Si está colapsado a una tira solo de frecuencia, haga clic en cualquier parte de él para expandirlo primero.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento (slice) que desea ajustar. El panel VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de preselección de filtro que corresponda al ancho de banda que desee. La radio aplica inmediatamente ese ancho de filtro al segmento.

Para guardar el ancho de filtro actual en una ranura de preselección:

1. Ajuste el filtro al ancho de banda que desee guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic derecho en la ranura del botón de preselección que desee sobrescribir.
3. El ancho de filtro actual se guarda en esa ranura.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                                                                       | Valor predeterminado |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Botones de preselección de filtro (pestaña Mode) | Cada botón aplica una preselección de ancho de filtro guardada al segmento. Haga clic izquierdo para aplicar; haga clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro bajo y alto personalizados se pueden almacenar por ranura mediante clic derecho. | —                    |
| Etiqueta de ancho de filtro      | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). | —                    |
| Botón ADSP (pestaña DSP)         | Abre el cuadro de diálogo Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8).                                                                                                                               | Estilizado como un conmutador de DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP)  | Activa la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8).                                                                                                                                             | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

## Cambios en la pestaña DSP en v0.9.8

La pestaña **DSP** ahora muestra solo los botones de reducción de ruido del lado de la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel VFO:

- **NR2**
- **RN2**
- **BNR**
- **NR4**
- **MNR**
- **DFNR**

Estos módulos DSP del lado del cliente ahora se acceden a través del menú superpuesto del espectro y el applet AetherDSP. Actívelos allí en lugar de desde el panel VFO.

Los botones que quedan en la pestaña DSP están organizados en una cuadrícula de cuatro columnas, seguida de los botones de lanzamiento ADSP y AetherVoice:

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

Una fila compartida de **control deslizante de nivel DSP** aparece debajo de la cuadrícula de botones. El control deslizante se reorienta automáticamente al botón DSP con nivel que se encendió más recientemente. En v0.9.8, cuando llega un cambio de estado de nivel DSP desde la radio (por ejemplo, cuando el perfil guardado de la radio tiene NR activado al inicio), el control deslizante aparece inmediatamente sin necesidad de re-activación manual. Su etiqueta muestra el nombre del objetivo actual (por ejemplo, **NR** o **NB**), y el valor a la derecha del control deslizante muestra el nivel actual numéricamente. Cuando ningún algoritmo DSP con nivel está activo —o solo RNN, ANFT o APF está encendido— la fila del control deslizante está presente en el diseño pero visualmente atenuada. Hacer clic en ella mientras está atenuada no tiene efecto.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botones NR / NB / ANF / APF / NRL / NRS / RNN / NRF / ANFL / ANFT (pestaña DSP) | Activa el algoritmo de reducción de ruido o filtrado correspondiente del lado de la radio para este segmento (slice). APF es visible solo en modo CW. | desactivado | — |
| Control deslizante de nivel DSP (pestaña DSP) | Establece el nivel de procesamiento para el algoritmo DSP con nivel activado más recientemente. La etiqueta a la izquierda identifica el objetivo actual. Se activa automáticamente al inicio si el perfil guardado de la radio tiene un DSP con nivel activado. Oculto (atenuado) cuando ningún algoritmo con nivel está activo. | — | — |
| Botón ADSP (pestaña DSP) | Abre el cuadro de diálogo Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Botón pulsador no marcable. | — | — |
| Botón AetherVoice (pestaña DSP) | Abre la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX. Botón pulsador no marcable. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. | — | — |

## Cambios en el comportamiento del squelch (v26.5.1)

El control de squelch en la pestaña **Audio** ahora está deshabilitado para modos RTTY y digitales, además del modo CW. Esto evita que el squelch bloquee señales FSK débiles que se envían a decodificadores externos a través de DAX (#2504).

Cuando cambia un segmento a modo DIGU, DIGL o RTTY:

- El botón y el control deslizante de Squelch se deshabilitan.
- Si el squelch estaba activo, se apaga automáticamente. El estado anterior se guarda internamente y se restaura si vuelve a un modo de voz.

Esto coincide con el comportamiento existente para el modo CW, donde la radio bloquea el squelch activado en un nivel fijo y rechaza los cambios del usuario.

## Cambios en la selección de antena (v26.5.2.1)

Los botones **RX antenna** y **TX antenna** ahora utilizan menús mejorados:

- El menú de antena RX utiliza `rxAntennaList()` del segmento cuando está disponible, recurriendo a la lista global de antenas para compatibilidad heredada.
- El menú de antena TX filtra inteligentemente los puertos de antena solo de RX verificando prefijos "RX", prefijos "ANT", prefijos "TX" o "XVTR" como tokens de respaldo.
- Los elementos del menú ahora almacenan el identificador de la antena como datos, permitiendo la selección por nombre interno en lugar de etiqueta mostrada.
- Cada elemento del menú incluye una información sobre herramientas y una sugerencia de estado que muestran el identificador de la antena.

### Mejoras en la entrada de frecuencia (v26.5.2.1)

La lógica de entrada de frecuencia se ha actualizado para manejar mejor las bandas de transverter (XVTR):

- La frecuencia máxima de XVTR se ha aumentado de 450 MHz a 50000 MHz para admitir bandas de microondas.
- El análisis de conveniencia de "tres dígitos de banda" (insertar un decimal después del tercer dígito para enteros simples como 1446 → 144.6 MHz) ahora solo se activa cuando la frecuencia del segmento está entre 100 MHz y 999 MHz. Para bandas de 23 cm y microondas (por encima de 1000 MHz), un entero simple como 1296 se trata directamente como 1296 MHz.

### Representación de la etiqueta del segmento (v26.5.2.1)

La etiqueta de letra del segmento ahora se renderiza como Qt Rich Text (`Qt::RichText`), corrigiendo un problema donde ciertas letras de segmento se mostraban incorrectamente (#2606). El estilo de la etiqueta sigue siendo el mismo.

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botón RX antenna | Abre un menú de selección de antena para la antena receptora de este segmento. Utiliza la lista de antenas específica del segmento cuando está disponible. Los elementos del menú muestran información sobre herramientas y sugerencia de estado. | — | — |
| Botón TX antenna | Abre un menú de selección de antena para la antena transmisora de este segmento. Filtra automáticamente los puertos de antena solo de RX. Los elementos del menú muestran información sobre herramientas y sugerencia de estado. | — | — |

## Consejos

- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda activo en todo momento. Haga clic directamente en ella para recorrer los botones de preselección sin cambiar a la pestaña Mode primero.
- Las ranuras de preselección se comparten entre todos los segmentos y modos. Sobrescribir una ranura afecta a cada segmento que la utilice.
- Las líneas de borde de filtro en el panadaptador del espectro reflejan el ancho de filtro activo. Si las líneas están ocultas, actívelas con el botón Filter edges en el panel VFO. Consulte [Ocultar o mostrar líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md).
- Para acceder a NR2, RN2, BNR, NR4, MNR o DFNR, haga clic derecho en la superposición del espectro o abra el applet AetherDSP.
- El control deslizante de nivel DSP ahora aparece inmediatamente al inicio para cualquier DSP con nivel que se haya guardado en el perfil de la radio, sin necesidad de activación manual.
- El menú de antena RX ahora utiliza la lista de antenas específica del segmento cuando está disponible, que puede diferir de la lista global de antenas en configuraciones de múltiples radios.
- Al ingresar una frecuencia en una banda VHF/UHF (100-999 MHz), los enteros simples de 4 o más dígitos tendrán un decimal insertado después del tercer dígito (por ejemplo, 14696 → 146.96 MHz). Para bandas de microondas por encima de 1000 MHz, los enteros simples se tratan directamente como MHz.

## Relacionados

- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Cambiar modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Ocultar o mostrar líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Descripción general del panel VFO](overview.md)
