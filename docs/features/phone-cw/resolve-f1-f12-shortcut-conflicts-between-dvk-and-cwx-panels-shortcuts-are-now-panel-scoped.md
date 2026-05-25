# Applet Phone/CW

El applet Phone/CW es un panel de transmisión sensible al modo que muestra controles de micrófono/procesador/monitor en modos de voz y cambia automáticamente a controles CW (retardo, velocidad, sintonía lateral, iámbico, tono) cuando el slice activo está en modo CW.

## Antes de comenzar

- El applet requiere una radio FLEX-8600 conectada con firmware 4.2
- El slice activo debe estar en modo de voz (para el panel Phone) o modo CW (para el panel CW)

## Abrir el applet

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW.
2. El applet cambia automáticamente entre los paneles Phone y CW según el modo del slice activo.

## Controles Phone

Cuando el slice activo está en un modo de voz, el applet muestra el panel Phone con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| Level | Medidor | -40 a +10 dBFS | Muestra el nivel pico de entrada del micrófono. Se suprime a -150 cuando met_in_rx está desactivado y no está transmitiendo. |
| Compression | Medidor | -25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz. Se activa con el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz. Lee 0 dB durante RX. En v26.5.3, el indicador de compresión ahora lee el valor COMPPEAK sin procesar (0–25 dB de compresión) y lo invierte para mostrarlo: 0 dB = sin compresión, -25 dB = compresión total. |
| Mic profile | Cuadro combinado | Se completa desde la radio | Carga el perfil de procesamiento de micrófono nombrado. |
| Mic source | Cuadro combinado | MIC, BAL, LINE, ACC, PC | Selecciona la fuente de entrada del micrófono. |
| Mic gain | Deslizador | 0–100 | Ajusta el nivel de entrada del micrófono. Para la fuente "PC" usa la persistencia local de PcMicGain. |
| +ACC | Conmutador | On/Off | Habilita la mezcla de entrada de micrófono de accesorio. |
| PROC | Conmutador | On/Off | Activa o desactiva el procesador de voz. |
| NOR/DX/DX+ | Deslizador | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones. |
| DAX | Conmutador | On/Off | Habilita DAX como fuente de audio de TX. |
| MON | Conmutador | On/Off | Habilita el monitor de sintonía lateral de TX. |
| Monitor volume | Deslizador | 0–100 | Ajusta el volumen del monitor de banda lateral. |
| ALC (panel Phone) | Medidor | -20 a 0 dBFS | Muestra el control automático de nivel desde el medidor ALC de software. Se llena de derecha a izquierda. |

## Controles CW

Cuando el slice activo está en modo CW, el applet muestra el panel CW con los siguientes controles:

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| Delay | Deslizador | 0–2000 ms (paso 10) | Establece el retardo de break-in CW. El QLineEdit adyacente acepta valores escritos (0–2000). |
| Speed | Deslizador | 5–100 WPM | Establece la velocidad de manipulación CW. El QLineEdit adyacente acepta valores escritos (5–100). |
| Sidetone | Conmutador | On/Off | Activa o desactiva el monitor de sintonía lateral CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de sintonía lateral de baja latencia del lado del cliente de forma sincronizada. En v26.5.3, la sintonía lateral CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). |
| Sidetone volume | Deslizador | 0–100 | Ajusta el volumen del monitor CW. El QLineEdit adyacente acepta valores escritos (0–100). |
| L / R pan | Deslizador | 0–100 | Ajusta la panorámica estéreo del monitor CW. El doble clic centra en 50 (centro). |
| Breakin | Conmutador | On/Off | Activa o desactiva el break-in completo (QSK). Respeta completamente la configuración break_in de la radio — no hay envolvente de PTT automático que fuerce TX. |
| Iambic | Conmutador | On/Off | Activa o desactiva el manipulador de paletas iámbico. |
| Pitch < / > | Campo de texto | 100–6000 Hz (paso 10) | QLineEdit con botones < / >. Escriba un valor o haga clic en los botones para aumentar/disminuir en pasos de 10 Hz. |
| ALC (panel CW) | Medidor | -20 a 0 dBFS | Refleja el medidor ALC del panel Phone. Ambos leen de MeterModel::swAlcChanged. |

## Controles comunes

| Control | Tipo | Rango | Comportamiento |
|---------|------|-------|---------------|
| ALC gauge | Medidor | -20 a 0 dBFS (llenado desde la derecha) | Muestra el control automático de nivel. Tanto el panel Phone como el CW muestran lecturas de ALC idénticas. En v26.5.3, ambos medidores ALC ahora se inicializan en -20 dBFS (vacío) en lugar de 0 dBFS (lleno) cuando el applet se abre por primera vez. |

## Alcance de los atajos F1-F12

- El panel CWX integrado limita sus atajos F1-F12 a la visibilidad del panel (#2464, #2469)
- Las asignaciones de teclas F del panel DVK y las teclas rápidas de CWX ya no se activan simultáneamente
- Las macros de CWX liberan automáticamente TX cuando la cola se vacía (#2450, #2507)

## Notas

- El medidor de nivel ahora se suprime correctamente durante la recepción cuando el usuario desactiva "Level Meter During Receive" (met_in_rx), independientemente de la fuente del micrófono. El método applyLevelMeterReceiveGate() maneja esto de manera consistente para todas las fuentes de micrófono, incluidas las rutas PC y RADE.
- El indicador de compresión en v26.5.3 lee el valor COMPPEAK sin procesar (0–25 dB de compresión) y lo invierte para mostrarlo: 0 dB = sin compresión, -25 dB = compresión total. Esto proporciona una representación más precisa de la cantidad de compresión real.
- Ambos medidores ALC ahora se inicializan en kAlcGaugeFloorDbfs (-20 dBFS) cuando el applet se construye por primera vez, evitando la visualización de lecturas obsoletas de 0 dBFS durante la fase de renderizado inicial.
