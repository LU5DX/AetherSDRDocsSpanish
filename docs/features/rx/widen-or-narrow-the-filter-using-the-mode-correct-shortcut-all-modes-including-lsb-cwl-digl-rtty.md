# Ampliar o estrechar el filtro usando el atajo corregido por modo (todos los modos, incluyendo LSB/CWL/DIGL/RTTY)

Use el atajo de ampliar/estrechar para recorrer los valores predefinidos de ancho de filtro por modo: una pulsación amplía el filtro, la otra lo estrecha. El atajo siempre aplica anchos de filtro apropiados para el modo del segmento actual, por lo que nunca obtendrá un filtro de ancho CW en SSB ni un filtro de ancho de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet de controles de RX debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet de controles de RX, haga clic en el **combo de modo** y seleccione el modo que desea utilizar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de valores predefinidos de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo apuntando a la izquierda (◀) junto al indicador de ancho de filtro para estrechar el filtro, o en el botón de triángulo apuntando a la derecha (▶) para ampliarlo.

Cada clic avanza por la lista de valores predefinidos del modo. El ancho de filtro actual se muestra en el indicador **2.7K** (ancho de filtro).

## Qué hace cada control

| Control                          | Valor predeterminado | Comportamiento                                                                       |
|----------------------------------|----------------------|--------------------------------------------------------------------------------------|
| **Valores predefinidos de ancho de filtro (◀ / ▶)** | Ver más abajo        | Recorre los anchos de filtro por modo en orden descendente (◀) o ascendente (▶). |
| **2.7K (ancho de filtro)**       | Depende del modo     | Muestra el ancho de banda del filtro del segmento actual.                             |

## Valores predefinidos de ancho de filtro por modo

| Modo | Valores predefinidos (Hz) |
|------|---------------------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400, 500, 600 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin valores predefinidos de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un valor predefinido de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet de controles de RX

