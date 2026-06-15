# Comprender por qué el estado de silencio no se restablece al reconectar (política de autoridad del radio #2489)

Cuando silencia un slice usando el botón de silencio en el applet RX Controls, el estado de silencio no se guarda ni se restablece después de una desconexión y reconexión del radio. Esto es por diseño: AetherSDR trata al radio como la fuente autoritativa para el estado de silencio del audio.

## Pasos

1. Haga clic en el botón de silencio (🔊 / 🔇) en el applet RX Controls para silenciar o activar el sonido del slice.
2. Desconéctese y vuelva a conectarse al radio; el botón de silencio regresa a su estado predeterminado de sonido activado (🔊).

## Qué hace cada control

| Control          | Etiqueta | Predeterminado |
|------------------|----------|----------------|
| Alternar silencio | 🔊 / 🔇  | 🔊 (sonido activado) |

## Detalles del comportamiento

- Un solo clic en el botón de silencio alterna el silencio para este slice. El icono (🔊 o 🔇) se actualiza solo cuando el radio confirma el cambio de estado mediante `SliceModel::audioMuteChanged`.
- Doble clic en el botón de silencio alterna el silencio para todos los slices propietarios simultáneamente.
- La acción de un solo clic se difiere por el intervalo de doble clic de la plataforma (aproximadamente 400 ms). Este retraso permite que un doble clic anule el clic individual y alterne todos los slices.
- No se necesita ninguna bandera de supresión para la señal `clicked()` final de una secuencia de doble clic. `eventFilter` devuelve `true` en `MouseButtonDblClick`, por lo que `QAbstractButton::mouseDoubleClickEvent` nunca se llama. El botón nunca entra en estado presionado en el segundo clic, y la segunda liberación no emite `clicked()`.

## Consejos

- El botón de silencio solo controla el audio del slice actualmente seleccionado. Cada slice tiene su propia alternancia de silencio.
- Si necesita con frecuencia que el audio comience silenciado después de una reconexión, silencie manualmente el slice después de conectar, o use el silencio por hardware del radio si está disponible.

## Relacionado

