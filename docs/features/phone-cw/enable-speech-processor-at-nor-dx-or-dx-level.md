# Habilitar el procesador de voz en nivel NOR, DX o DX+

Active el procesador de voz incorporado del FLEX-8600 y elija qué tan agresivamente comprime el audio transmitido. NOR ofrece compresión suave; DX y DX+ aumentan el procesamiento para contactos con señales más débiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- La porción activa debe estar en un modo de telefonía (USB, LSB, AM, etc.). El applet de Phone/CW muestra los controles de Phone solo cuando la porción activa no está en modo CW.
- Abra el applet de Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet de Phone/CW, haga clic en **PROC** para activar el procesador de voz. El botón se ilumina en verde cuando está activo.
2. Arrastre el control deslizante **NOR/DX/DX+** al nivel de compresión deseado:
   - Posición 0 — **NOR** (normal, menor compresión)
   - Posición 1 — **DX**
   - Posición 2 — **DX+** (mayor compresión)
3. Observe el indicador **Compression**. El relleno inverso muestra cuántos dB de compresión se están aplicando (rango: −25 a 0 dB). Mantenga la lectura fuera del extremo izquierdo para evitar un procesamiento excesivo. Pase el cursor sobre el indicador para ver el valor exacto de compresión en dB.
4. Observe el indicador **Level** para confirmar que la entrada del micrófono está llegando al procesador. El rango es de −40 a +10 dBFS; el medidor se vuelve rojo por encima de 0 dBFS. Pase el cursor sobre el indicador para ver el nivel máximo del micrófono en dB.
5. Observe el indicador **ALC** (panel de Phone) para confirmar que el nivel posterior al ALC por software está en el rango operativo normal (−20 a 0 dBFS). El indicador se llena desde la derecha; el ALC excesivo se fija en 0 dBFS. Pase el cursor sobre el indicador para ver el nivel exacto de ALC en dBFS.
6. Para desactivar el procesador, haga clic en **PROC** nuevamente. El botón vuelve a su estado sin iluminación.

## Qué hace cada control

