# Descripción general de los controles de RX

El applet RX Controls le brinda control individual por slice sobre cada parámetro de recepción: modo, frecuencia, filtro, AGC, audio, squelch, RIT/XIT y configuración del repetidor FM. Todos estos controles actúan sobre el slice que esté seleccionado en ese momento en el applet.

## Cómo funciona

El applet RX Controls está siempre visible en el Panel de Applets del lado derecho. Actívelo o desactívelo con el botón `RX` de la bandeja en la barra lateral derecha. Cuando hay más de un slice activo, aparece una fila de pestañas de slice (A a H) en la parte superior del applet; al hacer clic en una pestaña se vincula el applet a ese slice. Todos los controles que aparecen a continuación leen y escriben únicamente en ese slice.

El applet está organizado en grupos funcionales, de arriba a abajo:

**Fila de encabezado** — identidad del slice, bloqueo, selección de antena e indicadores de estado.

**Fila de frecuencia y modo** — lectura del VFO, selector de modo y control del paso de sintonía.

**Fila de filtro** — botones de preajuste, un widget de banda de paso arrastrable e indicador del ancho de filtro actual.

**Fila de audio** — silencio, ganancia AF y paneo estéreo.

**Fila de squelch** — activación del squelch y umbral.

**Fila de AGC** — modo AGC y umbral. Oculta en los modos de la familia FM.

**Fila de RIT/XIT** — desplazamientos de sintonía incremental para RX y TX de forma independiente.

**Fila del repetidor FM** — tono CTCSS, desplazamiento del repetidor y controles de dirección. Visible únicamente en los modos FM, NFM y DFM.

## Qué hace cada control

### Fila de encabezado

| Control | Valor predeterminado | Rango válido / opciones | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Pestañas de slice (A..H) | — | 1–8 pestañas, limitadas por el hardware | — | Selecciona a qué slice está vinculado el applet. La fila se oculta cuando solo hay un slice disponible. |
| Insignia de slice | A | A–H | — | Muestra la letra del slice vinculado actualmente, con color según la identidad del slice. |
| 🔓 / 🔒 | 🔓 (desbloqueado) | — | — | Activa o desactiva el bloqueo de sintonía. Un slice bloqueado ignora los cambios de frecuencia provenientes del panadapter o de la entrada de frecuencia. |
| ANT1 (antena RX) | ANT1 | De la lista de antenas del equipo | — | Abre un menú de antenas disponibles; al seleccionar una se establece la antena RX para este slice. La etiqueta es azul. |
| ANT1 (antena TX) | ANT1 | De la lista de antenas del equipo, excluyendo los puertos solo de RX | — | Abre un menú de antenas con capacidad TX; al seleccionar una se establece la antena TX para este slice. La etiqueta es roja. Los puertos cuyos nombres comienzan con `RX` quedan filtrados. |
| 2.7K (ancho de filtro) | 2.7K | — | — | Indicador de solo lectura. Muestra el ancho de banda del filtro actual. Se actualiza cuando se aplica un preajuste o se arrastra la banda de paso. |
| QSK | apagado (gris) | apagado (gris) / encendido (ámbar) | — | Solo lectura. Se ilumina en ámbar cuando el break-in total de CW está activo. Se controla desde el applet CW. |
| TX (insignia) | — | — | — | Haga clic para designar este slice como el slice TX. |

### Fila de frecuencia y modo

