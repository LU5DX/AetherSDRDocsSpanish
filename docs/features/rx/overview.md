# Descripción general de los controles RX

El applet RX Controls le proporciona control de recepción por slice: sintonía de frecuencia, modo, ancho de filtro, selección de antena, CAG, salida de audio, squelch, RIT/XIT y ajustes de repetidor FM. Todo lo que afecta la forma en que un slice recibe y presenta el audio reside aquí.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet requiere una conexión de radio activa.
- El applet RX siempre es visible en el panel de applets (barra lateral derecha). Si el panel está oculto, muéstrelo con View > Applet Panel, o haga clic en el botón de bandeja RX de la barra lateral derecha.

## Cómo funciona

El applet está vinculado a un slice a la vez. Cuando la radio tiene más de un slice activo, aparece una fila de pestañas etiquetadas de A a H en la parte superior del applet. Haga clic en cualquier pestaña para vincular el applet a ese slice. Todos los controles reflejan y operan únicamente sobre ese slice.

Los cambios realizados en el applet se envían inmediatamente a la radio mediante el protocolo SmartSDR. No existe un paso Apply o Save para la mayoría de los controles. La única excepción son los preajustes de ancho de filtro: los anchos de preajuste personalizados se guardan en la clave AppSettings `FilterPresets` y persisten entre sesiones.

## Qué hace cada control

### Selección de slice y encabezado

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona el slice que controla el applet. La fila de pestañas se oculta cuando solo hay un slice activo. |
| Insignia de slice | A | Muestra la letra del slice actualmente vinculado. El color refleja la identidad del slice. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes de clics, desplazamiento o control externo. |
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles. Seleccione una para establecer la antena RX de este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas con capacidad TX (los puertos solo de RX quedan excluidos). Seleccione una para establecer la antena TX de este slice. La etiqueta es roja. |
| Etiqueta de ancho de filtro | 2.7K | Indicador de solo lectura que muestra el ancho de banda de filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda de paso. |
| QSK | apagado (gris) | Se ilumina en ámbar cuando el CW full break-in está activo. Solo lectura; se controla desde el applet CW. |
| TX (insignia) | — | Haga clic para designar este slice como el slice TX. |

### Modo y frecuencia

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Combo de modo | USB | Establece el modo del slice. Modos disponibles: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY. Cambiar el modo remodela el filtro y los preajustes de paso. |
| Etiqueta de frecuencia | 0.000.000 | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | Escriba una frecuencia en MHz y presione Enter para sintonizar y volver a centrar el panadapter. Acepta valores de 0.001 a 54.000 MHz (hasta 450.000 MHz con una antena transverter). |
| STEP | 100 Hz | Establece el tamaño del paso de sintonía. Haga clic en < o > o use la rueda de desplazamiento para recorrer la lista de pasos por modo. Las opciones de paso dependen del modo activo (ejemplo para SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz). |

### Filtro

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Preajustes de ancho de filtro | — | Los botones aplican un ancho de filtro preajustado para el modo actual. Haga clic derecho en un botón de preajuste para guardar el ancho de filtro actual en ese slot. Se ocultan en los modos FM, NFM y DFM. Los preajustes se almacenan en `FilterPresets`. |
| Widget de banda de paso del filtro | — | Arrastre el borde inferior o superior de la visualización de la banda de paso para establecer un límite de filtro personalizado. |

### CAG

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo CAG | Med | Off, Slow, Med, Fast | Establece el modo de CAG. Se oculta en los modos de la familia FM. |
| Umbral de CAG | 65 | 0–100 | Establece el umbral de CAG. Cuando el modo CAG está en Off, ajusta en cambio el nivel CAG-off. |

### Salida de audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silencio) | — | Silencia o reactiva la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| Panorama L / R | 50 | 0–100 | Desplaza el audio del slice entre izquierda (0) y derecha (100). Doble clic restablece el valor a 50 (centro). |
| SQL | apagado | — | Activa el squelch al nivel actual del deslizador. |
| Nivel de squelch | 20 | 0–100 | Establece el umbral del squelch. No tiene efecto cuando SQL está apagado. |

### RIT y XIT

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| RIT | apagado | Activa o desactiva la sintonía incremental de recepción. Cuando está activo, la frecuencia de recepción del slice se desplaza según el offset RIT sin mover el VFO. |
| RIT 0 | — | Pone a cero el offset RIT de inmediato. |
| Offset RIT | +0 Hz | Ajusta el offset RIT en pasos de 10 Hz. Use < / > o la rueda de desplazamiento. |
| XIT | apagado | Activa o desactiva la sintonía incremental de transmisión. Cuando está activo, la frecuencia TX se desplaza según el offset XIT sin cambiar la recepción. |
| XIT 0 | — | Pone a cero el offset XIT de inmediato. |
| Offset XIT | +0 Hz | Ajusta el offset XIT en pasos de 10 Hz. Use < / > o la rueda de desplazamiento. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo del slice es FM, NFM o DFM.

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se transmite un tono CTCSS. |
| Valor del tono CTCSS | — | 67.0 Hz a 254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Se habilita solo cuando el modo de tono está configurado en CTCSS TX. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de offset del repetidor FM. |
| − (offset hacia abajo) | — | — | Establece la dirección del offset TX del repetidor hacia abajo (TX por debajo de RX). |
| Simplex | marcado | — | Establece el offset del repetidor en simplex (TX igual a RX). |
| + (offset hacia arriba) | — | — | Establece la dirección del offset TX del repetidor hacia arriba (TX por encima de RX). |
| REV | — | — | Invierte el signo del offset TX para trabajar un par de repetidor invertido. |

## Consejos

- El deslizador de panorama L / R tiene un pequeño punto de marca central en su ranura. Haga doble clic para volver al centro (50) sin necesidad de ajustarlo manualmente.
- Los preajustes de ancho de filtro son por modo. Los anchos de preajuste personalizados que guarde en un modo no afectan a otros modos.
- Los puertos de antena solo para RX (aquellos cuyos nombres comienzan con "RX") se excluyen automáticamente del menú de antena TX.

## Temas relacionados

- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Trabajar un repetidor FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