- [Resumen de RX Controls](../../features/rx/overview.md)
- [Sintonizar el radio a una frecuencia (escriba MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)

---

# RX Controls (RxApplet)

Controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorámica de AF, silenciador, RIT/XIT y configuración de repetidor FM.

## Pestañas de slice

| Control      | Etiqueta | Predeterminado | Rango válido               | Comportamiento                                                                                                                                                                                                                                                                                                                                                                  | Notas                                                                                                                                                                                              |
|--------------|----------|----------------|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pestañas de slice | A..H      | ninguno        | 1-8 botones (limitado por el máximo de slices del hardware) | Selecciona el slice al que está vinculado el applet RX; emite sliceActivationRequested.                                                                                                                                                                                                                                                                                         | Fila oculta si maxSlices <= 1. clearSliceButtons() elimina todos los botones de pestaña generados y restaura la insignia de slice estática al desconectar (v0.9.5.1, #2254). Las conexiones de clic del botón de slice están protegidas contra manejadores de señal duplicados en reconexiones. |
| Insignia de slice | A            | A/B/C/D/E/F/G/H | ninguno                   | Muestra la letra del slice actualmente vinculado.                                                                                                                                                                                                                                                                                                                               | Coloreada por identidad del slice.                                                                                                                                                                |

## Sintonización de frecuencia

| Control                    | Etiqueta     | Predeterminado           | Rango válido                                             | Comportamiento                                                                                                                                                                                               | Notas                                                                                                                                                               |
|----------------------------|--------------|--------------------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bloqueo de sintonía        | 🔓 / 🔒      | 🔓 (desbloqueado)        | ninguno                                                   | Alterna el bloqueo de sintonía en el slice; el slice bloqueado ignora los cambios de frecuencia.                                                                                                             | El icono cambia entre candado abierto y cerrado.                                                                                                                   |
| Etiqueta de frecuencia     | 0.000.000    | 0.001-54.000 MHz (450.000 MHz en XVTR)                   | Muestra la frecuencia actual del VFO con agrupación de puntos.                                                                                                                         | Haga clic para cambiar al modo de edición.                                                                                                                         |
| Edición de frecuencia      | ninguno      | 0.001-54.000 MHz (450.000 MHz en XVTR)                   | Ingrese MHz y presione Enter para sintonizar y re-centrar; admite escala automática de kHz/Hz. Escape cancela la entrada, restaura la frecuencia anterior y cierra el editor (v0.9.0, #1954). | Compatible con XVTR: acepta hasta 450 MHz cuando el slice está en una antena XVTR. Usa FreqLineEdit para un mejor manejo de entrada.                                |
| PASO (STEP)                | 100 Hz (índice 2) | lista por modo (ej. SSB: 1, 10, 50, 100, 500, 1000, 2000, 3000 Hz) | < / > o rueda del ratón recorre los tamaños de paso por modo; emite stepSizeChanged.                                                                                                                         | La lista de pasos depende del modo del slice. Los cambios de paso también emiten stepSizeChangedByUser para sincronización externa.                                |

## Selección de antena

| Control      | Etiqueta | Predeterminado             | Comportamiento                                                                                                                          | Notas                                                                                |
|--------------|----------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Antena RX    | ANT1     | de ant_list en estado del panadapter | Abre un menú que enumera las antenas disponibles; al seleccionar, establece slice->setRxAntenna.                                          | Rellenado desde ant_list del radio; etiqueta con color azul.                        |
| Antena TX    | ANT1     | de ant_list, excluyendo puertos solo RX | Abre un menú que enumera las antenas con capacidad TX; establece slice->setTxAntenna.                                                    | Etiqueta con color rojo; los puertos de antena solo RX (prefijo 'RX') se filtran.   |

## Modo y filtro

| Control                  | Etiqueta | Predeterminado | Rango válido                                                                   | Comportamiento                                                                                                                                                                         | Notas                                                                                                                                              |
|--------------------------|----------|----------------|--------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Combo de modo            | USB      | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE) | Establece el modo del slice; reconfigura los ajustes predefinidos de filtro y paso para el nuevo modo.                                                                                   | Seleccionar un modo emite wfmActivated(false) para eliminar cualquier superposición del demodulador de software WFM. La opción RADE requiere la bandera de compilación HAVE_RADE. |
| Botón WFM                | WFM      | desmarcado   | Activado/Desactivado | Alterna para habilitar el demodulador FM por software mediante DAX IQ → Hi-Fi Cable para recepción de FM de banda ancha.                                                               | Ubicado junto al combo de modo. Cuando se activa, emite wfmActivated(true) con el ID del slice actual.                                            |
| Ancho de filtro          | 2.7K     | ninguno       |                                                                                | Muestra el ancho de filtro actual en kHz.                                                                                                                                              | Se actualiza cuando se aplica un ajuste predefinido de filtro.                                                                                     |
| Ajustes predefinidos de ancho de filtro | ninguno       | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; AM/SAM: 5600-14000 Hz; CW: 50/100/250/400 Hz; DIG: 100-2000 Hz; RTTY: 250-1000 Hz | Haga clic para aplicar un ancho de filtro predefinido; clic derecho para guardar el ancho actual como predefinido.                                                                       | Botones ocultos para modos FM/NFM/DFM; los predefinidos son por modo. La lectura de ancho (compartida con VfoWidget mediante RxApplet::formatFilterWidth) utiliza lógica sensible al modo. El método stepFilterWidth(direction) recorre la lista de predefinidos por modo para un estrechamiento/ensanchamiento correcto (#2208). |
| Widget de banda de paso del filtro | ninguno       | ninguno       |                                                                                | Arrastre los bordes lo/hi para ajustar la banda de paso del filtro; emite filterChanged (lo, hi).                                                                                          | ninguno                                                                                                                                            |

## Indicador de break-in CW

| Control              | Etiqueta | Predeterminado | Comportamiento                                                               | Notas                                                        |
|----------------------|----------|----------------|------------------------------------------------------------------------------|--------------------------------------------------------------|
| Indicador QSK        | QSK      | ninguno        | Se enciende en ámbar cuando el break-in CW (QSK) está activo.                 | Solo lectura; controlado mediante el botón Breakin del applet CW. |

## Selección de slice TX

| Control    | Etiqueta | Comportamiento                                                                 | Notas |
|------------|----------|--------------------------------------------------------------------------------|-------|
| Insignia TX | TX       | Haga clic para establecer este slice como el slice TX (llama a slice->setTxSlice). | ninguno |

## Controles de audio

| Control               | Etiqueta | Predeterminado | Rango válido | Comportamiento                                                                                                                                                                                                                                                    | Notas                                                                                                                   |
|-----------------------|----------|----------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Alternar silencio     | 🔊 / 🔇  | 🔊 (sonido activado) | ninguno      | Un solo clic silencia/activa el sonido de este slice (diferido por el intervalo de discriminación de clic de la plataforma). Doble clic silencia/activa el sonido de todos los slices propietarios mediante la señal muteAllToggled. El icono cambia cuando el radio lo confirma mediante SliceModel::audioMuteChanged. | Según la Política de Ajustes con Autoridad del Radio (#2489), el estado de silencio NO se guarda/restablece al reconectar. |
| Ganancia AF           | 70       | 0-100         | Ajusta la ganancia de salida de audio del slice; emite afGainChanged.                                                                                                                                                                                             | ninguno                                                                                                                |
| Panorámica L / R      | 50       | 0-100         | Desplaza el audio del slice entre los canales izquierdo (0) y derecho (100).                                                                                                                                                                                      | Doble clic restablece a 50 (centro).                                                                                   |

## Silenciador (Squelch)

| Control            | Etiqueta | Predeterminado | Rango válido | Comportamiento                                                                                                                                                            | Notas                                                                                        |
|--------------------|----------|----------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| Alternar SQL       | SQL      | ninguno        | ninguno      | Activa el silenciador al nivel actual del deslizador. Desactivado (y apagado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el silenciador cortaría los caracteres FSK (#2504). | ninguno                                                                                      |
| Nivel de silenciador | 20       | 0-100         | Ajusta el umbral del silenciador; solo tiene efecto cuando SQL está activado. Desactivado en modos RTTY y digitales.                                                      | ninguno                                                                                      |

## Controles AGC

| Control           | Etiqueta | Predeterminado     | Rango válido  | Comportamiento                                                                                                                                                                                                                         | Notas                                                                                                                                                                                                                                                   |
|-------------------|----------|--------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Modo AGC          | Med      | Off, Slow, Med, Fast | Establece el modo AGC del slice.                                                                                                                                                                                                       | Oculto en modos de la familia FM.                                                                                                                                                                                                                       |
| Umbral AGC        | 65       | 0-100              | Establece el umbral AGC (o el nivel de apagado AGC cuando el modo AGC es Off).                                                                                                                                                         | Haga clic derecho en el deslizador para abrir un menú contextual y seleccione "Calibrar AGC-T contra el piso de ruido…" para establecer automáticamente el umbral basado en el piso de ruido actual. La información sobre herramientas refleja qué valor se está ajustando y anuncia la calibración con clic derecho. |

## RIT/XIT

| Control       | Etiqueta | Predeterminado | Rango válido | Comportamiento                                                                                        | Notas |
|---------------|----------|----------------|--------------|-------------------------------------------------------------------------------------------------------|-------|
| Alternar RIT  | RIT      | ninguno        | ninguno      | Activa/desactiva la Sintonización Incremental de Recepción (RIT).                                     | ninguno |
| Cero RIT      | RIT 0    | ninguno        | ninguno      | Pone a cero el desplazamiento RIT.                                                                     | ninguno |
| Desplazamiento RIT | +0 Hz | paso 10 Hz | < / > o rueda del ratón ajusta el desplazamiento RIT en pasos de 10 Hz.                               | ninguno |
| Alternar XIT  | XIT      | ninguno        | ninguno      | Activa/desactiva la Sintonización Incremental de Transmisión (XIT).                                   | ninguno |
| Cero XIT      | XIT 0    | ninguno        | ninguno      | Pone a cero el desplazamiento XIT.                                                                     | ninguno |
| Desplazamiento XIT | +0 Hz | paso 10 Hz | < / > o rueda del ratón ajusta el desplazamiento XIT en pasos de 10 Hz.                               | ninguno |

## Configuración de repetidor FM

| Control           | Etiqueta | Predeterminado     | Rango válido                                    | Comportamiento                                                                                                   | Notas                                               |
|-------------------|----------|--------------------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| Modo de tono      | Off      | Off, CTCSS TX      | Selecciona el modo de tono CTCSS en FM/NFM/DFM. | Visible solo en modos de la familia FM.                                                                           |
| Tono CTCSS        | ninguno  | 41 tonos estándar EIA/TIA-603 (67.0 Hz a 254.1 Hz) | Selecciona la frecuencia de tono CTCSS enviada con la transmisión.                                           | Habilitado solo cuando el Modo de tono = CTCSS TX. |
| Desplazamiento    | 0.0 MHz  | 0.0-100.0 MHz (paso 0.1) | Establece la frecuencia de desplazamiento del repetidor FM en MHz.                                           | ninguno                                             |
| Desplazamiento hacia abajo | −        | ninguno        | ningulo                                       | Establece la dirección del desplazamiento del repetidor como 'hacia abajo' (TX por debajo de RX).               | ninguno                                             |
| Símplex           | Símplex  | marcado          | ningulo                                       | Establece la dirección del desplazamiento del repetidor como símplex (TX = RX).                                | ninguno                                             |
| Desplazamiento hacia arriba | +        | ninguno        | ningulo                                       | Establece la dirección del desplazamiento del repetidor como 'hacia arriba' (TX por encima de RX).             | ninguno                                             |
| REV               | REV      | ninguno        | ningulo                                       | Invierte el signo del desplazamiento TX para trabajar un par de repetidor invertido.                           | ninguno                                             |

## Calibración del piso de ruido AGC-T

El deslizador de umbral AGC admite una función de calibración automática para establecer el umbral basado en el piso de ruido actual.

### Pasos

1. Haga clic derecho en el deslizador de umbral AGC.
2. Seleccione "Calibrar AGC-T contra el piso de ruido…" en el menú contextual.
3. El applet emite una solicitud para calibrar el ID del slice actual. El sistema mide el piso de ruido y establece el umbral AGC en consecuencia.

### Notas

- Esta función está disponible en
