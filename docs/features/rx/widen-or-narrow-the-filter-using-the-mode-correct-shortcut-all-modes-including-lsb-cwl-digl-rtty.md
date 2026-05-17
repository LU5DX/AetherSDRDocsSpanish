# Ampliar o reducir el filtro usando el atajo correcto para el modo (todos los modos, incluidos LSB/CWL/DIGL/RTTY)

Use el atajo de ampliar/reducir para recorrer los preajustes de ancho de filtro por modo: una pulsación amplía el filtro, la otra lo reduce. El atajo siempre aplica anchos de filtro apropiados para el modo del segmento actual, por lo que nunca obtendrá un filtro de ancho CW en SSB ni un filtro de ancho de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet Controles RX debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet Controles RX, haga clic en el **Combo de modo** y seleccione el modo que desea usar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de preajustes de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo apuntando a la izquierda (◀) junto al indicador de ancho de filtro para reducir el filtro, o en el botón de triángulo apuntando a la derecha (▶) para ampliarlo.

Cada clic avanza por la lista de preajustes del modo. El ancho de filtro actual se muestra en el indicador **2.7K** (ancho de filtro).

## Función de cada control

| Control                          | Valor predeterminado | Comportamiento                                                                 |
|----------------------------------|----------------------|--------------------------------------------------------------------------------|
| **Preajustes de ancho de filtro (◀ / ▶)** | Ver más abajo | Recorre los anchos de filtro por modo en orden descendente (◀) o ascendente (▶). |
| **2.7K (ancho de filtro)**       | Depende del modo     | Muestra el ancho de banda del filtro del segmento actual.                     |

## Preajustes de ancho de filtro por modo

| Modo | Preajustes (Hz) |
|------|-----------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin preajustes de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet Controles RX

