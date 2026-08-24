# Lea el medidor de ALC de software (pico SSB posterior al ALC de software) en el panel de Phone o CW

El indicador **ALC** en el subpanel de Phone o CW muestra el pico SSB posterior al ALC de software en dBFS. Este medidor le ayuda a configurar la ganancia de su micrófono o la envolvente de manipulación CW para transmitir a un nivel adecuado sin sobrecargar la cadena de audio.

## Qué hace cada control

| Control | Etiqueta | Comportamiento | Rango válido | Predeterminado | Clave de configuración |
|---------|----------|----------------|--------------|----------------|------------------------|
| Indicador ALC (panel Phone) | **ALC** | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Zona roja por encima de -3 dBFS. Se inicializa a -20 dBFS al construirse. Pase el cursor sobre el indicador para ver la lectura exacta en dBFS. | -20 a 0 dBFS | — | Ninguna |
| Indicador ALC (panel CW) | **ALC** | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Se inicializa a -20 dBFS al construirse. Pase el cursor sobre el indicador para ver la lectura exacta en dBFS. | -20 a 0 dBFS | — | Ninguna |

## Qué hace cada control de Phone/CW

| Control | Etiqueta | Comportamiento | Rango válido | Predeterminado | Clave de configuración |
|---------|----------|----------------|--------------|----------------|------------------------|
| Medidor de nivel | **Level** | Muestra el nivel pico de entrada del micrófono en dBFS (panel Phone). Se suprime a -150 cuando **Level Meter During Receive** está desactivado y no se está transmitiendo. Pase el cursor sobre el indicador para ver la lectura exacta en dB. | -40 a +10 dBFS (rojo > 0) | — | Ninguna |
| Medidor de compresión | **Compression** | Muestra la cantidad de compresión de voz en dB (panel Phone). Se habilita con el estado de interbloqueo TRANSMITTING de la radio y la activación del procesador de voz: lee 0 dB durante RX. Conversión: MeterModel expone COMPPEAK como positivo de 0 a 25 dB; el indicador muestra invertido de -25 a 0 dB. Pase el cursor sobre el indicador para ver la lectura positiva exacta en dB. | -25 a 0 dB (llenado invertido) | — | Ninguna |
| Perfil de micrófono | **Mic profile** | Carga un perfil de procesamiento de micrófono con nombre desde la radio. | Se completa desde radio micProfileList() | — | Ninguna |
| Fuente de micrófono | **Mic source** | Selecciona la fuente de entrada del micrófono. Cuando la radio es modulada por AetherSDR (modulación de host habilitada), este control se deshabilita y se fija en **PC** únicamente, con una información sobre herramientas que explica que otras fuentes son tomas de FlexRadio. Si el audio de transmisión de la radio se suministra desde la computadora y el cliente no puede seleccionar la entrada (p. ej., una radio cuya propia selección de entrada se realiza en la radio), el cuadro combinado se limita a **PC** únicamente con una información sobre herramientas que explica que esta radio toma el audio de transmisión desde la computadora. | MIC, BAL, LINE, ACC, PC (además de cualquier valor de micInputList()) | — | Ninguna |
| Ganancia de micrófono | **Mic gain** | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain. Cuando el cliente posee la ganancia de micrófono (RADE activo, o una radio cuya selección de entrada está fijada en PC), el valor se emite localmente; de lo contrario, se envía a la radio. | 0-100 | 50 | PcMicGain |
| +ACC | **+ACC** | Habilita la mezcla de entrada de micrófono de accesorios. | — | — | Ninguna |
| PROC | **PROC** | Alterna el procesador de voz. | — | — | Ninguna |
| NOR/DX/DX+ | **NOR/DX/DX+** | Nivel del procesador de tres posiciones. | 0 (NOR), 1 (DX), 2 (DX+) | 0 | Ninguna |
| DAX | **DAX** | Habilita DAX como fuente de audio de TX. Se oculta cuando la radio no admite audio de TX por DAX. | — | — | Ninguna |
| MON | **MON** | Habilita el monitor de tono lateral de TX. | — | — | Ninguna |
| Volumen del monitor | **Monitor volume** | Configura el volumen del monitor de banda lateral. | 0-100 | — | Ninguna |
| Indicador ALC (panel Phone) | **ALC** | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Zona roja por encima de -3 dBFS. Se inicializa a -20 dBFS al construirse. Pase el cursor sobre el indicador para ver la lectura exacta en dBFS. | -20 a 0 dBFS (rojo > -3) | — | Ninguna |
| Retardo (CW) | **Delay (CW)** | Configura el retardo de break-in en CW. El QLineEdit adyacente acepta valores escritos (0–2000). | 0-2000 ms (paso 10) | 500 | Ninguna |
| Velocidad (CW) | **Speed (CW)** | Configura la velocidad de manipulación CW. El QLineEdit adyacente acepta valores escritos (5–100). | 5-100 WPM | 20 | Ninguna |
| Tono lateral | **Sidetone** | Alterna el monitor de tono lateral CW y el CwSidetoneGenerator de baja latencia del lado del cliente en sincronía. Se enruta a la salida de audio seleccionada por el usuario. | — | — | Ninguna |
| Volumen del tono lateral | **Sidetone volume** | Configura el volumen del monitor CW. Controla tanto el volumen del lado de la radio (mon_gain_cw) como el del tono lateral del cliente. El QLineEdit adyacente acepta valores escritos (0–100). | 0-100 | 50 | Ninguna |
| Panorámica L / R (CW) | **L / R pan (CW)** | Configura la panorámica estéreo del monitor CW. Aplica panorámica de potencia constante al generador de tono lateral local. Doble clic centra en 50 (centro). | 0-100 | 50 | Ninguna |
| Breakin | **Breakin** | Alterna el break-in completo (QSK). Con Breakin activado, los bordes de manipulación activan TX; con Breakin desactivado, las manipulaciones se ponen en cola y el operador activa PTT manualmente. | — | — | Ninguna |
| Iámbico | **Iambic** | Alterna el manipulador de paleta iámbico. | — | — | Ninguna |
| Pitch < / > | **Pitch < / >** | QLineEdit con botones < / >. Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. | 100-6000 Hz (paso 10) | 600 | Ninguna |
| Indicador ALC (panel CW) | **ALC** | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Se inicializa a -20 dBFS al construirse. Pase el cursor sobre el indicador para ver la lectura exacta en dBFS. | -20 a 0 dBFS (rojo > -3) | — | Ninguna |

