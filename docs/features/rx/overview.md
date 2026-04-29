# Descripción general de los controles RX

El applet RX Controls le ofrece control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, CAG, audio, silenciador (squelch), RIT/XIT y ajustes de repetidor FM. Ábralo cuando necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX está siempre presente en el panel de applets (barra lateral derecha). Active o desactive su visibilidad con el botón RX del área de iconos. Cuando el equipo admite más de un slice, aparece una fila de pestañas de slice (A hasta H) en la parte superior; al hacer clic en una pestaña, el applet queda vinculado a ese slice. Todos los controles situados bajo la fila de pestañas afectan únicamente al slice seleccionado en ese momento.

Los preajustes de ancho de filtro son el único parámetro que persiste entre sesiones, almacenado bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo del equipo y AetherSDR no los guarda de forma independiente.

## Qué hace cada control

### Selección e identidad del slice

| Control | Predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Seleccionan qué slice controla el applet. La fila de pestañas se oculta cuando el equipo tiene un solo slice. |
| Indicador de slice | A | Muestra la letra del slice activo, con color según la identidad del slice. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa o desactiva el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes del panadapter y otras fuentes. |
| TX (indicador) | — | Haga clic para designar este slice como el slice TX. |

### Frecuencia y modo

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Selector de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY | Establece el modo del slice. Al cambiar de modo, los preajustes de filtro y paso se reconfiguran automáticamente. |
| Indicador de frecuencia | 0.000.000 | — | Muestra la frecuencia actual del VFO con agrupación por puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz con XVTR) | Escriba una frecuencia en MHz y pulse Intro para sintonizar y recentrar. Pulse Escape para cancelar y restaurar la frecuencia anterior. |
| STEP | 100 Hz | Lista por modo (p. ej., SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones triangulares izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. |

### Selección de antena

| Control | Predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú con las antenas disponibles de la lista de antenas del equipo. Seleccione una para establecer la antena RX de este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú con las antenas habilitadas para TX. Los puertos solo de recepción (cuyos nombres comienzan con `RX`) quedan excluidos. La etiqueta es roja. |

### Filtro

| Control | Predeterminado / rango | Clave de ajuste | Comportamiento |
|---|---|---|---|
| Preajustes de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como preajuste. Los botones se ocultan en los modos FM, NFM y DFM. |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda de filtro actual. Se actualiza al aplicar un preajuste o al arrastrar la banda de paso. Solo lectura. |
| Widget de banda de paso del filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso personalizada. |

### CAG

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo CAG | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta de la CAG. Se oculta en los modos de la familia FM. |
| Umbral de CAG | 65 | 0–100 | Establece el umbral de la CAG. Cuando el modo CAG es Off, ajusta en su lugar el nivel de CAG desactivada. |

### Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silencio) | — | Silencia o reactiva la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| Panorama L / R | 50 | 0–100 | Desplaza el audio entre los canales izquierdo (0) y derecho (100). Haga doble clic para restablecer el centro (50). |
| SQL | — | — | Activa el silenciador al nivel establecido por el deslizador de squelch. |
| Nivel de squelch | 20 | 0–100 | Establece el umbral del silenciador. Solo tiene efecto cuando SQL está activado. |

### RIT y XIT

| Control | Predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa o desactiva la sintonía incremental de recepción (RIT). |
| RIT 0 | — | Pone a cero el desplazamiento RIT de inmediato. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa o desactiva la sintonía incremental de transmisión (XIT). |
| XIT 0 | — | Pone a cero el desplazamiento XIT de inmediato. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierdo/derecho o la rueda del ratón en pasos de 10 Hz. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando el break-in total de CW está activo. Se controla desde el applet CW; aquí es solo lectura. |

### Controles de repetidor FM

Estos controles son visibles únicamente cuando el modo del slice es FM, NFM o DFM.

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | Selecciona si se envía un tono CTCSS durante la transmisión. |
| Valor del tono CTCSS | — | 67.0–254.1 Hz (41 tonos estándar EIA/TIA-603) | Selecciona la frecuencia del tono CTCSS. Solo activo cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento negativo) | — | — | Coloca la frecuencia TX por debajo de la frecuencia RX en la cantidad de desplazamiento indicada. |
| Simplex | marcado | — | Establece TX y RX en la misma frecuencia (sin desplazamiento). |
| + (desplazamiento positivo) | — | — | Coloca la frecuencia TX por encima de la frecuencia RX en la cantidad de desplazamiento indicada. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar con un par de repetidor invertido. |

## Consejos

- El deslizador de panorama L / R tiene una marca central en la ranura para ayudarle a encontrar el valor 50 visualmente. Al hacer doble clic siempre se restablece a 50 independientemente de la posición actual.
- Hacer clic derecho en un botón de preajuste de filtro guarda el ancho de filtro actual en esa posición, lo que le permite personalizar los preajustes por modo. Estos se almacenan en `FilterPresets` y sobreviven a los reinicios de la aplicación.
- El campo de edición de frecuencia acepta escalado automático de kHz y Hz, por lo que no es necesario escribir ceros iniciales para valores inferiores a 1 MHz.

## Relacionados

- [Sintonizar el equipo a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
- [Activar el silenciador y establecer su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Usar RIT para desplazar la frecuencia de recepción con una estación que deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Bloquear el slice para evitar una sintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Entender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
