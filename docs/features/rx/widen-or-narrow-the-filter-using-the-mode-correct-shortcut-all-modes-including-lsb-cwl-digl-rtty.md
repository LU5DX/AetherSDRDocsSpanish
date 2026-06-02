# Ampliar o reducir el filtro mediante el acceso directo de modo correcto (todos los modos, incluidos LSB/CWL/DIGL/RTTY)

Use el acceso directo de ampliar/reducir para recorrer los preajustes de ancho de filtro por modo: una pulsación amplía el filtro, la otra lo reduce. El acceso directo siempre aplica anchos de filtro apropiados para el modo actual del slice, por lo que nunca obtendrá un filtro de ancho CW en SSB ni un filtro de ancho de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet RX Controls debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet RX Controls, haga clic en el cuadro combinado **Mode** y seleccione el modo que desea utilizar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de preajustes de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo que apunta a la izquierda (◀) junto al indicador de ancho de filtro para reducir el filtro, o en el botón de triángulo que apunta a la derecha (▶) para ampliarlo.

Cada clic avanza por la lista de preajustes del modo. El ancho de filtro actual se muestra en el indicador de **2.7K** (ancho de filtro).

## Función de cada control

| Control                          | Valor predeterminado | Comportamiento                                                                       |
|----------------------------------|----------------------|--------------------------------------------------------------------------------------|
| **Preajustes de ancho de filtro (◀ / ▶)** | Ver más abajo        | Recorre los anchos de filtro por modo en orden descendente (◀) o ascendente (▶). |
| **2.7K (ancho de filtro)**       | Depende del modo     | Muestra el ancho de banda del filtro del slice actual.                              |

## Preajustes de ancho de filtro por modo

| Modo   | Preajustes (Hz) |
|--------|-----------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW      | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY    | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin preajustes de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet RX Controls

