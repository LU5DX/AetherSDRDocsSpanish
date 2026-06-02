# Lea el medidor ALC de software (pico SSB posterior al ALC de software) en el panel de Phone o CW

Esta página le muestra cómo monitorear el medidor de Control Automático de Nivel (ALC) por software, el cual indica el pico SSB posterior al ALC de software en dBFS. Este medidor le ayuda a ajustar la ganancia de su micrófono o la envolvente de manipulación de CW para transmitir a un nivel adecuado sin sobreexcitar la cadena de audio.

## Antes de comenzar

- Asegúrese de que su FLEX-8600 esté conectado y que el slice activo esté en un modo de voz (Phone) o modo CW.
- El applet de Phone/CW debe estar visible en la barra lateral derecha — actívelo usando el botón de la bandeja **P/CW** si es necesario.

## Pasos

1. Localice el indicador **ALC** en el subpanel de Phone o CW. Su rango es de **-20 a 0 dBFS**, y se llena de derecha a izquierda.
2. Active el transmisor (o, para CW, comience a enviar).
3. Observe la aguja del indicador ALC mientras ajusta la ganancia de su micrófono con el deslizador **Mic gain**:
   - El medidor está vacío (en **-20 dBFS**) cuando no se aplica ALC.
   - El indicador se llena hacia **0 dBFS** a medida que el ALC aumenta.
   - La zona roja comienza en **-3 dBFS** (marcada en el indicador).
4. Para CW, el mismo indicador ALC aparece en el subpanel de CW — es idéntico y está controlado por la misma fuente del medidor.

## Qué hace cada control