## Notas

- **Detección de modo (v26.8.4):** El applet ahora usa un único auxiliar `isCwMode()` para detectar slices en modo CW. Una Flex informa "CW" simple; un Icom y un HL2 escriben el mismo modo como CWU, y CWL es el de lado inverso. Los tres activan el subpanel CW.
- **Fuente de micrófono en radios que el cliente no puede seleccionar (v26.8.4):** Cuando la radio toma el audio de transmisión desde la computadora y el cliente no puede elegir la entrada (la selección de entrada propia de la radio se realiza en la radio), el cuadro combinado **Mic source** se reconstruye solo con **PC** listado, deshabilitado y con una información sobre herramientas: "Esta radio toma el audio de transmisión de esta computadora. Su propia selección de entrada se realiza en la radio." Se le indica al modelo que la selección de micrófono es **PC** para que radiocert no advierta que la captura de audio de transmisión no está en ejecución en una radio donde simplemente así es como llega el audio.
- **Propiedad de la ganancia de micrófono (v26.8.4):** El cliente posee la ganancia de micrófono cuando RADE está activo, o cuando la selección de entrada de la radio está fijada en PC. En esos casos, el valor de ganancia se emite localmente. De lo contrario, se envía a la radio.
- **Visibilidad del medidor de nivel (v26.8.4):** El indicador Level se oculta cuando la radio no informa un medidor de nivel de micrófono.
- **Visibilidad de DAX (v26.8.4):** La alternancia **DAX** se oculta cuando la radio no admite audio de TX por DAX, y cuando está oculta se fuerza a desactivada.
- **Fuente del medidor ALC (v26.5.1, #2552):** Ambos indicadores ALC leen MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS), reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin significado.
- En v26.5.3 ambos indicadores ALC se inicializan a -20 dBFS al construirse, evitando una lectura momentánea de escala completa al inicio.
- El indicador de compresión en v26.5.3 usa el valor COMPPEAK de MeterModel (positivo de 0 a 25 dB) y lo invierte para la visualización invertida del indicador de -25 a 0 dB.
- La lógica de supresión del medidor de nivel fue refactorizada en v26.5.3 en un método dedicado `applyLevelMeterReceiveGate()`, llamado cuando cambia el estado de transmisión o el estado activo de RADE.
- En v26.6.1 el estilo de los controles deslizantes se actualizó para usar el sistema de temas en lugar de valores de color codificados. Todos los controles deslizantes del applet Phone/CW ahora respetan el tema actual.
- En v26.7.4 los indicadores Level, Compression y ALC obtuvieron ventanas emergentes al pasar el cursor que muestran la lectura exacta del medidor en dB o dBFS. Pase el cursor sobre cualquier indicador durante la transmisión para leer el valor preciso.
- En v26.7.4 el cuadro combinado Mic source se deshabilita automáticamente y se fija en **PC** cuando la radio es modulada por AetherSDR (modulación de host habilitada), con una información sobre herramientas que explica el motivo.

## Relacionado

- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Configurar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
