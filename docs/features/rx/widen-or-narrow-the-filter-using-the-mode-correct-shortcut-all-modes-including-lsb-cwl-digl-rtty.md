# Ampliar o reducir el filtro usando el atajo correcto para el modo (todos los modos, incluidos LSB/CWL/DIGL/RTTY)

Use el atajo de ampliar/reducir para recorrer los valores preestablecidos de ancho de filtro por modo: una pulsación amplía el filtro, la otra lo reduce. El atajo siempre aplica los anchos de filtro apropiados para el modo del segmento activo, por lo que nunca obtendrá un filtro de ancho CW en SSB ni un filtro de ancho de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet RX Controls debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet RX Controls, haga clic en el **combo Mode** y seleccione el modo que desea usar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de valores preestablecidos de filtro y los tamaños de paso se actualizarán para ese modo.
2. Haga clic en el botón de triángulo que apunta a la izquierda (◀) junto al indicador de ancho de filtro para reducir el filtro, o en el botón de triángulo que apunta a la derecha (▶) para ampliarlo.

Cada clic avanza por la lista de valores preestablecidos del modo. El ancho de filtro actual se muestra en el indicador **2.7K** (ancho de filtro).

## Qué hace cada control

| Control                          | Valor predeterminado | Comportamiento                                                                       |
|----------------------------------|----------------------|--------------------------------------------------------------------------------------|
| **Valores preestablecidos de ancho de filtro (◀ / ▶)** | Ver más abajo        | Recorre los anchos de filtro por modo en orden descendente (◀) o ascendente (▶).      |
| **2.7K (ancho de filtro)**       | Depende del modo     | Muestra el ancho de banda del filtro del segmento actual.                            |

## Valores preestablecidos de ancho de filtro por modo

| Modo | Valores preestablecidos (Hz) |
|------|-----------------------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin valores preestablecidos de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un valor preestablecido de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet RX Controls

El applet RX Controls proporciona controles de recepción por segmento. Aparece cuando hace clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|----------------------|----------------|
| **Pestañas de segmento (A..H)** | pestaña | — | Selecciona a qué segmento está vinculado el applet RX. Fila oculta si maxSlices ≤ 1. |
| **Placa de segmento** | indicador | A | Muestra la letra del segmento actualmente vinculado. Coloreada según la identidad del segmento. La letra del segmento puede representarse como HTML (#2606). |
| **🔓 / 🔒** | botón_alternar | 🔓 (desbloqueado) | Alterna el bloqueo de sintonía en el segmento; un segmento bloqueado ignora los cambios de frecuencia. |
| **ANT1 (antena RX)** | cuadro_combinado | ANT1 | Abre un menú que lista las antenas disponibles; los elementos usan el identificador numérico de la antena o la siguiente etiqueta disponible cuando la lista de antenas del segmento está vacía. Al seleccionar, establece slice→setRxAntenna. Etiqueta de color azul. |
| **ANT1 (antena TX)** | cuadro_combinado | ANT1 | Abre un menú que lista las antenas capaces de TX; los puertos solo RX (prefijo 'RX') se filtran, y los elementos cuyo token comienza con 'ANT', 'TX' o es igual a 'XVTR' se muestran como alternativa. Al seleccionar, establece slice→setTxAntenna. Etiqueta de color rojo. |
| **2.7K (ancho de filtro)** | indicador | 2.7K | Muestra el ancho de filtro actual en kHz. Se actualiza cuando se aplica un valor preestablecido de filtro. |
| **QSK** | indicador | apagado (gris) | Se ilumina en ámbar cuando el break-in de CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (placa)** | botón_alternar | — | Haga clic para establecer este segmento como el segmento de TX. |
| **Combo Mode** | cuadro_combinado | USB | Establece el modo del segmento. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). La opción RADE requiere la bandera de compilación HAVE_RADE. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. |
| **Edición de frecuencia** | campo_texto | — | Ingrese MHz y presione Enter para sintonizar y recentrar. Usa `FrequencyEntryParser` para el procesamiento normalizado de texto. Admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y descarta el editor. Compatible con XVTR: acepta hasta 50000 MHz cuando está en una antena XVTR o cuando el valor ingresado supera explícitamente los 54 MHz. |
| **STEP** | cuadro_giratorio | 100 Hz (índice 2) | Recorre los tamaños de paso por modo. |
| **Valores preestablecidos de ancho de filtro** | botón_pulsador | — | Haga clic para aplicar un valor preestablecido de ancho de filtro; haga clic derecho para guardar el ancho actual como valor preestablecido. Botones ocultos para los modos FM/NFM/DFM. La lectura de ancho usa lógica consciente del modo para que los modos SSB/digitales muestren el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de valores preestablecidos por modo para ampliar/reducir correctos según el modo (#2208). |
| **Widget de banda de paso del filtro** | control_arrastrable | — | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro. |
| **Modo de tono (FM)** | cuadro_combinado | Off | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro_combinado | — | Selecciona la frecuencia de tono CTCSS. 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX. |
| **Offset (FM)** | cuadro_giratorio | 0.0 Mhz | Establece la frecuencia de offset de repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (offset hacia abajo)** | botón_alternar | — | Establece la dirección del offset del repetidor como 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón_alternar | marcado | Establece la dirección del offset del repetidor como simplex (TX = RX). |
| **+ (offset hacia arriba)** | botón_alternar | — | Establece la dirección del offset del repetidor como 'hacia arriba' (TX por encima de RX). |
| **REV** | botón_alternar | — | Invierte el signo del offset de TX para trabajar un par de repetidores invertido. |
| **🔊 / 🔇 (silenciar)** | botón_pulsador | 🔊 (sin silenciar) | Un solo clic silencia/activa el sonido de este segmento (aplazado por el intervalo de discriminación de clics de la plataforma). Doble clic silencia/activa el sonido de todos los segmentos propiedad del usuario mediante la señal muteAllToggled. El ícono cambia cuando la radio confirma mediante SliceModel::audioMuteChanged. Según la Política de Configuración Autoritativa de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar: la radio es la fuente de verdad para el silencio de audio. |
| **Ganancia AF** | control_deslizante | 70 | Ajusta la ganancia de salida de audio del segmento. Rango 0-100. |
| **Panorámico L / R** | control_deslizante | 50 | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). Doble clic restablece a 50 (centro). |
| **SQL** | botón_alternar | — | Activa el squelch en el nivel actual del control deslizante. Deshabilitado (y desactivado automáticamente) en RTTY, modos digitales (DIGU, DIGL) y modos CW donde el squelch interferiría con la decodificación. |
| **Nivel de squelch** | control_deslizante | 20 | Ajusta el umbral de squelch. Deshabilitado en RTTY, modos digitales y CW. El último nivel de squelch manual elegido por el usuario se conserva entre sesiones en la configuración `LastManualSquelchLevel`, por lo que sobrevive a los cambios de modo y reinicios de la aplicación. |
| **Modo AGC** | cuadro_combinado | Med | Establece el modo AGC del segmento. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral AGC** | control_deslizante | 65 | Establece el umbral AGC (o nivel de desactivación de AGC cuando el modo AGC está en Off). |
| **RIT** | botón_alternar | — | Activa/desactiva la sintonía incremental de recepción. |
| **RIT 0** | botón_pulsador | — | Pone a cero el offset de RIT. |
| **Offset RIT** | cuadro_giratorio | +0 Hz | Ajusta el offset de RIT en pasos de 10 Hz. |
| **XIT** | botón_alternar | — | Activa/desactiva la sintonía incremental de transmisión. |
| **XIT 0** | botón_pulsador | — | Pone a cero el offset de XIT. |
| **Offset XIT** | cuadro_giratorio | +0 Hz | Ajusta el offset de XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se deshabilita automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**
- **NT** (Digital de banda estrecha)
- **CW, CWL**

