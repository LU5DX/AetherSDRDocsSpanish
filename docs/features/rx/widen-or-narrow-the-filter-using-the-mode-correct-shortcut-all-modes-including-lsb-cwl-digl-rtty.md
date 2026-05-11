# Ampliar o reducir el filtro usando el atajo de modo correcto (todos los modos, incluidos LSB/CWL/DIGL/RTTY)

Use el atajo de ampliar/reducir para recorrer los valores preestablecidos de anchura de filtro por modo: una pulsación amplía el filtro, la otra lo reduce. El atajo siempre aplica anchuras de filtro adecuadas al modo del segmento actual, por lo que nunca obtendrá un filtro de anchura CW en SSB ni un filtro de anchura de radiodifusión en RTTY.

## Antes de comenzar

- Debe haber una radio conectada.
- El applet RX Controls debe estar visible (botón de bandeja **RX** en la barra lateral derecha).

## Pasos

1. En el applet RX Controls, haga clic en el **Mode combo** y seleccione el modo que desea usar (USB, LSB, CW, AM, SAM, DIGU, DIGL, RTTY, FM, etc.). La lista de valores preestablecidos de filtro y los tamaños de paso se actualizan para ese modo.
2. Haga clic en el botón de triángulo que apunta a la izquierda (◀) junto al indicador de anchura de filtro para reducir el filtro, o en el botón de triángulo que apunta a la derecha (▶) para ampliarlo.

Cada clic avanza por la lista de valores preestablecidos del modo. La anchura de filtro actual se muestra en el indicador **2.7K** (anchura de filtro).

## Qué hace cada control

| Control                          | Valor predeterminado | Comportamiento                                                                       |
|----------------------------------|----------------------|--------------------------------------------------------------------------------------|
| **Valores preestablecidos de anchura de filtro (◀ / ▶)** | Ver más abajo        | Recorre las anchuras de filtro por modo en orden descendente (◀) o ascendente (▶). |
| **2.7K (anchura de filtro)**     | Dependiente del modo | Muestra el ancho de banda del filtro del segmento actual.                           |

## Valores preestablecidos de anchura de filtro por modo

| Modo | Valores preestablecidos (Hz) |
|------|------------------------------|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 |
| CW | 50, 100, 250, 400 |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 |
| RTTY | 250, 300, 350, 400, 500, 1000 |
| FM, NFM, DFM | Sin valores preestablecidos de filtro (botones ocultos) |

## Relacionado

- [Seleccionar un valor preestablecido de anchura de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)

# Applet RX Controls

El applet RX Controls proporciona controles de recepción por segmento. Aparece al hacer clic en el botón de bandeja **RX** en la barra lateral derecha.

## Controles