| Control | Etiqueta | Comportamiento | Rango válido | Valor predeterminado | Clave de configuración |
|---------|----------|----------------|--------------|----------------------|------------------------|
| Indicador ALC (panel Phone) | **ALC** | Muestra la lectura de control automático de nivel del medidor ALC por software (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Zona roja por encima de -3 dBFS. Se inicializa a -20 dBFS al crearse. | -20 a 0 dBFS | — | Ninguna |
| Indicador ALC (panel CW) | **ALC** | Refleja el indicador ALC del panel Phone; ambos leen del mismo medidor ALC por software para lecturas coherentes entre voz y CW. Se inicializa a -20 dBFS al crearse. | -20 a 0 dBFS | — | Ninguna |

## Qué hace cada control de Phone/CW

| Control | Etiqueta | Comportamiento | Rango válido | Valor predeterminado | Clave de configuración |
|---------|----------|----------------|--------------|----------------------|------------------------|
| Medidor de nivel | **Level** | Muestra el nivel pico de entrada del micrófono en dBFS (panel Phone). Se suprime a -150 cuando **Level Meter During Receive** está desactivado y no se está transmitiendo. | -40 a +10 dBFS (rojo > 0) | — | Ninguna |
| Medidor de compresión | **Compression** | Muestra la cantidad de compresión de voz en dB (panel Phone). Se habilita con el estado de TRANSMISIÓN del interbloqueo de la radio y la habilitación del procesador de voz: lee 0 dB durante RX. Conversión: MeterModel expone COMPPEAK como positivo de 0..25 dB, el indicador muestra -25..0 dB invertido. | -25 a 0 dB (llenado invertido) | — | Ninguna |
| Perfil de micrófono | **Mic profile** | Carga un perfil de procesamiento de micrófono con nombre desde la radio. | Se obtiene de la lista micProfileList() de la radio | — | Ninguna |
| Fuente de micrófono | **Mic source** | Selecciona la fuente de entrada del micrófono. | MIC, BAL, LINE, ACC, PC (más cualquier otra de micInputList()) | — | Ninguna |
| Ganancia de micrófono | **Mic gain** | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain. | 0-100 | 50 | PcMicGain |
| +ACC | **+ACC** | Activa la mezcla de entrada del micrófono auxiliar. | — | — | Ninguna |
| PROC | **PROC** | Activa/desactiva el procesador de voz. | — | — | Ninguna |
| NOR/DX/DX+ | **NOR/DX/DX+** | Nivel del procesador de tres posiciones. | 0 (NOR), 1 (DX), 2 (DX+) | 0 | Ninguna |
| DAX | **DAX** | Activa DAX como fuente de audio de TX. | — | — | Ninguna |
| MON | **MON** | Activa el monitor de tono lateral de TX. | — | — | Ninguna |
| Volumen del monitor | **Monitor volume** | Ajusta el volumen del monitor de banda lateral. | 0-100 | — | Ninguna |
| Indicador ALC (panel Phone) | **ALC** | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Se inicializa a -20 dBFS al crearse. | -20 a 0 dBFS (rojo > -3) | — | Ninguna |
| Retardo (CW) | **Delay (CW)** | Establece el retardo de ruptura de CW. El QLineEdit adyacente acepta valores escritos (0–2000). | 0-2000 ms (paso 10) | 500 | Ninguna |
| Velocidad (CW) | **Speed (CW)** | Establece la velocidad de manipulación de CW. El QLineEdit adyacente acepta valores escritos (5–100). | 5-100 WPM | 20 | Ninguna |
| Tono lateral | **Sidetone** | Activa/desactiva el monitor de tono lateral de CW y el CwSidetoneGenerator local de baja latencia del lado del cliente de forma sincronizada. Se dirige a la salida de audio seleccionada por el usuario. | — | — | Ninguna |
| Volumen del tono lateral | **Sidetone volume** | Establece el volumen del monitor de CW. Controla tanto el volumen del lado de la radio (mon_gain_cw) como el del tono lateral del lado del cliente. El QLineEdit adyacente acepta valores escritos (0–100). | 0-100 | 50 | Ninguna |
| Pan L / R (CW) | **L / R pan (CW)** | Establece la panorámica estéreo del monitor de CW. Aplica panorámica de potencia constante al generador de tono lateral local. Haga doble clic para centrar en 50 (centro). | 0-100 | 50 | Ninguna |
| Ruptura | **Breakin** | Activa/desactiva la ruptura completa (QSK). Con Breakin activado, los bordes de la tecla activan TX; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | — | — | Ninguna |
| Iámbico | **Iambic** | Activa/desactiva el manipulador de paletas iámbico. | — | — | Ninguna |
| Tono < / > | **Pitch < / >** | QLineEdit con botones < / >. Escriba un valor (100–6000) o haga clic en los botones para aumentar/disminuir en pasos de 10 Hz. | 100-6000 Hz (paso 10) | 600 | Ninguna |
| Indicador ALC (panel CW) | **ALC** | Refleja el indicador ALC del panel Phone; controlado por el mismo medidor ALC por software. Se inicializa a -20 dBFS al crearse. | -20 a 0 dBFS (rojo > -3) | — | Ninguna |

## Notas

- En la versión 26.5.3, ambos indicadores ALC se inicializan a -20 dBFS al crearse, lo que evita una lectura momentánea a escala completa al iniciar.
- El indicador de compresión en la versión 26.5.3 usa el valor COMPPEAK de MeterModel (positivo de 0..25 dB) y lo invierte para la visualización invertida del indicador de -25..0 dB.
- La lógica de supresión del medidor de nivel se ha refactorizado en la versión 26.5.3 en un método dedicado `applyLevelMeterReceiveGate()`, llamado cuando cambia el estado de transmisión o el estado activo de RADE.
- En la versión 26.6.1, el estilo de los deslizadores se actualizó para usar el sistema de temas en lugar de valores de color codificados. Todos los deslizadores del applet Phone/CW ahora respetan el tema actual.

## Relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla auxiliar](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Establecer la velocidad de manipulación de CW en WPM](set-cw-keying-speed-in-wpm.md)
