# Applet Phone/CW (P/CW)

El applet Phone/CW proporciona controles de transmisión según el modo. Cuando la franja (slice) activa está en un modo de telefonía (USB, LSB, AM, FM), el applet muestra controles de micrófono y procesador. Cuando la franja activa está en modo CW o CWL, cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iambic, tono).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La franja activa debe estar en modo de telefonía o modo CW para que aparezcan los controles correspondientes.

## Cómo abrir el applet

1. Haga clic en el botón **P/CW** en la barra lateral derecha.

## Subpanel Phone

El subpanel Phone contiene la selección de entrada de micrófono, ganancia, procesamiento y controles de monitoreo.

### Fuente de micrófono

Seleccione qué entrada física o virtual utiliza la radio como fuente de micrófono para transmisiones de voz. La elección determina desde dónde toma la FLEX-8600 el audio de TX.

1. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
2. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en la radio.

**Descripciones de fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada a nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio del ordenador. La radio no reporta el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

Cuando la radio está siendo modulada por AetherSDR (modulación de host activa), el cuadro desplegable **Mic source** se limita a `PC` y queda deshabilitado. Una información sobre herramientas explica: "Esta radio es modulada por AetherSDR, por lo que el micrófono del PC es la única entrada. Las otras fuentes son conectores de FlexRadio."

### Controles Phone

| Control            | Descripción                                                                                                                                                                                     | Predeterminado |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Mic source**     | Selecciona la fuente de entrada de micrófono enviada a la radio.                                                                                                                               | —              |
| **Mic gain**       | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena en el lado del cliente en `PcMicGain` porque la radio no gestiona la ganancia en esa ruta.              | 50             |
| **+ACC**           | Habilita la mezcla de entrada del micrófono de accesorios junto con la fuente principal.                                                                                                        | —              |
| **PROC**           | Activa o desactiva el procesador de voz.                                                                                                                                                        | —              |
| **NOR/DX/DX+**     | Nivel de procesador de tres posiciones: 0 (NOR), 1 (DX), 2 (DX+).                                                                                                                              | 0              |
| **DAX**            | Habilita DAX como fuente de audio de TX.                                                                                                                                                        | —              |
| **MON**            | Habilita el monitor de tono lateral de TX para modos de telefonía.                                                                                                                              | —              |
| **Monitor volume** | Establece el volumen del monitor de banda lateral.                                                                                                                                              | —              |

### Medidores (panel Phone)

#### Medidor de nivel

Muestra el nivel de pico de entrada del micrófono en dBFS de -40 a +10 dBFS. Los valores por encima de 0 dBFS aparecen en rojo, indicando recorte.

- Se suprime a -150 dBFS cuando la radio está recibiendo y `met_in_rx` está desactivado.
- Pase el cursor sobre el medidor para ver el nivel de pico exacto en dB con un decimal.

#### Medidor de compresión

Muestra la cantidad de compresión de voz en dB de -25 a 0 dB, con relleno invertido. El medidor indica 0 dB durante la recepción — está controlado por el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz.

- Pase el cursor sobre el medidor para ver la cantidad exacta de compresión en dB con un decimal. El valor se muestra como número positivo (p. ej., "12.5 dB" para 12.5 dB de compresión).

#### Medidor de ALC (panel Phone)

Muestra la lectura del control automático de nivel desde el medidor de ALC por software (pico de SSB posterior al ALC por software en dBFS). El relleno es de derecha a izquierda: vacío a -20 dBFS, completo a 0 dBFS. La zona roja (> -3 dBFS) indica ALC excesivo.

- Pase el cursor sobre el medidor para ver el nivel exacto de ALC en dBFS con un decimal.

| Medidor             | Rango        | Zona roja | Dirección de relleno | Fuente                                      |
|---------------------|--------------|-----------|----------------------|---------------------------------------------|
| **Level**           | -40 a +10 dBFS | > 0 dBFS  | De abajo hacia arriba | Pico de entrada del micrófono               |
| **Compression**     | -25 a 0 dB  | —         | De derecha a izquierda | Valor COMPPEAK de la radio (0–25 dB positivos, mostrados como negativos) |
| **ALC**             | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico de SSB posterior al ALC por software) |

