# Ensanchar o estrechar el filtro usando el atajo de modo correcto (todos los modos, incluyendo LSB/CWL/DIGL/RTTY)

Use el atajo de ensanchar/estrechar para recorrer los valores preestablecidos de anchura de filtro por modo — una pulsación ensancha el filtro, la otra lo estrecha. El atajo siempre aplica anchuras de filtro apropiadas para el modo del segmento actual, por lo que nunca obtendrá un filtro de anchura CW en SSB ni un filtro de anchura de radiodifusión en RTTY.

## Antes de empezar

- Debe haber una radio conectada.
- El applet de Controles de RX debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet de Controles de RX, haga clic en el **Combo Modo** y seleccione el modo que desea usar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de valores preestablecidos de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo apuntando a la izquierda (◀) junto al indicador de anchura de filtro para estrechar el filtro, o en el botón de triángulo apuntando a la derecha (▶) para ensancharlo.

Cada clic avanza por la lista de valores preestablecidos del modo. La anchura de filtro actual se muestra en el indicador **2.7K** (anchura de filtro).

## Qué hace cada control

| Control                          | Valor predeterminado | Comportamiento                                                                       |
|----------------------------------|----------------------|--------------------------------------------------------------------------------------|
| **Valores preestablecidos de anchura de filtro (◀ / ▶)** | Ver más abajo        | Recorre las anchuras de filtro por modo en orden descendente (◀) o ascendente (▶).    |
| **2.7K (anchura de filtro)**     | Dependiente del modo | Muestra el ancho de banda del filtro del segmento actual.                            |

## Valores preestablecidos de anchura de filtro por modo

| Modo   | Valores preestablecidos (Hz) |
|--------|----------------------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW      | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY    | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin valores preestablecidos de filtro (botones ocultos) |

## Relacionado

