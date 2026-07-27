# Applet P/CW (Phone/CW)

El applet Phone/CW proporciona controles de transmisión adaptados al modo. Cuando el slice activo está en un modo de teléfono (USB, LSB, AM, FM), el applet muestra controles de micrófono y procesador. Cuando el slice activo está en modo CW o CWL, cambia automáticamente a controles CW (retardo, velocidad, tono lateral, iámbico, tono).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en modo de teléfono o modo CW para que aparezcan los controles respectivos.

## Cómo abrir el applet

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

## Subpanel de teléfono

El subpanel de teléfono contiene la selección de entrada de micrófono, ganancia, procesamiento y controles de monitoreo.

### Fuente de micrófono

Seleccione qué entrada física o virtual utiliza la radio como fuente de micrófono para transmisiones de voz. La elección determina de dónde toma el FLEX-8600 su audio de TX.

1. Localice el cuadro desplegable **Mic source** en el subpanel de teléfono.
2. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en la radio.

**Descripciones de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio del ordenador. La radio no informa el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

Cuando la radio está siendo modulada por AetherSDR (modulación de host activa), el cuadro desplegable **Mic source** se fuerza únicamente a `PC` y se deshabilita. Una información sobre herramientas explica: "Esta radio es modulada por AetherSDR, por lo que el micrófono del PC es la única entrada. Las otras fuentes son conectores FlexRadio."

### Controles de teléfono

| Control            | Descripción                                                                                                                                                                                     | Valor por defecto |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| **Mic source**     | Selecciona la fuente de entrada de micrófono enviada a la radio.                                                                                                                                | —       |
| **Mic gain**       | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena del lado del cliente en `PcMicGain` porque la radio no gestiona la ganancia en esa ruta.              | 50      |
| **+ACC**           | Habilita la mezcla de la entrada de micrófono de accesorios junto con la fuente principal.                                                                                                      | —       |
| **PROC**           | Activa o desactiva el procesador de voz.                                                                                                                                                        | —       |
| **NOR/DX/DX+**     | Nivel del procesador de tres posiciones: 0 (NOR), 1 (DX), 2 (DX+).                                                                                                                             | 0       |
| **DAX**            | Habilita DAX como fuente de audio de TX.                                                                                                                                                        | —       |
| **MON**            | Habilita el monitor de tono lateral de TX para modos de teléfono.                                                                                                                               | —       |
| **Monitor volume** | Establece el volumen del monitor de banda lateral.                                                                                                                                              | —       |

### Indicadores de medición (Panel de teléfono)

#### Indicador de nivel

Muestra el nivel máximo de entrada del micrófono en dBFS de -40 a +10 dBFS. Los valores superiores a 0 dBFS aparecen en rojo, lo que indica recorte.

- Suprimido a -150 dBFS cuando la radio está recibiendo y `met_in_rx` está desactivado.
- Pase el cursor sobre el indicador para ver el nivel máximo exacto en dB con un decimal.

#### Indicador de compresión

Muestra la cantidad de compresión de voz en dB de -25 a 0 dB, con llenado invertido. El indicador marca 0 dB durante la recepción; está controlado por el estado de TRANSMISIÓN del interbloqueo de la radio y la activación del procesador de voz.

- Pase el cursor sobre el indicador para ver la cantidad exacta de compresión en dB con un decimal. El valor se muestra como un número positivo (por ejemplo, "12.5 dB" para 12.5 dB de compresión).

#### Indicador ALC (Panel de teléfono)

Muestra la lectura del control automático de nivel del medidor ALC de software (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. La zona roja (> -3 dBFS) indica ALC excesivo.

- Pase el cursor sobre el indicador para ver el nivel ALC exacto en dBFS con un decimal.

| Indicador         | Rango        | Zona roja | Dirección de llenado | Fuente                                      |
|-------------------|--------------|-----------|----------------------|---------------------------------------------|
| **Level**         | -40 a +10 dBFS | > 0 dBFS  | De abajo arriba      | Pico de entrada del micrófono               |
| **Compression**   | -25 a 0 dB   | —         | De derecha a izquierda | Valor COMPPEAK de la radio (0–25 dB positivo, mostrado como negativo) |
| **ALC**           | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software) |

## Subpanel CW

Cuando el slice activo está en modo CW o CWL, el applet cambia automáticamente al subpanel CW.

### Controles CW