Al cambiar a cualquiera de estos modos, el squelch se desactiva y el botón SQL y el control deslizante se deshabilitan. Esto evita que el squelch bloquee señales FSK débiles e interrumpa la decodificación, particularmente en modos RTTY y digitales donde el squelch eliminaría caracteres FSK (#2504). El estado guardado del squelch se restaura al cambiar a un modo no digital. El nivel de squelch manual se conserva entre cambios de modo mediante la configuración del lado del cliente `LastManualSquelchLevel`, que permanece independiente de los niveles de squelch automáticos de la radio.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (Detección de Radar) está disponible (requiere la bandera de compilación HAVE_RADE), al seleccionar RADE del combo Mode se activa el subsistema de detección de radar para el segmento actual. El modo RADE es solo del lado del cliente: la radio devuelve el modo real (DIGL/DIGU) inmediatamente después de establecer RADE, por lo que el modo() del segmento nunca será "RADE" después de que la radio responda. Al cambiar de RADE en el segmento que está actualmente en modo RADE, se desactiva la detección de radar. El sistema maneja correctamente los cambios de modo en los reenlaces de segmentos, cambios de combo VFO y cargas de perfiles.

## Detalles de ingreso de frecuencia

Al ingresar una frecuencia en el campo de texto **Edición de frecuencia**:

- El texto se normaliza usando `FrequencyEntryParser::normalizedMhzText()` para eliminar los puntos separadores.
- Si el valor ingresado supera explícitamente los 54 MHz (detectado mediante `FrequencyEntryParser::isExplicitMhzEntry()`), la frecuencia se trata como una entrada de VHF/UHF alta incluso sin una antena XVTR.
- Cuando está en una antena XVTR o cuando el valor ingresado supera los 54 MHz, la frecuencia máxima permitida es de 50000 MHz.
- Para entradas no XVTR por debajo de 54 MHz, se aplica el escalado automático estándar: los valores superiores a 54000 se dividen por 1e6, los valores superiores a 54 se dividen por 1e3.
- La entrada emite `directEntryCommitted(freqMhz, "rx-direct-entry")` para consistencia con otras rutas de ingreso de frecuencia.

## Comportamiento del botón de silencio

El botón **🔊 / 🔇 (silenciar)** usa un botón pulsador (no verificable) con discriminación de clics:

- **Un solo clic**: Alterna el silencio solo para este segmento. La acción se aplaza por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularlo.
- **Doble clic**: Alterna el silencio para todos los segmentos propiedad del usuario mediante la señal `muteAllToggled`. El segundo clic cancela el temporizador de un solo clic.
- El ícono (🔊/🔇) se actualiza solo cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`, asegurando que el estado mostrado coincida con el estado real de la radio.
- El estado de silencio no se guarda ni restaura al reconectar: la radio es siempre la fuente de verdad.
