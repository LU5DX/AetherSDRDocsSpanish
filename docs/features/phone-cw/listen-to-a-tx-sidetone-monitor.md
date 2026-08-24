# Applet de Phone/CW

El applet de Phone/CW es un panel de transmisión que se adapta al modo. Muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando el slice activo está en modo CW.

En la v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR).

En la v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Los indicadores ALC de ambos paneles ahora se inicializan a -20 dBFS al inicio.

En la v26.6.1, todos los estilos de deslizadores y etiquetas ahora usan el ThemeManager para un tema coherente en toda la aplicación. El widget contenedor aplica una clase de tema de `applet/digi`.

En la v26.7.4, los cuatro indicadores (Level, Compression, ALC Phone, ALC CW) ahora muestran una ventana emergente con el valor al pasar el mouse sobre ellos, mostrando la lectura exacta con un decimal para una monitorización precisa (#3936). Además, cuando la modulación del host está activa, el cuadro combinado de fuente de micrófono se bloquea en "PC" con una información sobre herramientas que explica que solo la entrada de PC está disponible.

En la v26.8.4, el cuadro combinado de fuente de micrófono ahora se adapta inteligentemente a radios cuya entrada de audio de transmisión no puede seleccionarse desde este cliente. En dichas radios, el cuadro combinado se reduce a una única entrada "PC" con una información sobre herramientas que explica que la selección de entrada del propio radio se realiza en el radio. Esto evita la apariencia engañosa de entradas de micrófono seleccionables que se ignorarían silenciosamente. El cliente también aplica automáticamente el estado de selección de micrófono de PC al modelo de transmisión para mantenerlo sincronizado. Además, la detección del modo CW ahora reconoce correctamente todas las variantes de CW (CW, CWU, CWL) de cualquier radio, no solo el modo "CW" básico de Flex.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet de Phone/CW requiere una conexión de radio activa.
- Abra el Applet Panel. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: habilite el monitor de banda lateral

1. Haga clic en el botón de la bandeja P/CW en la barra lateral derecha para abrir el applet de Phone/CW.
2. Confirme que el applet muestra el panel de Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para habilitar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el control deslizante de volumen del monitor para establecer el nivel de reproducción (0–100).

### Modo Phone: ajuste la configuración del micrófono

1. Seleccione un perfil de micrófono del menú desplegable para cargar un perfil de procesamiento de micrófono con nombre.
2. Seleccione la fuente de micrófono del menú desplegable. En radios donde la entrada es seleccionable, las opciones incluyen MIC, BAL, LINE, ACC, PC, además de las entradas de micrófono disponibles del radio. Cuando la modulación del host está activa, el cuadro combinado se bloquea en "PC" con una información sobre herramientas que explica que solo la entrada de PC está disponible. En radios cuya entrada de audio de transmisión no puede seleccionarse desde este cliente (v26.8.4), el cuadro combinado se reduce a una única entrada "PC" con una información sobre herramientas que explica que la selección de entrada del propio radio se realiza en el radio.
3. Ajuste el control deslizante de ganancia del micrófono para establecer el nivel de entrada del micrófono (0–100). Cuando la fuente es PC, el valor se almacena localmente en `PcMicGain`.
4. Haga clic en +ACC para habilitar la mezcla de entrada del micrófono auxiliar.
5. Haga clic en PROC para alternar el procesador de voz.
6. Use el control deslizante NOR/DX/DX+ para seleccionar el nivel del procesador: 0 (NOR), 1 (DX) o 2 (DX+).
7. Haga clic en DAX para habilitar DAX como fuente de audio de TX.

### Modo CW: ajuste la configuración de CW

1. Cambie el slice activo a un modo CW (CW, CWU o CWL). El applet muestra automáticamente el panel de CW.
2. Ajuste el control deslizante de Delay para establecer el retardo de break-in de CW (0–2000 ms, paso de 10). También puede escribir un valor directamente en el QLineEdit (0–2000).
3. Ajuste el control deslizante de Speed para establecer la velocidad de tecleo de CW (5–100 WPM). También puede escribir un valor directamente en el QLineEdit (5–100).
4. Haga clic en Sidetone para habilitar el monitor de CW. El botón se resalta cuando está activo.
5. Ajuste el control deslizante de volumen del tono lateral para establecer el nivel (0–100). También puede escribir un valor directamente en el QLineEdit (0–100).
6. Use el control deslizante L / R pan (CW) para establecer el paneo estéreo (doble clic para re-centrar en 50).
7. Haga clic en Breakin para alternar el break-in completo (QSK).
8. Haga clic en Iambic para alternar el manipulador de paleta iámbica.
9. Use los botones Pitch < / > para avanzar en pasos de 10 Hz, o escriba un valor directamente en el QLineEdit (100–6000 Hz).

### Lectura de valores de indicadores con el mouse

1. Mueva el cursor del mouse sobre cualquier indicador (Level, Compression, ALC Phone, ALC CW).
2. Aparece una ventana emergente que muestra el valor numérico exacto con un decimal.
3. El indicador Level muestra el valor en dB (p. ej., "-12.3 dB").
4. El indicador Compression muestra la cantidad de compresión como un valor positivo en dB (p. ej., "15.0 dB" para -15 dB de compresión).
5. Los indicadores ALC muestran el valor en dBFS (p. ej., "-5.2 dBFS").

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                     | Predeterminado                                          |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MON                 | Habilita el monitor de banda lateral de TX (panel de Phone).                                                                                                                                                                                                                                                 | —                                                       |
| Monitor volume      | Establece el nivel de reproducción del monitor de banda lateral.                                                                                                                                                                                                                                             | —                                                       |
| DAX                 | Habilita DAX como fuente de audio de TX.                                                                                                                                                                                                                                                                     | —                                                       |
| Mic profile         | Carga un perfil de procesamiento de micrófono con nombre.                                                                                                                                                                                                                                                    | —                                                       |
| Mic source          | Selecciona la fuente de entrada del micrófono. Cuando la modulación del host está activa, el cuadro combinado se bloquea en "PC" con una información sobre herramientas que explica que solo la entrada de PC está disponible (v26.7.4). En radios cuya entrada de audio de transmisión no puede seleccionarse desde este cliente, el cuadro combinado se reduce a una única entrada "PC" con una información sobre herramientas que explica que la selección de entrada del propio radio se realiza en el radio (v26.8.4). | —                                                       |
| Mic gain            | Ajusta el nivel de entrada del micrófono. Para la fuente de PC usa la persistencia local de PcMicGain.                                                                                                                                                                                                       | 50                                                      |
| +ACC                | Habilita la mezcla de entrada del micrófono auxiliar.                                                                                                                                                                                                                                                        | —                                                       |
| PROC                | Alterna el procesador de voz.                                                                                                                                                                                                                                                                                | —                                                       |
| NOR/DX/DX+          | Control deslizante de nivel del procesador de tres posiciones.                                                                                                                                                                                                                                               | 0                                                       |
| Delay (CW)          | Establece el retardo de break-in de CW. El QLineEdit adyacente acepta valores escritos (0–2000) (v0.9.8, #2429). En v0.9.8, se corrigió setCwDelay para almacenar en caché el valor inmediatamente para que la emisión del radio no haga que el control deslizante vuelva a su posición anterior (#2428).                                                                   | 500 ms                                                  |
| Speed (CW)          | Establece la velocidad de tecleo de CW. El QLineEdit adyacente acepta valores escritos (5–100) (v0.9.8, #2429).                                                                                                                                                                                              | 20 WPM                                                  |
| Sidetone            | Alterna el monitor de tono lateral de CW. También habilita/deshabilita el CwSidetoneGenerator de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX del radio como el tono lateral local de PortAudio se controlan mediante este único botón. El tono y el paneo siempre siguen automáticamente la configuración cw_pitch y mon_pan_cw del radio. En v26.5.3, el audio del tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | —                                                       |
| Sidetone volume     | Establece el volumen del monitor de CW. También establece el volumen del generador de tono lateral local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100) (v0.9.8, #2429).                                                                                                                                                                    | 50                                                      |
| L / R pan (CW)      | Establece el paneo estéreo del monitor de CW. Aplica paneo de potencia constante al generador de tono lateral local (v0.9.1+). Doble clic para re-centrar en 50.                                                                                                                                              | 50                                                      |
| Breakin             | Alterna el break-in completo (QSK). En v0.9.7, las rutas de teclado/MIDI de CW ahora respetan completamente esta configuración: con Breakin activado (QSK), los flancos de tecla activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente.                                                     | —                                                       |
| Iambic              | Alterna el manipulador de paleta iámbica.                                                                                                                                                                                                                                                                    | —                                                       |
| Pitch < / >         | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz (v0.9.8, #2429).                                                                                                                                                                | 600 Hz                                                  |
| Level               | Nivel de pico de entrada del micrófono en dBFS (panel de Phone). Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                                                                                                                               | —                                                       |
| Compression         | Cantidad de compresión de voz en dB (panel de Phone). Puerta controlada por el estado TRANSMITTING del interbloqueo del radio y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, el valor del medidor de compresión se invierte: 0 dB = sin compresión, -25 dB = compresión completa.                                                         | —                                                       |
| ALC (panel de Phone)| Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico de SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado de HWALC (voltaje RCA) al medidor de ALC de software en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Reflejado por un indicador idéntico en el subpanel de CW. En v26.7.4, admite ventana emergente de valor al pasar el mouse para lectura exacta (#3936). | —                                                       |
| ALC (panel de CW)   | Refleja el indicador ALC del panel de Phone; ambos leen de MeterModel::swAlcChanged para lecturas coherentes entre voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio. En v26.7.4, admite ventana emergente de valor al pasar el mouse para lectura exacta (#3936). | —                                                       |

## Información de los medidores

| Medidor                | Qué muestra                                                                                                                               | Rango válido             | Notas                                                                                                                           |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Indicador Level        | Nivel de pico de entrada del micrófono en dBFS. El paso del mouse muestra el valor exacto con un decimal (v26.7.4, #3936).               | -40 a +10 dBFS (rojo > 0)| Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                                  |
| Indicador Compression  | Cantidad de compresión de voz en dB (relleno invertido). En v26.5.3, 0 dB = sin compresión, -25 dB = compresión completa. El paso del mouse muestra la cantidad de compresión como un valor positivo (v26.7.4, #3936). | -25 a 0 dB               | Puerta controlada por el estado TRANSMITTING del interbloqueo del radio y la habilitación del procesador de voz: lee 0 dB durante RX (v0.9.7). En v26.5.3, invertido respecto a versiones anteriores. |
| Indicador ALC (Phone)  | Control automático de nivel — pico de SSB posterior al ALC de software, leído de MeterModel::swAlcChanged. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El paso del mouse muestra el valor exacto con un decimal en dBFS (v26.7.4, #3936). | -20 a 0 dBFS (rojo > -3) | Reconectado de HWALC (voltaje RCA) al medidor de ALC de software en v26.5.1 (#2552). En v26.5.3, se inicializa a -20 dBFS al inicio. Reflejado por un indicador idéntico en el panel de CW. |
| Indicador ALC (CW)     | Reflejo del indicador ALC del panel de Phone, escalado idénticamente. Ambos leen de MeterModel::swAlcChanged. El paso del mouse muestra el valor exacto con un decimal en dBFS (v26.7.4, #3936).       | -20 a 0 dBFS (rojo > -3) | Añadido en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo HGauge::setFillFromRight. En v26.5.3, se inicializa a -20 dBFS al inicio. |

## Consejos

- El botón Sidetone y el control deslizante de volumen del tono lateral controlan ambas rutas de audio (monitor DAX del radio y generador del lado del cliente) juntos. No hay un control separado para habilitar o ajustar el tono lateral local de forma independiente.
- El tono siempre sigue automáticamente la configuración de tono de CW del radio. Use el widget Pitch < / > para cambiar el tono de CW del radio, y tanto el tono de decodificación como el tono lateral se actualizarán en consecuencia.
- El botón MON y el botón Sidetone son controles separados en paneles separados. MON se aplica a modos de voz; Sidetone se aplica a modo CW.