El applet de controles de RX proporciona controles de recepción por segmento. Aparece al hacer clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|----------------------|----------------|
| **Pestañas de segmento (A..H)** | pestaña | — | Selecciona a qué segmento está vinculado el applet de RX; emite sliceActivationRequested. Fila oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de segmento estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic del botón de segmento están protegidas contra manejadores de señal duplicados en reconexiones. |
| **Insignia de segmento** | indicador | A | Muestra la letra del segmento actualmente vinculado. Coloreada según la identidad del segmento. |
| **🔓 / 🔒** | botón de alternancia | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el segmento; el segmento bloqueado ignora los cambios de frecuencia. El icono cambia entre candado abierto y cerrado. |
| **ANT1 (antena RX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas disponibles; al seleccionar, establece slice->setRxAntenna. Se completa con la lista de antenas de la radio y los tokens de antena virtual de KiwiSDR. Etiqueta de color azul. Cuando se asigna un perfil KiwiSDR al segmento seleccionado, el token de antena virtual correspondiente aparece marcado en el menú. Seleccionar una antena virtual KiwiSDR emite kiwiRxAntennaSelected(sliceId, profileId); seleccionar una antena de radio emite flexRxAntennaSelected(sliceId) y luego establece la antena del segmento. |
| **ANT1 (antena TX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas con capacidad TX; los puertos solo RX (prefijo 'RX') se filtran. Al seleccionar, establece slice->setTxAntenna. Etiqueta de color rojo. |
| **2.7K (ancho de filtro)** | indicador | 2.7K | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un valor predefinido de filtro. |
| **QSK** | indicador | apagado (gris) | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (insignia)** | botón de alternancia | — | Haga clic para establecer este segmento como el segmento TX (llama a slice->setTxSlice). |
| **Combo de modo** | cuadro combinado | USB | Establece el modo del segmento; reconfigura los valores predefinidos de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). Seleccionar un modo de radio real elimina la superposición de demodulación por software WFM si estaba activa en este segmento. La opción RADE requiere la bandera de compilación HAVE_RADE. |
| **WFM** | botón pulsador | apagado | Botón de alternancia para el demodulador de FM por software a través de DAX IQ → Hi-Fi Cable. Cuando está habilitado, el botón brilla en verde; cuando está deshabilitado, se vuelve gris. Emite la señal wfmActivated con el ID del segmento. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. Los eventos de cambio de valor de accesibilidad se publican en la etiqueta cuando cambia el texto de frecuencia, lo que permite que la tecnología de asistencia anuncie las actualizaciones. |
| **Edición de frecuencia** | campo de texto | — | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite escala automática de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). Usa FreqLineEdit con texto de sugerencia "MHz". Consciente de XVTR: acepta hasta 450 MHz cuando el segmento está en una antena XVTR. |
| **STEP (PASO)** | cuadro de número | 100 Hz (índice 2) | < / > o rueda del ratón recorre los tamaños de paso por modo; emite stepSizeChanged y stepSizeChangedByUser. La lista de pasos depende del modo del segmento. |
| **Valores predefinidos de ancho de filtro** | botón pulsador | — | Haga clic para aplicar un ancho de filtro predefinido; haga clic derecho para guardar el ancho actual como un valor predefinido. Botones ocultos para los modos FM/NFM/DFM. La lectura del ancho (compartida con VfoWidget a través de RxApplet::formatFilterWidth) utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de valores predefinidos por modo para ampliar/estrechar corregido por modo (#2208). |
| **Widget de banda de paso del filtro** | control de arrastre | — | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). |
| **Modo de tono (FM)** | cuadro combinado | Apagado | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro combinado | — | Selecciona la frecuencia del tono CTCSS enviada con la transmisión. 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX. |
| **Desplazamiento (FM)** | cuadro de número | 0.0 MHz | Establece la frecuencia de desplazamiento del repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (desplazamiento hacia abajo)** | botón de alternancia | — | Establece la dirección del desplazamiento del repetidor a 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón de alternancia | marcado | Establece la dirección del desplazamiento del repetidor a simplex (TX = RX). |
| **+ (desplazamiento hacia arriba)** | botón de alternancia | — | Establece la dirección del desplazamiento del repetidor a 'hacia arriba' (TX por encima de RX). |
| **REV** | botón de alternancia | — | Invierte el signo del desplazamiento TX para trabajar un par de repetidores inverso. |
| **🔊 / 🔇 (silencio)** | botón pulsador | 🔊 (sin silenciar) | Un solo clic silencia/activa el sonido de este segmento (diferido por el intervalo de discriminación de clic de la plataforma). Doble clic silencia/activa el sonido de todos los segmentos propietarios a través de la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. Según la Política de Configuración Autoritaria de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (intervalo predeterminado de doble clic de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic único. |
| **Ganancia AF** | deslizador | 70 | Ajusta la ganancia de salida de audio del segmento; emite afGainChanged. Rango 0-100. |
| **Panorámica L / R** | deslizador | 50 | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). El doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera — la posición neutral muestra un punto de marca central en la ranura. |
| **SQL** | botón de alternancia | — | Activa el squelch en el nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). |
| **Nivel de squelch** | deslizador | 20 | Ajusta el umbral de squelch; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. |
| **Modo AGC** | cuadro combinado | Med | Establece el modo AGC del segmento. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral AGC** | deslizador | 65 | Establece el umbral AGC (o el nivel de AGC apagado cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando e incluye una sugerencia sobre la calibración con clic derecho. |
| **RIT** | botón de alternancia | — | Activa/desactiva la sintonización incremental de recepción. |
| **RIT 0** | botón pulsador | — | Pone a cero el desplazamiento RIT. |
| **Desplazamiento RIT** | cuadro de número | +0 Hz | < / > o rueda del ratón ajusta el desplazamiento RIT en pasos de 10 Hz. |
| **XIT** | botón de alternancia | — | Activa/desactiva la sintonización incremental de transmisión. |
| **XIT 0** | botón pulsador | — | Pone a cero el desplazamiento XIT. |
| **Desplazamiento XIT** | cuadro de número | +0 Hz | < / > o rueda del ratón ajusta el desplazamiento XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se desactiva automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**

Al cambiar a cualquiera de estos modos, el squelch se apaga y el botón SQL y el deslizador se deshabilitan. Esto evita que el squelch bloquee las señales FSK débiles y rompa la decodificación, particularmente en modos RTTY y digitales donde el squelch recortaría los caracteres FSK (#2504).

## Demodulador de software WFM

El botón **WFM** proporciona un demodulador de FM por software para recibir señales FM de banda ancha (radiodifusión). Esto utiliza la transmisión DAX IQ a un dispositivo Hi-Fi Cable.

- Haga clic en el botón **WFM** para activar o desactivar el demodulador WFM para el segmento actual.
- Cuando está activado, el botón brilla en verde. Cuando está desactivado, aparece gris.
- Seleccionar cualquier otro modo del **combo de modo** desactiva automáticamente el demodulador WFM para ese segmento.
- El estado del botón se sincroniza en las reconexiones — si WFM estaba activo en un segmento antes de la desconexión, se volverá a activar cuando se restaure el segmento.

## Calibrar AGC-T contra el piso de ruido

El deslizador **umbral AGC** admite un menú contextual con clic derecho para la calibración del piso de ruido.

1. Haga clic derecho en el deslizador **umbral AGC**.
2. Seleccione **Calibrar AGC-T contra el piso de ruido…** en el menú contextual.
3. Aparece un panel de calibración — siga las instrucciones en pantalla para medir el piso de ruido actual y ajustar el umbral AGC-T automáticamente.

La información sobre herramientas en el deslizador **umbral AGC** indica qué valor se está ajustando (Umbral AGC o Nivel AGC Apagado) y anuncia la función de calibración con clic derecho.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (detección de radar) está disponible (requiere la bandera de compilación HAVE_RADE), seleccionar RADE del combo de modo activa el subsistema de detección de radar para el segmento actual. Al salir del modo RADE a través del combo de modo, el applet emite radeActivated(false) solo si el segmento estaba realmente en RADE (#2376), evitando señales de desactiv