## Subpanel CW

Cuando la franja activa está en modo CW o CWL, el applet cambia automáticamente al subpanel CW.

### Controles CW

| Control               | Descripción                                                                                                                                              | Predeterminado | Rango válido          | Notas                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|-----------------------|------------------------------------------------------------------------------------------------|
| **Delay**             | Retardo de break-in en CW en milisegundos. Escriba un valor directamente en el campo de texto o use el control deslizante adyacente.                       | 500 ms        | 0–2000 ms (paso 10)   | El valor se almacena en caché inmediatamente para evitar el retroceso del control deslizante (#2428). |
| **Speed**             | Velocidad de tecleo CW en palabras por minuto. Escriba un valor directamente o use el control deslizante.                                                 | 20 WPM        | 5–100 WPM             | —                                                                                              |
| **Sidetone**          | Activa o desactiva el tono lateral de CW. Controla simultáneamente el monitor alimentado por DAX de la radio y el generador de tono lateral del lado del cliente. | —             | On / Off              | —                                                                                              |
| **Sidetone volume**   | Volumen del monitor de CW. Escriba un valor directamente o use el control deslizante. Controla de forma sincronizada tanto el lado de la radio (`mon_gain_cw`) como el generador de tono lateral del lado del cliente. | 50            | 0–100                 | Un solo control deslizante gobierna ambas rutas.                                                |
| **L / R pan (CW)**    | Establece el paneo estéreo para el monitor de CW y aplica paneo de potencia constante al generador de tono lateral local. Haga doble clic para centrar en 50. | 50            | 0–100                 | —                                                                                              |
| **Breakin**           | Activa el break-in completo (QSK). Con Breakin activado, los flancos de tecla activan la transmisión y el retardo de break-in mantiene el relé. Con Breakin desactivado, las teclas se ponen en cola y el PTT debe activarse manualmente. | —             | On / Off              | Respeta plenamente la configuración `break_in` de la radio a partir de la v0.9.7.              |
| **Iambic**            | Activa el modo de manipulador de paletas iambic.                                                                                                          | —             | On / Off              | —                                                                                              |
| **Pitch < / >**       | Tono del tono lateral y la decodificación de CW. Escriba un valor (100–6000) o haga clic en los botones **<** / **>** para avanzar en pasos de 10 Hz.       | 600 Hz        | 100–6000 Hz (paso 10) | El tono siempre sigue automáticamente la configuración `cw_pitch` de la radio.                 |

### Cómo funciona la escritura

1. Haga clic en cualquier campo de texto de valor (p. ej., el campo **Delay** que muestra "500").
2. Escriba un número nuevo con el teclado.
3. Presione Enter o Tab para confirmar el valor. El control deslizante se actualiza inmediatamente para coincidir.
4. Si escribe un valor fuera del rango válido, se limita al valor válido más cercano al presionar Enter.

### Comportamiento del tono lateral

El interruptor **Sidetone** y el control deslizante **Sidetone volume** controlan de forma sincronizada tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (~10 ms de latencia). No hay controles separados de tono lateral local; un único conjunto de controles gobierna ambas rutas.

En la v26.5.3 (#2899), el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario (configurada en Settings > Audio) en lugar de la salida predeterminada.

El tono y el paneo siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio. No hay un interruptor "Follow" separado ni un control deslizante manual de sobreescritura de tono.

### Medidor de ALC (panel CW)

Un medidor de ALC idéntico aparece en el subpanel CW, leyendo de la misma fuente `MeterModel::swAlcChanged` que el medidor de ALC del panel Phone. Esto garantiza lecturas de ALC coherentes en operación de voz y CW.

- Pase el cursor sobre el medidor para ver el nivel exacto de ALC en dBFS con un decimal.

| Medidor           | Rango        | Zona roja | Dirección de relleno | Fuente                                      |
|-------------------|--------------|-----------|----------------------|---------------------------------------------|
| **ALC (CW)**      | -20 a 0 dBFS | > -3 dBFS | De derecha a izquierda | `MeterModel::swAlcChanged` (pico de SSB posterior al ALC por software) |

## Integración del panel CWX

Los atajos F1–F12 del panel CWX integrado se controlan por el modo de la franja activa mediante `MainWindow::CwxPanel::setShortcutsEnabled` en lugar de la visibilidad del panel. Los atajos se activan cuando la franja está en modo CW/CWL, independientemente de si el panel CWX es visible (#2582). Estos atajos son mutuamente excluyentes con las asignaciones de teclas F del panel DVK. Las macros CWX también liberan la transmisión automáticamente cuando la cola se vacía (#2450, #2507).

## Compatibilidad con temas (v26.6.1)

El applet Phone/CW es compatible con el tema activo. Los siguientes elementos visuales respetan el tema seleccionado:

- **Contenedor del applet** — Utiliza el estilo del tema para un fondo coherente.
- **Controles deslizantes y rieles** — Todos los controles deslizantes usan `applyPrimarySliderStyle()` para los colores del tema.
- **Colores de etiquetas** — Etiquetas como "Delay:", "Speed:", "L" y "R" (etiquetas de paneo) usan el color de texto secundario del tema.
- **Botones de paso** — Los botones **<** y **>** para el tono de CW usan el fondo y los colores de acento del tema para los estados normal, hover y presionado.

## Lecturas al pasar el cursor (v26.7.4)

En la v26.7.4 (#3936), los tres medidores del panel Phone (Level, Compression, ALC) y el medidor de ALC del panel CW obtuvieron ventanas emergentes de lectura al pasar el cursor. Pase el cursor sobre cualquier medidor para ver el valor numérico exacto:

- **Medidor de nivel**: Muestra "X.X dB" (un decimal).
- **Medidor de compresión**: Muestra la cantidad de compresión como valor positivo en dB (p. ej., "12.5 dB").
- **Medidores de ALC (Phone y CW)**: Muestran "X.X dBFS" (un decimal).

## Entrada de micrófono según capacidades (v26.8.4)

En la v26.8.4, el selector **Mic source** y el medidor **Level** detectan las capacidades:

- Cuando la entrada de audio de transmisión de la radio no es seleccionable desde el cliente (la radio toma el audio de TX del ordenador), el cuadro desplegable **Mic source** se limita a `PC`. El desplegable queda deshabilitado y muestra una información sobre herramientas que explica que la selección de entrada de la radio se realiza en la propia radio. Esto evita presentar una entrada atenuada que parezca una entrada de micrófono utilizable.
- Cuando solo `PC` está disponible, el cliente aplica explícitamente el estado de selección de micrófono `PC` al modelo de transmisión, de modo que las herramientas descendentes (como radiocert) lean el estado correcto.
- El medidor **Level** se oculta por completo en radios cuyo nivel de micrófono no puede medirse en el lado del cliente.

## Consejos

- Cuando use `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta a la radio, porque la medición del micrófono de PC se ejecuta en el lado del cliente independientemente de la configuración `met_in_rx` de la radio.
- Para mezclar el puerto de accesorios junto con su fuente principal, habilite el botón de alternancia **+ACC** después de seleccionar su fuente principal.
- A velocidades de CW más altas, la ruta de tono lateral del lado del cliente (~10 ms de latencia) es más utilizable que el monitor alimentado por DAX de la radio. Dado que el interruptor **Sidetone** controla ambas rutas juntas, habilitar el tono lateral siempre activa automáticamente la ruta de baja latencia.
- El medidor **Compression** indica 0 dB durante la recepción. Esto es intencional: el medidor está controlado por el estado de interbloqueo TRANSMITTING de la radio.
- El botón **Breakin** respeta plenamente la configuración `break_in` de la radio. Con **Breakin** activado (QSK), los flancos de tecla activan la transmisión y el retardo de break-in mantiene el relé. Con **Breakin** desactivado, debe activar el PTT manualmente.