| Control           | Tipo                                                                                                                                                              | Valor predeterminado                                                                                                      |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **PROC**          | Botón de alternancia                                                                                                                                              | Desactivado                                                                                                               |
| **NOR/DX/DX+**    | Control deslizante                                                                                                                                                | 0 (NOR)                                                                                                                   |
| **Level**         | Indicador                                                                                                                                                         | —                                                                                                                         |
| **Compression**   | Indicador                                                                                                                                                         | —                                                                                                                         |
| **ALC (panel Phone)** | Indicador que muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor para una lectura exacta en dBFS. | Reconfigurado desde HWALC (voltaje RCA) al medidor ALC por software en v26.5.1 (#2552). Es reflejado por un indicador idéntico en el subpanel CW. |
| **ALC (panel CW)**    | Indicador que refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Pase el cursor para una lectura exacta en dBFS. | Añadido en v26.5.1 (#2552) como parte de la división del medidor ALC por software. Usa el modo HGauge::setFillFromRight.                          |

## Todos los controles del applet

| Control               | Tipo          | Valor predeterminado | Rango válido       | Comportamiento |
|-----------------------|---------------|---------|-------------------|----------|
| **Level**             | Indicador     | —       | −40 a +10 dBFS (rojo > 0) | Muestra el nivel máximo de entrada del micrófono en dBFS. Suprimido a −150 cuando met_in_rx está desactivado y no se transmite. Pase el cursor para una lectura exacta en dB (v26.7.4). |
| **Compression**       | Indicador     | —       | −25 a 0 dB (relleno inverso) | Muestra la cantidad de compresión de voz en dB. En v0.9.7, está controlado por el estado de TRANSMITTING del entrelazado de la radio y la activación del procesador de voz: lee 0 dB durante RX. Pase el cursor para una lectura exacta en dB (v26.7.4). |
| **Perfil de micrófono** | Cuadro combinado | —       | Poblado desde radio micProfileList() | Carga el perfil de procesamiento de micrófono nombrado. |
| **Fuente de micrófono** | Cuadro combinado | —       | MIC, BAL, LINE, ACC, PC (más cualquier valor de micInputList()) | Selecciona la fuente de entrada del micrófono. Cuando la modulación de host está activa (la radio es modulada por AetherSDR), el cuadro combinado está deshabilitado y solo muestra "PC" con un tooltip explicativo. |
| **Ganancia de micrófono** | Control deslizante | 50      | 0–100           | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local de PcMicGain. |
| **+ACC**              | Botón de alternancia | —       | —               | Activa la mezcla de entrada del micrófono auxiliar. |
| **PROC**              | Botón de alternancia | —       | —               | Activa o desactiva el procesador de voz. |
| **NOR/DX/DX+**        | Control deslizante | 0       | 0 (NOR), 1 (DX), 2 (DX+) | Nivel del procesador de tres posiciones. |
| **DAX**               | Botón de alternancia | —       | —               | Activa DAX como fuente de audio TX. |
| **MON**               | Botón de alternancia | —       | —               | Activa el monitor de señal lateral TX. |
| **Volumen del monitor** | Control deslizante | —       | 0–100           | Establece el volumen del monitor de banda lateral. |
| **ALC (panel Phone)** | Indicador     | —       | −20 a 0 dBFS (rojo > −3) | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged. Se llena de derecha a izquierda. Pase el cursor para una lectura exacta en dBFS (v26.7.4). |
| **ALC (panel CW)**    | Indicador     | —       | −20 a 0 dBFS (rojo > −3) | Refleja el indicador ALC del panel Phone. Se llena de derecha a izquierda. Pase el cursor para una lectura exacta en dBFS (v26.7.4). |
| **Retardo (CW)**      | Control deslizante + edición | 500     | 0–2000 ms        | Establece el retardo de break-in CW. El QLineEdit adyacente acepta valores escritos (0–2000). |
| **Velocidad (CW)**    | Control deslizante + edición | 20      | 5–100 WPM        | Establece la velocidad de manipulación CW. El QLineEdit adyacente acepta valores escritos (5–100). |
| **Señal lateral**     | Botón de alternancia | —       | —               | Activa o desactiva el monitor de señal lateral CW. También activa/desactiva el generador de señal lateral de baja latencia del lado del cliente (CwSidetoneGenerator) de forma sincronizada. |
| **Volumen de señal lateral** | Control deslizante + edición | 50      | 0–100           | Establece el volumen del monitor CW. También establece el volumen del generador de señal lateral local de forma sincronizada. El QLineEdit adyacente acepta valores escritos (0–100). |
| **Pan L / R (CW)**    | Control deslizante | 50      | 0–100           | Establece el paneo estéreo del monitor CW. Haga doble clic para centrar en 50 (centro). |
| **Breakin**           | Botón de alternancia | —       | —               | Activa o desactiva el break-in completo (QSK). En v0.9.7, respeta completamente la configuración break_in de la radio. |
| **Iambic**            | Botón de alternancia | —       | —               | Activa o desactiva el manipulador de paletas iámbicas. |
| **Pitch < / >**       | Texto + botones| 600     | 100–6000 Hz      | QLineEdit con botones < / >. Escriba un valor (100–6000) o haga clic en los botones para avanzar de a 10 Hz. |

## Consejos

- Ajuste la ganancia del micrófono antes de activar el procesador. Una lectura saludable de **Level** antes de activar **PROC** le proporciona al procesador una señal útil para trabajar. Consulte [Ajustar la ganancia del micrófono y activar la mezcla auxiliar](adjust-mic-gain-and-enable-the-accessory-mix.md).
- Comience en **NOR** y pase a **DX** o **DX+** solo si los informes de señal lo justifican. Un procesamiento intenso en señales fuertes suena distorsionado para la estación receptora.
- El indicador **Compression** lee 0 dB (sin relleno) cuando **PROC** está desactivado, cuando la radio no está transmitiendo o cuando no hay audio presente.
- Ambos indicadores **ALC** (paneles Phone y CW) usan la misma fuente de medidor ALC por software. Para operación SSB, apunte a −10 a −5 dBFS en el indicador ALC para una calidad de audio de transmisión óptima.
- Pase el cursor sobre cualquier indicador (**Level**, **Compression** o cualquiera de los **ALC**) para ver la lectura numérica exacta en una ventana emergente (v26.7.4). Esto le permite leer el valor preciso sin tener que estimar la posición de llenado del indicador.

## Solución de problemas

- **El botón PROC no es visible** — El applet está mostrando el panel CW. El panel Phone, incluido **PROC**, aparece solo cuando la porción activa está en un modo de telefonía, no CW.
- **El indicador Compression muestra 0 dB con PROC activado** — En v0.9.7 y posteriores, el indicador **Compression** está controlado por el estado de TRANSMITTING del entrelazado de la radio: intencionalmente lee 0 dB durante la recepción para evitar lecturas obsoletas de la cadena TX. Si el indicador aún lee 0 dB mientras transmite, la radio no está recibiendo audio de la fuente de micrófono seleccionada. Verifique el indicador **Level** y la configuración de **Fuente de micrófono**. Si **Fuente de micrófono** es **PC**, la radio siempre informa el nivel de micrófono como 0; use el indicador **Level** en el applet en su lugar.
- **El control deslizante NOR/DX/DX+ vuelve a su lugar** — El control deslizante tiene tres posiciones válidas (0, 1, 2). Arrastrar entre los puntos de encaje hace que aterrice en el entero más cercano; este es el comportamiento esperado.
- **El cuadro combinado de fuente de micrófono está deshabilitado y solo muestra "PC"** — Esto ocurre cuando la radio está en modo de modulación de host (modulada por AetherSDR). El micrófono de la PC es la única entrada disponible en este modo; otras fuentes son conectores FlexRadio que no aplican. Un tooltip lo explica.
- **El indicador Level no aparece al conectar** — Si **Fuente de micrófono** es **PC**, el indicador **Level** aparece inmediatamente al conectar sin requerir una transmisión o que `met_in_rx` esté activo (v0.9.3, corrección #2086). Cuando el modo RADE está activo, el indicador **Level** también aparece durante la recepción (consulte [Comportamiento del indicador Level](#level-gauge-behavior-v093)). Si el indicador aún está ausente, verifique que **Fuente de micrófono** esté configurada como **PC** y que AetherSDR haya terminado de conectarse a la radio.
- **El panel Phone no se actualiza cuando VOX se activa/desactiva mediante un atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior si el panel Phone no se actualiza inmediatamente cuando VOX se activa/desactiva mediante un atajo de teclado.
- **El indicador ALC muestra valores inesperados** — Los medidores ALC ahora leen del medidor ALC por software (MeterModel::swAlcChanged) en rangos de dBFS. Los valores fuera de −20 a 0 dBFS no se muestran; el indicador simplemente se fija en el extremo más cercano. Esto reemplaza la ruta HWALC anterior que producía lecturas sin significado.

## Controles del panel CW (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor para los parámetros CW fueron reemplazadas con widgets QLineEdit. Los controles deslizantes y botones adyacentes permanecen sin cambios. Haga clic en cualquier valor y escriba un número directamente para configurarlo. Los valores se ajustan al rango válido cuando presiona Enter o Tab.

| Control               | Tipo          | Valor predeterminado | Rango válido       |
|-----------------------|---------------|---------|-------------------|
| **Retardo (CW)**      | Control deslizante + edición | 500     | 0–2000 ms         |
| **Velocidad (CW)**    | Control deslizante + edición | 20      | 5–100 WPM         |
| **Volumen de señal lateral** | Control deslizante + edición | 50      | 0–100             |
| **Pitch < / >**       | Texto + botones| 600     | 100–6000 Hz       |

- Los widgets QLineEdit de **Retardo (CW)**, **Velocidad (CW)** y **Volumen de señal lateral** usan `QIntValidator` para restringir la entrada al rango válido.
- El widget **Pitch < / >** (CwTriBtn) permite escribir un valor (100–6000) o hacer clic en los botones < / > para avanzar de a 10 Hz.
- El control deslizante **Retardo (CW)** se corrigió en v0.9.8 (#2428) para que `setCwDelay` almacene en caché el valor inmediatamente, evitando que la emisión de la radio devuelva el control deslizante a su lugar.
- El control deslizante **Volumen de señal lateral** controla tanto el volumen del monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de señal lateral del lado del cliente de forma sincronizada.

## Comportamiento de la señal lateral CW (v0.9.1 y posteriores)

La alternancia **Sidetone** y el control deslizante **Sidetone volume** en el panel CW controlan tanto el monitor alimentado por DAX de la radio como el generador de señal lateral de baja latencia del lado del cliente de forma sincronizada. Ya no hay un botón separado **Local STn**, un control deslizante de volumen local separado ni una alternancia **Follow** de tono. Esos controles se han eliminado.

- Activar **Sidetone** enciende tanto el monitor del lado de la radio como el generador del lado del cliente simultáneamente.
- Ajustar **Sidetone volume** establece tanto `mon_gain_cw` en la radio como