El applet RX Controls proporciona controles de recepción por slice. Aparece al hacer clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|----------------------|----------------|
| **Pestañas de slice (A..H)** | pestaña | — | Selecciona a qué slice está vinculado el applet RX; emite sliceActivationRequested. La fila se oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic del botón de slice están protegidas contra manejadores de señal duplicados entre reconexiones. |
| **Insignia de slice** | indicador | A | Muestra la letra del slice actualmente vinculado. Coloreada según la identidad del slice. |
| **🔓 / 🔒** | botón_de_alternancia | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia. El icono cambia entre candado abierto y cerrado. |
| **ANT1 (antena RX)** | cuadro_combinado | ANT1 | Abre un menú que lista las antenas disponibles; al seleccionar, establece slice->setRxAntenna. Se completa desde la ant_list de la radio. Etiqueta de color azul. |
| **ANT1 (antena TX)** | cuadro_combinado | ANT1 | Abre un menú que lista las antenas con capacidad TX; los puertos solo RX (prefijo 'RX') se filtran. Al seleccionar, establece slice->setTxAntenna. Etiqueta de color rojo. |
| **2.7K (ancho de filtro)** | indicador | 2.7K | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un preajuste de filtro. |
| **QSK** | indicador | apagado (gris) | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (insignia)** | botón_de_alternancia | — | Haga clic para establecer este slice como el slice TX (llama a slice->setTxSlice). |
| **Cuadro combinado Mode** | cuadro_combinado | USB | Establece el modo del slice; reconfigura los preajustes de filtro y paso para el nuevo modo. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). La opción RADE requiere la marca de compilación HAVE_RADE. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. |
| **Campo de edición de frecuencia** | campo_de_texto | — | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite autoescalado de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor (v0.9.0, #1954). Compatible con XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR. |
| **STEP** | cuadro_giratorio | 100 Hz (índice 2) | < / > o la rueda del ratón recorren los tamaños de paso por modo; emite stepSizeChanged. La lista de pasos depende del modo del slice. |
| **Preajustes de ancho de filtro** | botón_de_pulsación | — | Haga clic para aplicar un ancho de filtro preajustado; haga clic derecho para guardar el ancho actual como preajuste. Los botones se ocultan para los modos FM/NFM/DFM. La lectura del ancho (compartida con VfoWidget mediante RxApplet::formatFilterWidth) utiliza lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de preajustes por modo para ampliar/reducir correctos según el modo (#2208). |
| **Widget de banda pasante del filtro** | controlador_de_arrastre | — | Arrastre los bordes lo/hi para ajustar la banda pasante del filtro; emite filterChanged (lo, hi). |
| **Modo de tono (FM)** | cuadro_combinado | Off | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro_combinado | — | Selecciona la frecuencia de tono CTCSS enviada con la transmisión. 41 tonos estándar EIA/TIA-603 (67,0 Hz a 254,1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX. |
| **Desplazamiento (FM)** | cuadro_giratorio | 0.0 MHz | Establece la frecuencia de desplazamiento del repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (desplazamiento hacia abajo)** | botón_de_alternancia | — | Establece la dirección del desplazamiento del repetidor como 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón_de_alternancia | marcado | Establece la dirección del desplazamiento del repetidor como simplex (TX = RX). |
| **+ (desplazamiento hacia arriba)** | botón_de_alternancia | — | Establece la dirección del desplazamiento del repetidor como 'hacia arriba' (TX por encima de RX). |
| **REV** | botón_de_alternancia | — | Invierte el signo del desplazamiento TX para trabajar un par de repetidores invertido. |
| **🔊 / 🔇 (silenciar)** | botón_de_pulsación | 🔊 (sin silenciar) | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clic de la plataforma). Doble clic silencia/activa el sonido de todos los slices propietarios mediante la señal muteAllToggled. El icono cambia cuando la radio lo confirma mediante SliceModel::audioMuteChanged. Según la Política de Ajustes Autoritativos de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. El clic único se difiere por clickDiscriminationIntervalMs() (intervalo de doble clic predeterminado de la plataforma, ~400 ms) para que un doble clic pueda anularlo. El manejador de doble clic está en eventFilter y cancela el temporizador de clic único. |
| **Ganancia AF** | deslizador | 70 | Ajusta la ganancia de salida de audio del slice; emite afGainChanged. Rango 0-100. |
| **Panorámica L / R** | deslizador | 50 | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). El relleno del deslizador se ancla desde el centro hacia afuera: la posición neutra muestra un punto de marca central en la ranura. |
| **SQL** | botón_de_alternancia | — | Activa el silenciador en el nivel actual del deslizador. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador recortaría los caracteres FSK (#2504). |
| **Nivel de silenciador** | deslizador | 20 | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Deshabilitado en modos RTTY y digitales. |
| **Modo AGC** | cuadro_combinado | Med | Establece el modo AGC del slice. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral AGC** | deslizador | 65 | Establece el umbral AGC (o el nivel AGC desactivado cuando el modo AGC es Off). La información sobre herramientas refleja qué valor se está ajustando. |
| **RIT** | botón_de_alternancia | — | Activa/desactiva la sintonización incremental de recepción. |
| **RIT 0** | botón_de_pulsación | — | Pone a cero el desplazamiento RIT. |
| **Desplazamiento RIT** | cuadro_giratorio | +0 Hz | < / > o la rueda del ratón ajustan el desplazamiento RIT en pasos de 10 Hz. |
| **XIT** | botón_de_alternancia | — | Activa/desactiva la sintonización incremental de transmisión. |
| **XIT 0** | botón_de_pulsación | — | Pone a cero el desplazamiento XIT. |
| **Desplazamiento XIT** | cuadro_giratorio | +0 Hz | < / > o la rueda del ratón ajustan el desplazamiento XIT en pasos de 10 Hz. |

## Comportamiento del silenciador en modos digitales y RTTY

El silenciador se desactiva automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**

Al cambiar a cualquiera de estos modos, el silenciador se apaga y el botón y deslizador SQL se deshabilitan. Esto evita que el silenciador bloquee señales FSK débiles e interrumpa la decodificación, particularmente en modos RTTY y digitales donde el silenciador recortaría los caracteres FSK (#2504).

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (Detección de Radar) está disponible (requiere la marca de compilación HAVE_RADE), al seleccionar RADE del cuadro combinado Mode se activa el subsistema de detección de radar para el slice actual. Al salir del modo RADE mediante el cuadro combinado de modo, el applet emite radeActivated(false) solo si el slice estaba realmente en RADE (#2376), evitando señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE. El modo RADE es solo del lado del cliente: la radio devuelve el modo real (DIGL/DIGU) inmediatamente después de configurar RADE, por lo que el modo() del slice nunca será "RADE" después de que la radio responda.

## Comportamiento del botón de silencio

El botón **🔊 / 🔇 (silenciar)** utiliza un botón_de_pulsación (no marcable) con discriminación de clic:

- **Clic único**: Activa/desactiva el silencio solo para este slice. La acción se difiere por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla.
- **Doble clic**: Activa/desactiva el silencio para todos los slices propietarios mediante la señal `muteAllToggled`. El segundo clic cancela el temporizador de clic único.
- El icono (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio mediante `SliceModel::audioMuteChanged`, asegurando que el estado mostrado coincida con el estado real de la radio.
- El estado de silencio no se guarda ni restaura al reconectar: la radio es siempre la fuente de verdad.

## Soporte de temas

El applet RX Controls se integra con el sistema de temas para una apariencia visual coherente:

- Los botones de **Preajustes de ancho de filtro** utilizan estilos tokenizados mediante `ThemeManager::resolve()`, lo que permite que se re-tematicen junto con el resto de la interfaz de usuario. Los estilos hacen referencia a tokens de tema como `{{color.background.1}}`, `{{color.background.2}}` y `{{color.text.primary}}`.
- El deslizador de **Panorámica L / R** utiliza `CenterMarkSlider`, cuyo relleno se ancla desde el centro hacia afuera. La ranura del deslizador se pinta con colores conscientes del tema (`color.background.1` para la ranura, `color.accent` para el relleno). Un punto de marca central proporciona un punto de referencia visual de posición neutra.
- El botón **TX (insignia)** utiliza estilos tokenizados mediante `ThemeManager::applyStyleSheet()`, haciendo referencia a `{{color.background.1}}` para los estados normal/flotante y `{{color.accent}}` para el estado presionado.