| Control | Valor predeterminado | Rango válido / opciones | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Selector de modo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY | — | Establece el modo del slice. Reorganiza los botones de preajuste de filtro y la lista de pasos para el nuevo modo. |
| Etiqueta de frecuencia | 0.000.000 | — | — | Muestra la frecuencia actual del VFO con agrupación por puntos. Haga clic para entrar en modo de edición. |
| Edición de frecuencia | — | 0.001–54.000 MHz (hasta 450.000 MHz en una antena transverter) | — | Escriba una frecuencia en MHz y presione Enter para sintonizar y recentrar el panadapter. Presione Escape para cancelar y restaurar la frecuencia anterior. |
| STEP | 100 Hz | Lista por modo (p. ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | — | Haga clic en `<` / `>` o use la rueda del ratón para recorrer los tamaños de paso. Los pasos disponibles cambian según el modo. |

### Fila de filtro

| Control | Valor predeterminado | Rango válido / opciones | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Preajustes de ancho de filtro | — | USB/LSB: 1800–3300 Hz; AM/SAM: 5600–14000 Hz; CW: 50–400 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz | `FilterPresets` | Haga clic en un botón para aplicar ese ancho de filtro. Haga clic derecho en un botón para guardar el ancho de filtro actual como ese preajuste. Los botones se ocultan en los modos FM, NFM y DFM. Los preajustes se almacenan por modo. |
| Widget de banda de paso del filtro | — | — | — | Arrastre el borde inferior o superior para ajustar directamente los límites de la banda de paso del filtro. |

### Fila de audio

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| 🔊 / 🔇 (silencio) | 🔊 (con audio) | — | — | Silencia o activa la salida de audio del slice. |
| Ganancia AF | 70 | 0–100 | — | Ajusta el nivel de salida de audio del slice. |
| Paneo L / R | 50 | 0 (todo a la izquierda) – 100 (todo a la derecha) | — | Panea el audio del slice entre los canales izquierdo y derecho. Doble clic restablece el valor a 50 (centro). |

### Fila de squelch

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| SQL | apagado | — | — | Activa el squelch en el nivel actual del deslizador. |
| Nivel de squelch | 20 | 0–100 | — | Establece el umbral del squelch. No tiene efecto mientras SQL está apagado. |

### Fila de AGC

| Control | Valor predeterminado | Rango válido / opciones | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Modo AGC | Med | Off, Slow, Med, Fast | — | Establece el modo AGC del slice. Oculto en los modos de la familia FM. |
| Umbral AGC | 65 | 0–100 | — | Establece el umbral del AGC. Cuando el modo AGC es Off, este control ajusta en su lugar el nivel de ganancia RF manual. La información emergente refleja qué valor se está ajustando. |

### Fila de RIT / XIT

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| RIT | apagado | — | — | Activa o desactiva la Sintonía Incremental de Recepción. |
| RIT 0 | — | — | — | Pone a cero el desplazamiento RIT de inmediato. |
| Desplazamiento RIT | +0 Hz | Paso: 10 Hz | — | Haga clic en `<` / `>` o use la rueda del ratón para ajustar el desplazamiento RIT en pasos de 10 Hz. |
| XIT | apagado | — | — | Activa o desactiva la Sintonía Incremental de Transmisión. |
| XIT 0 | — | — | — | Pone a cero el desplazamiento XIT de inmediato. |
| Desplazamiento XIT | +0 Hz | Paso: 10 Hz | — | Haga clic en `<` / `>` o use la rueda del ratón para ajustar el desplazamiento XIT en pasos de 10 Hz. |

### Fila del repetidor FM (solo modos FM, NFM, DFM)

| Control | Valor predeterminado | Rango válido / opciones | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Modo de tono (FM) | Off | Off, CTCSS TX | — | Selecciona si se envía un tono CTCSS en la transmisión. |
| Valor del tono CTCSS | — | 41 tonos estándar, 67.0–254.1 Hz (EIA/TIA-603) | — | Selecciona la frecuencia del tono CTCSS. Se habilita únicamente cuando el modo de tono es CTCSS TX. |
| Desplazamiento (FM) | 0.0 MHz | 0.0–100.0 MHz, paso 0.1 | — | Establece la frecuencia de desplazamiento del repetidor FM. |
| − (desplazamiento hacia abajo) | — | — | — | Fija la frecuencia TX por debajo de la frecuencia RX en la cantidad del desplazamiento. |
| Simplex | marcado | — | — | Fija la frecuencia TX igual a la frecuencia RX (sin desplazamiento). |
| + (desplazamiento hacia arriba) | — | — | — | Fija la frecuencia TX por encima de la frecuencia RX en la cantidad del desplazamiento. |
| REV | — | — | — | Invierte la dirección del desplazamiento TX para trabajar un par de repetidor invertido. |

## Consejos

- Los valores de los preajustes de filtro se guardan por modo bajo `FilterPresets`. Si hace clic derecho en un botón de preajuste y almacena un ancho personalizado, este persiste entre sesiones para ese modo.
- El deslizador de paneo L / R tiene una marca central en la ranura. Haga doble clic en cualquier punto del deslizador para volver al centro (50) de inmediato.
- La información emergente del umbral AGC cambia su etiqueta según si el modo AGC es Off o está activo, de modo que siempre sabe qué parámetro está ajustando.
- El botón de bloqueo de sintonía 🔓 / 🔒 es la forma más rápida de evitar que un slice sea resintonizado accidentalmente mientras hace clic en el panadapter.

## Temas relacionados

- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el equipo a una frecuencia (escribir MHz en la lectura)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)
