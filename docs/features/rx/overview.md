# Descripción general de RX Controls

El applet RX Controls proporciona ajustes de recepción por slice (canal de recepción): modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, silenciador, RIT/XIT y opciones de repetidor FM. Ábralo para ajustar cualquier parámetro de recepción del slice actualmente seleccionado.

## Cómo funciona

RX Controls se encuentra en el Panel de Applets de la barra lateral derecha. Actívelo o desactívelo con el botón RX del bandeja. Cuando el equipo admite más de un slice, aparece una fila de pestañas de slice (de A a H) en la parte superior; haga clic en una pestaña para vincular el applet a ese slice. Todos los controles que aparecen a continuación se aplican únicamente a ese slice.

El applet está organizado en grupos funcionales, descritos a continuación.

### Identificación del slice y fila de encabezado

| Control | Función | Valor predeterminado |
|---|---|---|
| Insignia de slice | Muestra la letra (A–H) del slice vinculado. Con código de color según la identidad del slice. | A |
| 🔓 / 🔒 | Activa o desactiva el bloqueo de sintonía. Cuando está bloqueado (🔒), el slice ignora los cambios de frecuencia. | 🔓 (desbloqueado) |
| ANT1 (azul) | Abre el menú de antena de RX. Seleccione cualquier antena de la lista de antenas del equipo. | ANT1 |
| ANT1 (rojo) | Abre el menú de antena de TX. Los puertos exclusivos de RX (con prefijo "RX") quedan excluidos. | ANT1 |
| 2.7K | Indicador de solo lectura que muestra el ancho de banda del filtro actual. Se actualiza al aplicar un ajuste preestablecido. | Refleja el filtro activo |
| QSK | Color ámbar cuando está activo el break-in completo de CW. Solo lectura; se controla desde el applet CW. | Apagado (gris) |
| TX (insignia) | Haga clic para designar este slice como el slice de TX. | — |

### Modo y frecuencia

| Control | Función | Valor predeterminado |
|---|---|---|
| Selector de modo | Establece el modo del slice. Reajusta el filtro y los pasos preestablecidos según el nuevo modo. | USB |
| Indicador de frecuencia | Muestra la frecuencia VFO actual con agrupación por puntos. Haga clic para activar el modo de edición. | 0.000.000 |
| Edición de frecuencia | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Acepta hasta 54.000 MHz (450.000 MHz cuando el slice está en una antena XVTR). | — |
| STEP | Alterna entre los tamaños de paso por modo mediante los botones < / > o la rueda del ratón. | 100 Hz |

Modos disponibles: USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY. RADE está disponible en compilaciones que incluyen soporte HAVE_RADE.

### Ancho de filtro

| Control | Función | Clave de ajuste |
|---|---|---|
| Preajustes de ancho de filtro | Botones para anchos de banda comunes según el modo actual. Haga clic para aplicar; haga clic derecho para guardar el ancho actual como preajuste. Ocultos en los modos FM, NFM y DFM. | `FilterPresets` |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. | — |

Rangos de preajuste por modo:

- **USB / LSB:** 1800, 2100, 2400, 2700, 2900, 3300 Hz
- **AM / SAM:** 5600, 6000, 8000, 10000, 12000, 14000 Hz
- **CW:** 50, 100, 250, 400 Hz
- **DIGU / DIGL:** 100, 300, 600, 1000, 1500, 2000 Hz
- **RTTY:** 250, 300, 350, 400, 500, 1000 Hz
- **FM / NFM / DFM:** sin preajustes

### Audio

| Control | Función | Predeterminado | Rango |
|---|---|---|---|
| 🔊 / 🔇 (silenciar) | Silencia la salida de audio del slice. | 🔊 (con audio) | — |
| Ganancia AF | Ajusta el nivel de salida de audio del slice. | 70 | 0–100 |
| Balance L / R | Desplaza el audio del slice entre el canal izquierdo (0) y el derecho (100). Doble clic para restablecer al centro. | 50 | 0–100 |

### Silenciador (Squelch)

| Control | Función | Predeterminado | Rango |
|---|---|---|---|
| SQL | Activa el silenciador en el nivel actual del control deslizante. | Apagado | — |
| Nivel de silenciador | Establece el umbral del silenciador. No tiene efecto si SQL está desactivado. | 20 | 0–100 |

### CAG (AGC)

Oculto en los modos FM, NFM y DFM.

| Control | Función | Predeterminado | Rango |
|---|---|---|---|
| Modo CAG | Establece el modo de control automático de ganancia. | Med | Off, Slow, Med, Fast |
| Umbral de CAG | Establece el umbral de la CAG. Cuando el modo CAG es Off, establece en su lugar el nivel CAG desactivado. | 65 | 0–100 |

### RIT y XIT

| Control | Función | Predeterminado |
|---|---|---|
| RIT | Activa o desactiva la sintonía incremental de recepción (Receive Incremental Tuning). | Off |
| RIT 0 | Pone a cero el desplazamiento RIT inmediatamente. | — |
| Desplazamiento RIT | Los botones < / > o la rueda del ratón ajustan el desplazamiento RIT en pasos de 10 Hz. | +0 Hz |
| XIT | Activa o desactiva la sintonía incremental de transmisión (Transmit Incremental Tuning). | Off |
| XIT 0 | Pone a cero el desplazamiento XIT inmediatamente. | — |
| Desplazamiento XIT | Los botones < / > o la rueda del ratón ajustan el desplazamiento XIT en pasos de 10 Hz. | +0 Hz |

### Ajustes de repetidor FM

Estos controles aparecen únicamente cuando el modo del slice es FM, NFM o DFM.

| Control | Función | Predeterminado | Rango |
|---|---|---|---|
| Modo de tono | Selecciona el modo de tono CTCSS. | Off | Off, CTCSS TX |
| Valor de tono CTCSS | Selecciona la frecuencia del tono CTCSS transmitido. Activo únicamente cuando el modo de tono es CTCSS TX. | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) |
| Desplazamiento | Establece el desplazamiento del repetidor FM en MHz. | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) |
| − | Establece la dirección del desplazamiento hacia abajo (TX por debajo de RX). | — | — |
| Simplex | Establece la dirección del desplazamiento en simplex (TX igual a RX). | Seleccionado | — |
| + | Establece la dirección del desplazamiento hacia arriba (TX por encima de RX). | — | — |
| REV | Invierte el signo del desplazamiento de TX para trabajar un par de repetidor invertido. | Off | — |

## Relacionados

- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
- [Sintonizar el equipo a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena de RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
- [Activar el silenciador y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Usar RIT para desplazar la frecuencia de recepción con una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