| Control               | Descripción                                                                                                                                              | Valor por defecto | Rango válido           | Notas                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----------------------|------------------------------------------------------------------------------------------------|
| **Delay**             | Retardo de ruptura CW en milisegundos. Escriba un valor directamente en el campo de texto o use el deslizador adyacente.                                  | 500 ms  | 0–2000 ms (paso 10)   | El valor se almacena en caché inmediatamente para evitar el rebote del deslizador (#2428).    |
| **Speed**             | Velocidad de tecleo CW en palabras por minuto. Escriba un valor directamente o use el deslizador.                                                          | 20 WPM  | 5–100 WPM             | —                                                                                              |
| **Sidetone**          | Activa o desactiva el tono lateral CW. Controla simultáneamente el monitor alimentado por DAX de la radio y el generador de tono lateral del lado del cliente. | —       | Activado / Desactivado | —                                                                                              |
| **Sidetone volume**   | Volumen del monitor CW. Escriba un valor directamente o use el deslizador. Controla simultáneamente el lado de la radio (`mon_gain_cw`) y el generador de tono lateral del lado del cliente. | 50      | 0–100                 | Un solo deslizador gobierna ambas rutas.                                                        |
| **L / R pan (CW)**    | Establece la panorámica estéreo para el monitor CW y aplica panorámica de potencia constante al generador de tono lateral local. Haga doble clic para centrar en 50. | 50      | 0–100                 | —                                                                                              |
| **Breakin**           | Activa o desactiva la ruptura completa (QSK). Con Breakin ACTIVADO, los flancos de la llave activan TX y el retardo de ruptura mantiene el relé. Con Breakin DESACTIVADO, las llaves se ponen en cola y el PTT debe activarse manualmente. | —       | Activado / Desactivado | Respeta completamente el ajuste `break_in` de la radio a partir de la v0.9.7.                 |
| **Iambic**            | Activa o desactiva el modo de manipulador de paletas iámbico.                                                                                             | —       | Activado / Desactivado | —                                                                                              |
| **Pitch < / >**       | Tono lateral y tono de descodificación CW. Escriba un valor (100–6000) o haga clic en los botones **<** / **>** para incrementar o decrementar de 10 en 10 Hz. | 600 Hz  | 100–6000 Hz (paso 10) | El tono siempre sigue automáticamente el ajuste `cw_pitch` de la radio.                       |

### Cómo escribir

1. Haga clic en cualquier campo de texto de valor (por ejemplo, el campo **Delay** que muestra "500").
2. Escriba un nuevo número con su teclado.
3. Pulse Enter o Tabulador para confirmar el valor. El deslizador se actualiza para coincidir inmediatamente.
4. Si escribe un valor fuera del rango válido, se ajusta al valor válido más cercano cuando pulsa Enter.

### Comportamiento del tono lateral

El interruptor **Sidetone** y el deslizador **Sidetone volume** controlan simultáneamente el monitor alimentado por DAX de la radio y el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia). No hay controles de tono lateral local separados; un solo conjunto de controles gobierna ambas rutas.

En la v26.5.3 (#2899), el tono lateral CW se enruta a la salida de audio seleccionada por el usuario (configurada en Settings > Audio) en lugar de la salida predeterminada.

El tono y la panorámica siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No hay un interruptor "Follow" separado ni un deslizador de anulación de tono manual.

### Indicador ALC (Panel CW)

Aparece un indicador ALC idéntico en el subpanel CW, que lee de la misma fuente `MeterModel::swAlcChanged` que el indicador ALC del panel de teléfono. Esto garantiza lecturas ALC coherentes en toda la operación de voz y CW.

- Pase el cursor sobre el indicador para ver el nivel ALC exacto en dBFS con un decimal.

| Indicador       | Rango        | Zona roja | Dirección de llenado | Fuente                                      |
|-----------------|--------------|-----------|----------------------|---------------------------------------------|
| **ALC (CW)**    | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico SSB posterior al ALC de software) |

## Integración del panel CWX

Los atajos F1–F12 del panel CWX integrado se activan mediante el modo del slice activo a través de `MainWindow::CwxPanel::setShortcutsEnabled` en lugar de la visibilidad del panel. Los atajos se disparan cuando el slice está en modo CW/CWL independientemente de si el panel CWX está visible (#2582). Estos atajos son mutuamente excluyentes con las asignaciones de teclas F del panel DVK. Las macros CWX también liberan TX automáticamente cuando la cola se vacía (#2450, #2507).

## Soporte de temas (v26.6.1)

El applet Phone/CW soporta el tema activo. Los siguientes elementos visuales respetan el tema seleccionado:

- **Contenedor del applet** — Utiliza el estilo del tema para un fondo coherente.
- **Manijas y ranuras de deslizadores** — Todos los deslizadores usan `applyPrimarySliderStyle()` para los colores del tema.
- **Colores de etiquetas** — Etiquetas como "Delay:", "Speed:", "L" y etiquetas de panorámica "R" usan el color de texto secundario del tema.
- **Botones de paso** — Los botones **<** y **>** para CW Pitch usan el color de fondo y acento del tema para los estados normal, hover y presionado.

## Lecturas al pasar el cursor (v26.7.4)

En la v26.7.4 (#3936), los tres medidores del panel de teléfono (Level, Compression, ALC) y el indicador ALC del panel CW obtuvieron ventanas emergentes de lectura al pasar el cursor. Pase el cursor sobre cualquier indicador para ver el valor numérico exacto:

- **Indicador Level**: Muestra "X.X dB" (un decimal).
- **Indicador Compression**: Muestra la cantidad de compresión como un valor positivo en dB (por ejemplo, "12.5 dB").
- **Indicadores ALC (Phone y CW)**: Muestra "X.X dBFS" (un decimal).

## Consejos

- Cuando use `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta a la radio, porque la medición del micrófono del PC se ejecuta del lado del cliente independientemente del ajuste `met_in_rx` de la radio.
- Para mezclar el puerto de accesorios junto con su fuente principal, active el botón de conmutación **+ACC** después de seleccionar su fuente principal.
- A velocidades CW más altas, la ruta de tono lateral del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX de la radio. Debido a que el interruptor **Sidetone** controla ambas rutas juntas, activar el tono lateral siempre activa automáticamente la ruta de baja latencia.
- El indicador **Compression** marca 0 dB durante la recepción. Esto es intencional: el indicador está controlado por el estado de TRANSMISIÓN del interbloqueo de la radio.
- El botón **Breakin** respeta completamente el ajuste `break_in` de la radio. Con **Breakin** activado (QSK), los flancos de la llave activan TX y el retardo de ruptura mantiene el relé. Con **Breakin** desactivado, debe activar el PTT manualmente.
