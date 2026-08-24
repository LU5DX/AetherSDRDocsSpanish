# Habilitar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz integrado del FLEX-8600 y elija con qué agresividad comprime el audio transmitido. NOR ofrece compresión leve; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice activo debe estar en un modo de teléfono (USB, LSB, AM, etc.). El applet Phone/CW muestra los controles de Phone solo cuando el slice activo no está en modo CW.
- Abra el applet Phone/CW haciendo clic en el botón de la bandeja **P/CW** en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, compresión mínima)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (compresión máxima)
3. Observe el medidor **Compression**. El relleno invertido muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo. Pase el cursor sobre el medidor para ver el valor exacto de compresión en dB.
4. Observe el medidor **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el medidor se pone en rojo por encima de 0 dBFS. Pase el cursor sobre el medidor para ver el nivel máximo exacto del micrófono en dB.
5. Observe el medidor **ALC** (panel de Phone) para confirmar que el nivel posterior al ALC de software está en el rango operativo normal (−20 a 0 dBFS). El medidor se llena desde la derecha; un ALC excesivo se fija en 0 dBFS. Pase el cursor sobre el medidor para ver el nivel exacto de ALC en dBFS.
6. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado sin iluminación.

## Qué hace cada control

| Control           | Tipo                                                                                                                              | Predeterminado                                                                                                             |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **PROC**          | Botón de alternancia                                                                                                                                                     | Off                                                                                                                      |
| **NOR/DX/DX+**    | Control deslizante                                                                                                                                                            | 0 (NOR)                                                                                                                  |
| **Level**         | Medidor                                                                                                                                                             | —                                                                                                                        |
| **Compression**   | Medidor                                                                                                                                                             | —                                                                                                                        |
| **ALC (panel de Phone)** | Medidor que muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a −20 dBFS, lleno a 0 dBFS. Pase el cursor para obtener la lectura exacta en dBFS. | Reconfigurado de HWALC (voltaje RCA) a medidor de ALC de software en v26.5.1 (#2552). Reflejado por un medidor idéntico en el subpanel de CW. |
| **ALC (panel de CW)**    | Medidor que refleja el medidor de ALC del panel de Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Se llena de derecha a izquierda: vacío a −20 dBFS, lleno a 0 dBFS. Pase el cursor para obtener la lectura exacta en dBFS. | Añadido en v26.5.1 (#2552) como parte de la división del medidor de ALC de software. Usa el modo HGauge::setFillFromRight. |

## Todos los controles del applet

| Control               | Tipo          | Predeterminado | Rango válido       | Comportamiento |
|-----------------------|---------------|---------|-------------------|----------|
| **Level**             | Medidor         | —       | −40 a +10 dBFS (rojo > 0) | Muestra el nivel máximo de entrada del micrófono en dBFS. Se suprime a −150 cuando met_in_rx está desactivado y no se está transmitiendo. Pase el cursor para ver la lectura exacta en dB (v26.7.4). Oculto cuando la radio toma el audio de transmisión de este equipo y su propia selección de entrada se realiza en la radio (v26.8.4). |
| **Compression**       | Medidor         | —       | −25 a 0 dB (relleno invertido) | Muestra la cantidad de compresión de voz en dB. En v0.9.7, controlado por el estado TRANSMITTING del interlock de la radio y la activación del procesador de voz: lee 0 dB durante RX. Pase el cursor para ver la lectura exacta en dB (v26.7.4). |
| **Perfil de micrófono**       | Cuadro combinado     | —       | Se rellena desde micProfileList() de la radio | Carga el perfil de procesamiento de micrófono nombrado. |
| **Fuente de micrófono**        | Cuadro combinado     | —       | MIC, BAL, LINE, ACC, PC (más cualquier valor de micInputList()) | Selecciona la fuente de entrada del micrófono. Cuando la modulación del host está activa (la radio es modulada por AetherSDR), el cuadro combinado está deshabilitado y muestra solo "PC" con una información sobre herramientas explicativa. Cuando la radio toma el audio de transmisión de este equipo y su propia selección de entrada se realiza en la radio (v26.8.4), el cuadro combinado muestra solo "PC" y está deshabilitado, y el modelo se fuerza a informar "PC" para que radiocert no advierta sobre la falta de captura de audio de transmisión. |
| **Ganancia de micrófono**          | Control deslizante        | 50      | 0–100           | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain. En v26.8.4, micLevelChanged solo se emite cuando el cliente posee la ganancia: modo RADE, o entradas de micrófono seleccionables con PC seleccionado. |
| **+ACC**              | Botón de alternancia | —       | —               | Activa la mezcla de entrada del micrófono accesorio. |
| **PROC**              | Botón de alternancia | —       | —               | Alterna el procesador de voz. |
| **NOR/DX/DX+**        | Control deslizante        | 0       | 0 (NOR), 1 (DX), 2 (DX+) | Nivel de procesador de tres posiciones. |
| **DAX**               | Botón de alternancia | —       | —               | Activa DAX como fuente de audio TX. Oculto cuando la radio toma el audio de transmisión de este equipo (v26.8.4). |
| **MON**               | Botón de alternancia | —       | —               | Activa el monitor de sintonía lateral de TX. |
| **Volumen del monitor**    | Control deslizante        | —       | 0–100           | Establece el volumen del monitor de banda lateral. |
| **ALC (panel de Phone)** | Medidor         | —       | −20 a 0 dBFS (rojo > −3) | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged. Se llena de derecha a izquierda. Pase el cursor para ver la lectura exacta en dBFS (v26.7.4). |
| **ALC (panel de CW)**    | Medidor         | —       | −20 a 0 dBFS (rojo > −3) | Refleja el medidor de ALC del panel de Phone. Se llena de derecha a izquierda. Pase el cursor para ver la lectura exacta en dBFS (v26.7.4). |
| **Delay (CW)**        | Control deslizante + edición | 500     | 0–2000 ms        | Establece el retardo de break-in de CW. El QLineEdit adyacente acepta valores escritos (0–2000). |
| **Speed (CW)**        | Control deslizante + edición | 20      | 5–100 WPM        | Establece la velocidad de tecleo CW. El QLineEdit adyacente acepta valores escritos (5–100). |
| **Sidetone**          | Botón de alternancia | —       | —               | Alterna el monitor de sintonía lateral de CW. También activa/desactiva en sincronía el CwSidetoneGenerator de baja latencia del lado del cliente. |
| **Volumen del sidetone**   | Control deslizante + edición | 50      | 0–100           | Establece el volumen del monitor de CW. También establece en sincronía el volumen del generador de sintonía lateral local. El QLineEdit adyacente acepta valores escritos (0–100). |
| **Pan L / R (CW)**    | Control deslizante        | 50      | 0–100           | Establece el paneo estéreo del monitor de CW. Doble clic para centrar en 50 (centro). |
| **Breakin**           | Botón de alternancia | —       | —               | Alterna el break-in completo (QSK). En v0.9.7, respeta completamente el ajuste break_in de la radio. |
| **Iambic**            | Botón de alternancia | —       | —               | Alterna el manipulador de paleta iámbica. |
| **Pitch < / >**       | Texto + botones| 600     | 100–6000 Hz      | QLineEdit con botones < / >. Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable de **Level** antes de activar **PROC** le da al procesador una señal útil con la que trabajar. Consulte [Adjust mic gain and enable the accessory mix](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y cambie a **DX** o **DX+** solo si los reportes de señal lo justifican. El procesamiento intenso en señales fuertes suena distorsionado para la estación receptora.
- El medidor **Compression** lee 0 dB (sin relleno) cuando **PROC** está desactivado, cuando la radio no está transmitiendo, o cuando no hay audio presente.
- Ambos medidores **ALC** (paneles de Phone y CW) usan la misma fuente de medidor de ALC de software. Para operación SSB, apunte a −10 a −5 dBFS en el medidor de ALC para una calidad de audio de transmisión óptima.
- Pase el cursor sobre cualquier medidor (**Level**, **Compression** o cualquiera de los medidores **ALC**) para ver la lectura numérica exacta en una ventana emergente (v26.7.4). Esto le permite leer el valor preciso sin tener que estimar la posición del relleno del medidor.
- Si la radio toma el audio de transmisión de este equipo (v26.8.4), el medidor **Level** y el botón **DAX** están ocultos, y **Fuente de micrófono** muestra solo "PC" con una información sobre herramientas. Esto se aplica a radios cuya selección de entrada de audio se realiza en la propia radio.

## Solución de problemas

- **El botón PROC no está visible** — El applet está mostrando el panel de CW. El panel de Phone, incluido **PROC**, aparece solo cuando el slice activo está en un modo de teléfono, no en CW.
- **El medidor Compression muestra 0 dB con PROC activado** — En v0.9.7 y posteriores, el medidor **Compression** está controlado por el estado TRANSMITTING del interlock de la radio: lee intencionalmente 0 dB durante la recepción para evitar lecturas obsoletas de la cadena TX. Si el medidor aún lee 0 dB mientras transmite, la radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el medidor **Level** y el ajuste **Fuente de micrófono**. Si **Fuente de micrófono** es **PC**, la radio siempre reporta el nivel de micrófono como 0; use el medidor **Level** en el applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su posición** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Arrastrar entre los puntos de ajuste hace que aterrice en el entero más cercano; este es el comportamiento esperado.
- **El cuadro combinado de Fuente de micrófono está deshabilitado y muestra solo "PC"** — Esto ocurre cuando la radio está en modo de modulación del host (modulada por AetherSDR). El micrófono de PC es la única entrada disponible en este modo; otras fuentes son conectores de FlexRadio que no se aplican. Una información sobre herramientas lo explica. En v26.8.4, esto también ocurre en radios cuya selección de entrada de audio se realiza en la propia radio, donde "PC" indica que la radio toma el audio de transmisión de este equipo. En tales radios, la información sobre herramientas dice: "Esta radio toma el audio de transmisión de este equipo. Su propia selección de entrada se realiza en la radio."
- **El medidor Level no aparece al conectar** — Si **Fuente de micrófono** es **PC**, el medidor **Level** aparece inmediatamente al conectar sin requerir transmisión o que `met_in_rx` esté activo (v0.9.3, corrección #2086). Cuando el modo RADE está activo, el medidor **Level** también aparece durante la recepción (consulte [Comportamiento del medidor Level](#level-gauge-behavior-v093)). Si el medidor aún está ausente, verifique que **Fuente de micrófono** esté configurado en **PC** y que AetherSDR haya terminado de conectarse a la radio. En v26.8.4, el medidor **Level** está intencionalmente oculto en radios que toman el audio de transmisión de este equipo.
- **El panel de Phone no se actualiza cuando VOX se alterna con un atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel de Phone no se actualiza inmediatamente cuando VOX se alterna mediante un atajo de teclado.
- **El medidor ALC muestra valores inesperados** — Los medidores de ALC ahora leen del medidor de ALC de software (MeterModel::swAlcChanged) en rangos de dBFS. Los valores fuera de −20 a 0 dBFS no se muestran; el medidor simplemente se fija en el extremo más cercano. Esto reemplaza la ruta HWALC anterior que producía lecturas sin significado.
- **El botón DAX está oculto** — En radios que toman el audio de transmisión de este equipo (v26.8.4), el botón **DAX** está oculto porque DAX no es la ruta de audio. Si necesita usar DAX, conéctese a una radio cuya selección de entrada de audio se realice en la propia radio.

## Controles del panel de CW (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor para los parámetros de CW se reemplazaron con widgets QLineEdit. Los controles deslizantes y botones adyacentes permanecen sin cambios. Haga clic en cualquier valor y escriba un número directamente para configurarlo. Los valores se limitan al rango válido cuando presiona Enter o Tab.

| Control               | Tipo          | Predeterminado | Rango válido       |
|-----------------------|---------------|---------|-------------------|
| **Delay (CW)**        | Control deslizante + edición | 500     | 0–2000 ms         |
| **Speed (CW