El applet Controles RX proporciona controles de recepción por segmento. Aparece al hacer clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|---------------------|----------------|
| **Pestañas de segmento (A..H)** | pestaña | — | Selecciona a qué segmento está vinculado el applet RX. Fila oculta si maxSlices ≤ 1. |
| **Insignia de segmento** | indicador | A | Muestra la letra del segmento vinculado actualmente. Coloreado según la identidad del segmento. La letra del segmento puede mostrarse como HTML (#2606). |
| **🔓 / 🔒** | botón de alternancia | 🔓 (desbloqueado) | Activa/desactiva el bloqueo de sintonía en el segmento; el segmento bloqueado ignora los cambios de frecuencia. |
| **ANT1 (antena RX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas disponibles; los elementos usan el identificador numérico de la antena o la etiqueta disponible siguiente cuando la lista de antenas del segmento está vacía. Al seleccionar, establece slice→setRxAntenna. Etiqueta de color azul. |
| **ANT1 (antena TX)** | cuadro combinado | ANT1 | Abre un menú que lista las antenas con capacidad TX; los puertos solo RX (prefijo 'RX') se filtran, y los elementos cuyo token comienza con 'ANT', 'TX' o es igual a 'XVTR' se muestran como alternativa. Al seleccionar, establece slice→setTxAntenna. Etiqueta de color rojo. |
| **2.7K (ancho de filtro)** | indicador | 2,7K | Muestra el ancho de filtro actual en kHz. Se actualiza al aplicar un preajuste de filtro. |
| **QSK** | indicador | apagado (gris) | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (insignia)** | botón de alternancia | — | Haga clic para establecer este segmento como el segmento TX. |
| **Combo de modo** | cuadro combinado | USB | Establece el modo del segmento. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). La opción RADE requiere la marca de compilación HAVE_RADE. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia VFO actual con agrupación de puntos. Haga clic para cambiar al modo de edición. |
| **Edición de frecuencia** | campo de texto | — | Ingrese MHz y presione Enter para sintonizar y rec entrar. Admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor. Compatible con XVTR: acepta hasta 450 MHz. |
| **STEP** | cuadro de número | 100 Hz (índice 2) | Recorre los tamaños de paso por modo. |
| **Preajustes de ancho de filtro** | botón pulsador | — | Haga clic para aplicar un ancho de filtro preajustado; haga clic derecho para guardar el ancho actual como preajuste. Los botones están ocultos para los modos FM/NFM/DFM. La lectura de ancho usa lógica consciente del modo, por lo que los modos SSB/digitales muestran el ancho etiquetado correcto (#2197). El método stepFilterWidth(direction) recorre la lista de preajustes por modo para ampliar/reducir correctos según el modo (#2208). |
| **Widget de banda de paso de filtro** | control de arrastre | — | Arrastre los bordes bajo/alto para ajustar la banda de paso del filtro. |
| **Modo de tono (FM)** | cuadro combinado | Off | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro combinado | — | Selecciona la frecuencia de tono CTCSS. 41 tonos estándar EIA/TIA-603 (67,0 Hz a 254,1 Hz). Habilitado solo cuando el modo de tono = CTCSS TX. |
| **Offset (FM)** | cuadro de número | 0,0 MHz | Establece la frecuencia de offset del repetidor FM en MHz. Rango 0,0-100,0 MHz (paso 0,1). |
| **− (offset hacia abajo)** | botón de alternancia | — | Establece la dirección del offset del repetidor como 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón de alternancia | marcado | Establece la dirección del offset del repetidor como simplex (TX = RX). |
| **+ (offset hacia arriba)** | botón de alternancia | — | Establece la dirección del offset del repetidor como 'hacia arriba' (TX por encima de RX). |
| **REV** | botón de alternancia | — | Invierte el signo del offset TX para trabajar un par de repetidores invertido. |
| **🔊 / 🔇 (silenciar)** | botón de alternancia | 🔊 (sin silenciar) | Silencia la salida de audio del segmento. Según la Política de Ajustes Autoritativos de la Radio (#2489), el estado de silencio NO se guarda/restaura al reconectar — la radio es la fuente de verdad para el silencio de audio. |
| **Ganancia AF** | control deslizante | 70 | Ajusta la ganancia de salida de audio del segmento. Rango 0-100. |
| **Panorámica L / R** | control deslizante | 50 | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). Doble clic para restablecer a 50 (centro). |
| **SQL** | botón de alternancia | — | Activa el squelch en el nivel actual del control deslizante. Deshabilitado (y apagado automáticamente) en RTTY, modos digitales (DIGU, DIGL) y modos CW donde el squelch interferiría con la decodificación. |
| **Nivel de squelch** | control deslizante | 20 | Ajusta el umbral de squelch. Deshabilitado en RTTY, modos digitales y CW. El último nivel de squelch manual elegido por el usuario se conserva entre sesiones en la configuración `LastManualSquelchLevel`, por lo que sobrevive a cambios de modo y reinicios de la aplicación. |
| **Modo AGC** | cuadro combinado | Med | Establece el modo AGC del segmento. Opciones: Off, Slow, Med, Fast. Oculto en modos de la familia FM. |
| **Umbral AGC** | control deslizante | 65 | Establece el umbral AGC (o el nivel de AGC desactivado cuando el modo AGC es Off). |
| **RIT** | botón de alternancia | — | Activa/desactiva la sintonización incremental de recepción. |
| **RIT 0** | botón pulsador | — | Pone a cero el offset RIT. |
| **Offset RIT** | cuadro de número | +0 Hz | Ajusta el offset RIT en pasos de 10 Hz. |
| **XIT** | botón de alternancia | — | Activa/desactiva la sintonización incremental de transmisión. |
| **XIT 0** | botón pulsador | — | Pone a cero el offset XIT. |
| **Offset XIT** | cuadro de número | +0 Hz | Ajusta el offset XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se desactiva automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**
- **NT** (Narrow-band Digital)
- **CW, CWL**

Al cambiar a cualquiera de estos modos, el squelch se apaga y el botón SQL y el control deslizante se deshabilitan. Esto evita que el squelch enmascare señales FSK débiles y rompa la decodificación, particularmente en RTTY y modos digitales donde el squelch recortaría los caracteres FSK (#2504). El estado de squelch guardado se restaura al cambiar a un modo no digital. El nivel de squelch manual se conserva entre cambios de modo mediante la configuración del lado del cliente `LastManualSquelchLevel`, que permanece independiente de los niveles de squelch automáticos de la radio.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (Detección de Radar) está disponible (requiere la marca de compilación HAVE_RADE), seleccionar RADE del combo de modo activa el subsistema de detección de radar para el segmento actual. El modo RADE es solo del lado del cliente — la radio devuelve el modo real (DIGL/DIGU) inmediatamente después de establecer RADE, por lo que el modo() del segmento nunca será "RADE" después de que la radio responda. Al cambiar del modo RADE en el segmento que está actualmente en modo RADE, se desactiva la detección de radar. El sistema maneja correctamente los cambios de modo entre reasignaciones de segmento, cambios de combo VFO y cargas de perfiles.
