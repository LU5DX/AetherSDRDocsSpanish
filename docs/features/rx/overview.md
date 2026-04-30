# Descripción general de controles RX

El applet RX Controls le brinda control por slice sobre cada parámetro de recepción: modo, frecuencia, selección de antena, ancho de filtro, AGC, audio, squelch, RIT/XIT y configuración de repetidor FM. Ábralo cuando necesite configurar cómo un slice recibe o transmite.

## Cómo funciona

El applet RX siempre está presente en el Applet Panel (barra lateral derecha). Active o desactive su visibilidad con el botón RX tray. Cuando la radio admite más de un slice, aparece una fila de pestañas de slice (A a H) en la parte superior; haga clic en una pestaña para vincular el applet a ese slice. Todos los controles debajo de la fila de pestañas afectan solo al slice seleccionado actualmente.

Los presets de ancho de filtro son la única configuración que persiste entre sesiones, almacenada bajo la clave `FilterPresets`. Todos los demás controles reflejan el estado en vivo de la radio y no se guardan independientemente por AetherSDR.

## Qué hace cada control

### Selección de slice e identidad

| Control | Predeterminado | Comportamiento |
|---|---|---|
| Pestañas de slice (A..H) | — | Selecciona qué slice controla el applet. La fila de pestañas se oculta cuando la radio tiene solo un slice. Los bordes de los botones y los fondos activos siguen el color por slice configurado en SliceColorManager. |
| Insignia de slice | A | Muestra la letra del slice activo. El color está controlado por SliceColorManager; los colores personalizables por slice persisten entre sesiones y se reflejan aquí, en los botones de pestañas de slice, widgets VFO y barras de medidor. Solo lectura. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | Activa/desactiva el bloqueo de sintonización. Un slice bloqueado ignora cambios de frecuencia del panadapter y otras fuentes. |
| TX (insignia) | — | Haga clic para designar este slice como el slice TX. |

### Frecuencia y modo

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Combo Modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, NT, RTTY (+ RADE si se establece la bandera de compilación HAVE_RADE) | Establece el modo del slice. Cambiar el modo remoldea automáticamente los presets de filtro y paso. |
| Etiqueta de frecuencia | 0.000.000 | — | Muestra la frecuencia VFO actual con agrupación punteada. Haga clic para entrar en modo edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz en XVTR) | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| STEP | 100 Hz | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | Haga clic en los botones de triángulo izquierdo/derecho o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian con el modo. |

### Selección de antena

| Control | Predeterminado | Comportamiento |
|---|---|---|
| ANT1 (antena RX) | ANT1 | Abre un menú de antenas disponibles de la lista de antenas de la radio. Seleccione para establecer la antena RX para este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | Abre un menú de antenas capaces de TX. Se excluyen los puertos solo RX (nombres que comienzan con `RX`). La etiqueta es roja. |

### Filtro

| Control | Predeterminado / rango | Clave de configuración | Comportamiento |
|---|---|---|---|
| Presets de ancho de filtro | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; CW: 50/100/250/400 Hz; AM/SAM: 5600–14000 Hz; DIG: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho. Haga clic derecho para guardar el ancho de filtro actual como un preset. Los botones se ocultan en modos FM, NFM y DFM. |
| Etiqueta de ancho de filtro | 2.7K | — | Muestra el ancho de banda de filtro actual. Se actualiza cuando se aplica un preset o se arrastra la banda de paso. Solo lectura. |
| Widget de banda de paso de filtro | — | — | Arrastre el borde inferior o superior para establecer una banda de paso de filtro personalizada. |

### AGC

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | Establece la velocidad de respuesta del AGC. Se oculta en modos de la familia FM. |
| Umbral de AGC | 65 | 0–100 | Establece el umbral de AGC. Cuando el modo AGC es Off, ajusta el nivel de AGC apagado en su lugar. |

### Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (sin silenciar) | — | Silencia o dessilencia la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | Ajusta el nivel de salida de audio del slice. |
| L / R pan | 50 | 0–100 | Panoramiza el audio entre los canales izquierdo (0) y derecho (100). Doble clic para restablecer al centro (50). |
| SQL | — | — | Activa el squelch en el nivel establecido por el regulador de squelch. Se deshabilita y fuerza a desactivarse en modos DIGU, DIGL, NT, CW y CWL. |
| Nivel de squelch | 20 | 0–100 | Establece el umbral de squelch. Solo entra en vigencia cuando SQL está activado. |

### RIT y XIT

| Control | Predeterminado | Comportamiento |
|---|---|---|
| RIT | off | Activa/desactiva Receive Incremental Tuning. |
| RIT 0 | — | Anula el desplazamiento RIT inmediatamente. |
| Desplazamiento RIT | +0 Hz | Ajuste con los botones izquierda/derecha o rueda del ratón en pasos de 10 Hz. |
| XIT | off | Activa/desactiva Transmit Incremental Tuning. |
| XIT 0 | — | Anula el desplazamiento XIT inmediatamente. |
| Desplazamiento XIT | +0 Hz | Ajuste con los botones izquierda/derecha o rueda del ratón en pasos de 10 Hz. |

### Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| QSK | Gris / ámbar | Se ilumina en ámbar cuando CW full break-in está activo. Controlado desde el applet CW; solo lectura aquí. |

### Controles de repetidor FM

Estos controles son visibles solo cuando el modo de slice es FM, NFM o DFM.

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Modo Tone (FM) | Off | Off, CTCSS TX | Selecciona si un tono CTCSS se envía en transmisión. |
| Valor de tono CTCSS | — | 67.0–254.1 Hz (41 tonos EIA/TIA-603 estándar) | Selecciona la frecuencia del tono CTCSS. Activo solo cuando Tone mode es CTCSS TX. |
| Offset (FM) | 0.0 MHz | 0.0–100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (offset abajo) | — | — | Establece la frecuencia TX por debajo de la frecuencia RX por la cantidad de desplazamiento. |
| Simplex | marcado | — | Establece TX y RX a la misma frecuencia (sin desplazamiento). |
| + (offset arriba) | — | — | Establece la frecuencia TX por encima de la frecuencia RX por la cantidad de desplazamiento. |
| REV | — | — | Invierte la dirección del desplazamiento para trabajar un par de repetidor invertido. |

## Consejos

- El regulador L / R pan tiene un punto de marca de centro en la ranura para ayudarle a encontrar 50 a simple vista. Hacer doble clic siempre lo restablece a 50 independientemente de la posición actual.
- Haga clic derecho en un botón preset de filtro para guardar el ancho de filtro actual en esa ranura, permitiéndole personalizar presets por modo. Se almacenan en `FilterPresets` y persisten entre reinicios de aplicación.
- El campo de edición de frecuencia acepta escalado automático de kHz y Hz, por lo que no necesita escribir ceros iniciales para valores menores a MHz.
- Los colores por slice se administran con SliceColorManager. Los cambios que realice en los colores de slice se reflejan de manera coherente en los botones de pestañas de slice, la insignia de slice, widgets VFO y barras de medidor, y persisten entre sesiones.

## Relacionado

- [Sintonice la radio a una frecuencia (escriba MHz en el readout)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambie el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccione un preset de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccione la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
- [Active el squelch y establezca su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Use RIT para compensar la frecuencia de recepción de una estación a la deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Use XIT para compensar la frecuencia de transmisión sin cambiar RX](use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Trabaje un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Bloquee el slice para prevenir resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambie entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