| Control | Tipo | Valor predeterminado | Comportamiento |
|---------|------|----------------------|----------------|
| **Pestañas de segmento (A..H)** | pestaña | — | Selecciona el segmento al que está vinculado el applet RX. La fila se oculta si maxSlices ≤ 1. |
| **Distintivo de segmento** | indicador | A | Muestra la letra del segmento vinculado actualmente. Coloreado según la identidad del segmento. |
| **🔓 / 🔒** | botón de alternancia | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía en el segmento; un segmento bloqueado ignora los cambios de frecuencia. |
| **ANT1 (antena RX)** | cuadro combinado | ANT1 | Abre un menú con las antenas disponibles; al seleccionar una, establece slice→setRxAntenna. Etiqueta de color azul. |
| **ANT1 (antena TX)** | cuadro combinado | ANT1 | Abre un menú con las antenas con capacidad TX; establece slice→setTxAntenna. Etiqueta de color rojo. Los puertos solo RX (prefijo 'RX') se filtran. |
| **2.7K (anchura de filtro)** | indicador | 2.7K | Muestra la anchura de filtro actual en kHz. Se actualiza al aplicar un valor preestablecido de filtro. |
| **QSK** | indicador | apagado (gris) | Se ilumina en ámbar cuando el break-in CW (QSK) está activo. Solo lectura; controlado mediante el botón Breakin del applet CW. |
| **TX (distintivo)** | botón de alternancia | — | Haga clic para establecer este segmento como el segmento TX. |
| **Mode combo** | cuadro combinado | USB | Establece el modo del segmento. Opciones: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE). La opción RADE requiere la marca de compilación HAVE_RADE. |
| **Etiqueta de frecuencia** | indicador | 0.000.000 | Muestra la frecuencia actual del VFO con agrupación de puntos. Haga clic para cambiar al modo de edición. |
| **Edición de frecuencia** | campo de texto | — | Introduzca MHz y presione Enter para sintonizar y volver a centrar. Admite escalado automático de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor. Con cobertura de XVTR: acepta hasta 450 MHz. |
| **STEP** | cuadro de giro | 100 Hz (índice 2) | Recorre los tamaños de paso por modo. |
| **Valores preestablecidos de anchura de filtro** | botón pulsador | — | Haga clic para aplicar una anchura de filtro preestablecida; haga clic derecho para guardar la anchura actual como un valor preestablecido. Los botones se ocultan para los modos FM/NFM/DFM. |
| **Widget de banda de paso del filtro** | control de arrastre | — | Arrastre los bordes inferior/superior para ajustar la banda de paso del filtro. |
| **Modo de tono (FM)** | cuadro combinado | Off | Selecciona el modo de tono CTCSS en FM/NFM/DFM. Visible solo en los modos de la familia FM. |
| **Valor de tono CTCSS** | cuadro combinado | — | Selecciona la frecuencia de tono CTCSS. 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz). Habilitado solo cuando Tone mode = CTCSS TX. |
| **Offset (FM)** | cuadro de giro | 0.0 Mhz | Establece la frecuencia de offset del repetidor FM en MHz. Rango 0.0-100.0 MHz (paso 0.1). |
| **− (offset hacia abajo)** | botón de alternancia | — | Establece la dirección del offset del repetidor a 'hacia abajo' (TX por debajo de RX). |
| **Simplex** | botón de alternancia | marcado | Establece la dirección del offset del repetidor a simplex (TX = RX). |
| **+ (offset hacia arriba)** | botón de alternancia | — | Establece la dirección del offset del repetidor a 'hacia arriba' (TX por encima de RX). |
| **REV** | botón de alternancia | — | Invierte el signo del offset TX para trabajar con un par de repetidores invertido. |
| **🔊 / 🔇 (silencio)** | botón de alternancia | 🔊 (sin silenciar) | Silencia la salida de audio del segmento. |
| **Ganancia AF** | control deslizante | 70 | Ajusta la ganancia de salida de audio del segmento. Rango 0-100. |
| **Panorámica L / R** | control deslizante | 50 | Desplaza el audio del segmento entre los canales izquierdo (0) y derecho (100). Haga doble clic para restablecer a 50 (centro). |
| **SQL** | botón de alternancia | — | Activa el squelch en el nivel actual del control deslizante. Deshabilitado (y desactivado automáticamente) en modos RTTY, digitales (DIGU, DIGL) y CW donde el squelch interferiría con la decodificación. |
| **Nivel de squelch** | control deslizante | 20 | Ajusta el umbral de squelch. Deshabilitado en modos RTTY, digitales y CW. |
| **Modo AGC** | cuadro combinado | Med | Establece el modo AGC del segmento. Opciones: Off, Slow, Med, Fast. Oculto en los modos de la familia FM. |
| **Umbral AGC** | control deslizante | 65 | Establece el umbral AGC (o el nivel de desactivación de AGC cuando el modo AGC es Off). |
| **RIT** | botón de alternancia | — | Activa o desactiva la sintonización incremental de recepción. |
| **RIT 0** | botón pulsador | — | Pone a cero el offset RIT. |
| **Offset RIT** | cuadro de giro | +0 Hz | Ajusta el offset RIT en pasos de 10 Hz. |
| **XIT** | botón de alternancia | — | Activa o desactiva la sintonización incremental de transmisión. |
| **XIT 0** | botón pulsador | — | Pone a cero el offset XIT. |
| **Offset XIT** | cuadro de giro | +0 Hz | Ajusta el offset XIT en pasos de 10 Hz. |

## Comportamiento del squelch en modos digitales y RTTY

El squelch se desactiva automáticamente en los siguientes modos:

- **RTTY**
- **DIGU, DIGL**
- **NT** (Narrow-band Digital)
- **CW, CWL**

Al cambiar a cualquiera de estos modos, el squelch se apaga y el botón SQL y el control deslizante se deshabilitan. Esto evita que el squelch enmascare señales FSK débiles y afecte la decodificación, particularmente en modos RTTY y digitales donde el squelch cortaría los caracteres FSK (#2504). El estado de squelch guardado se restaura al cambiar a un modo no digital.

## Comportamiento del modo RADE (si está habilitado)

Cuando el modo RADE (Radar Detection) está disponible (requiere la marca de compilación HAVE_RADE), al seleccionar RADE del Mode combo se activa el subsistema de detección de radar para el segmento actual. Al salir del modo RADE en el segmento que está actualmente en modo RADE, se desactiva la detección de radar. El sistema maneja correctamente los cambios de modo a través de reenlaces de segmento, cambios de VFO combo y cargas de perfiles.