- [Seleccione un valor preestablecido de anchura de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambie de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet de Controles de RX

El applet de Controles de RX proporciona controles de recepción por segmento. Aparece cuando hace clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control                        | Tipo            | Valor predeterminado | Comportamiento |
|--------------------------------|-----------------|----------------------|----------------|
| **Pestañas de segmento (A..H)** | pestaña         | —                    | Selecciona el segmento al que está vinculado el applet RX; emite sliceActivationRequested. La fila se oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de segmento estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic del botón de segmento están protegidas contra manejadores de señal duplicados a través de reconexiones. |
| **Insignia de segmento**        | indicador       | A                  | Muestra la letra del segmento actualmente vinculado. Coloreada por identidad del segmento. |
| **🔓 / 🔒**                   | botón de alternancia | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el segmento; el segmento bloqueado ignora los cambios de frecuencia. El icono cambia entre un candado abierto y cerrado. |
| **ANT1 (antena RX)**           | cuadro combinado | ANT1               | Abre un menú que lista las antenas disponibles; al seleccionar establece slice->setRxAntenna. Se completa desde la ant_list de la radio. Etiqueta de color azul. |
| **ANT1 (antena TX)**           | cuadro combinado | ANT1               | Abre un menú que lista las antenas con capacidad TX; los puertos solo RX (prefijo 'RX') se filtran. Al seleccionar establece slice->setTxAntenna. Etiqueta de color rojo. |
| **2.7K (anchura de filtro)**   | indicador       | 2.7K               | Muestra la anchura de filtro actual en kHz. Se actualiza cuando se aplica un valor preestablecido de filtro. |
| **QSK**                        | indicador       | apagado (gris)     | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (insignia)**              | botón de alternancia | —               | Haga clic para establecer este segmento como el segmento TX (llama a slice->setTxSlice). |
| **Combo Modo**                 | cuadro combinado | USB                | Establece el modo del segmento; reconfigura los valores preestablecidos de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). Al seleccionar un modo de radio real, elimina la superposición del demodulador de software WFM si se estaba ejecutando en este segmento. La opción RADE requiere la bandera de compilación HAVE_RADE. |
| **WFM**                        | botón pulsador  | apagado            | Botón de alternancia para el demodulador FM por software a través de DAX IQ → Hi-Fi Cable. Cuando está activado, el botón brilla en verde; cuando está desactivado, se vuelve gris. Emite la señal wfmActivated con el ID del segmento. |
| **Etiqueta de frecuencia**     | indicador       | 0.000.000          | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. |
| **Edición de frecuencia**      | campo de texto   | —               | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y oculta el editor (v0.9.0, #1954). Usa FreqLineEdit con texto de sugerencia "MHz". Compatible con XVTR: acepta hasta 450 MHz cuando el segmento está en una antena XVTR. |
| **PASO**                       | cuadro de giro   | 100 Hz (índice 2)  | < / > o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged y stepSizeChangedByUser. La lista de pasos depende del modo del segmento. |
| **Valores preestablecidos de anchura de filtro** | botón pulsador | — | Haga clic para aplicar un valor preestablecido de anchura de filtro; haga clic derecho para guardar la anchura actual como valor preestablecido. Los botones se ocultan para los modos FM/NFM/DFM. El indicador de anchura (compartido con VfoWidget a través de RxApplet::formatFilterWidth) usa lógica consciente del modo para que los modos SSB/digitales muestren la anchura etiquetada correcta (#2197). El método stepFilterWidth(direction) recorre la lista de valores preestablecidos por modo para ensanchar/estrechar correctos según el modo (#2208). |
| **Widget de banda de paso del filtro** | asa de arrastre | — | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi). |
| **Modo de tono (FM)**          | cuadro combinado | Off                | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS**        | cuadro combinado | —               | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX. |
| **Desplazamiento (FM)**        | cuadro de giro   | 0.0 MHz            | Establece la frecuencia de desplazamiento del repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (desplazamiento hacia abajo)** | botón de alternancia | — | Establece la dirección del desplazamiento del repetidor a 'hacia abajo' (TX por debajo de RX). |
| **Simplex**                   | botón de alternancia | marcado          | Establece la dirección del desplazamiento del repetidor a simplex (TX = RX). |
| **+ (desplazamiento hacia arriba)** | botón de alternancia | — | Establece la dirección del desplazamiento del repetidor a 'hacia arriba' (TX por encima de RX). |
| **REV**                       | botón de alternancia | —               | Invierte el signo del desplazamiento TX para trabajar un par de repetidor inverso. |
| **🔊 / 🔇 (silencio)**       | botón pulsador  | 🔊 (sin silenciar) | Un solo clic silencia/restaura el sonido de este segmento (diferido por el intervalo de discriminación de clic de la plataforma). Doble clic silencia/restaura el sonido de todos los segmentos propios a través de la señal muteAllToggled. El icono cambia cuando la radio lo confirma a través de SliceModel::audioMuteChanged. Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. El clic simple se difiere por clickDiscriminationIntervalMs() (intervalo de doble clic predeterminado de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic simple. |
| **Ganancia AF**                | deslizador       | 70                 | Ajusta la ganancia de salida de audio del segmento; emite afGainChanged. Rango 0-100. |
| **Panorámica L / R**           | deslizador       | 50                 | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera — la posición neutra muestra un punto de marca central en la ranura. |
| **SQL**                       | botón de alternancia | —               | Activa el squelch en el nivel actual del deslizador. Deshabilitado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). |
| **Nivel de squelch**          | deslizador       | 20                 | Ajusta el umbral de squelch; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. |
| **Modo CAG**                  | cuadro combinado | Med                | Establece el modo CAG del segmento. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral CAG**                | deslizador       | 65                 | Establece el umbral CAG (o nivel CAG desactivado cuando el modo CAG es Off). La información sobre herramientas refleja qué valor se está ajustando e incluye una sugerencia sobre la calibración con clic derecho. |
| **RIT**                       | botón de alternancia | —               | Activa/desactiva la Sintonía Incremental de Recepción. |
| **RIT 0**                     | botón pulsador  | —               | Pone a cero el desplazamiento RIT. |
| **Desplazamiento RIT**        | cuadro de giro   | +0 Hz              | < / > o la rueda del ratón ajustan el desplazamiento RIT en pasos de 10 Hz. |
| **XIT**                       | botón de alternancia | —               | Activa/desactiva la Sintonía Incremental de Transmisión. |
| **XIT 0**                     | botón pulsador  | —               | Pone a cero el desplazamiento XIT. |
| **Desplazamiento XIT**        | cuadro de giro   | +0 Hz              | < / > o la rueda del ratón ajustan el desplazamiento XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se desactiva automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**

Al cambiar a cualquiera de estos modos, el squelch se apaga y el botón SQL y el deslizador se deshabilitan. Esto evita que el squelch bloquee señales FSK débiles e interrumpa la decodificación, particularmente en modos RTTY y digitales donde el squelch recortaría los caracteres FSK (#2504).

## Demodulador de software WFM

El botón **WFM** proporciona un demodulador FM por software para recibir señales FM de banda ancha (radiodifusión). Esto utiliza la transmisión DAX IQ a un dispositivo Hi-Fi Cable.

- Haga clic en el botón **WFM** para activar o desactivar el demodulador WFM para el segmento actual.
- Cuando está activado, el botón brilla en verde. Cuando está desactivado, aparece gris.
- Seleccionar cualquier otro modo del **Combo Modo** desactiva automáticamente el demodulador WFM para ese segmento.
- El estado del botón se sincroniza a través de reconexiones — si WFM estaba activo en un segmento antes de la desconexión, se volverá a activar cuando el segmento se restaure.

## Calibrar CAG-T contra el piso de ruido

El deslizador de **Umbral CAG** admite un menú contextual con clic derecho para la calibración del piso de ruido.

1. Haga clic derecho en el deslizador **Umbral CAG**.
2. Seleccione **Calibrar CAG-T contra el piso de ruido…** del menú contextual.
3. Aparece un panel de calibración — siga las instrucciones en pantalla para medir el piso de ruido actual y ajustar el umbral CAG-T automáticamente.

La información sobre herramientas en el deslizador **Umbral CAG** indica qué valor se está ajustando (Umbral CAG o Nivel CAG Desactivado) y anuncia la función de calibración con clic derecho.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (Detección de Radar) está disponible (requiere la bandera de compilación HAVE_RADE), seleccionar RADE del Combo Modo activa el subsistema de detección de radar para el segmento actual. Al salir del modo RADE a través del combo modo, el applet emite radeActivated(false) solo si el segmento estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un segmento que no es RADE. El modo RADE es solo del lado del cliente — la radio devuelve el modo real (DIGL/DIGU) inmediatamente después
