# Ajustar la ganancia del micrófono y habilitar la mezcla de accesorios

Use esta página para configurar el nivel de entrada del micrófono y mezclar la entrada de accesorios junto con la fuente de micrófono principal en modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de la bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o derecha para ajustar el nivel de entrada. La lectura numérica a la derecha del control deslizante se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena del lado del cliente como `PcMicGain`. La radio siempre reporta `mic_level=0` para la fuente PC; AetherSDR conserva el valor localmente.
   - Cuando el modo RADE está activo, el control deslizante también actúa como un control de ganancia RADE del lado del cliente y se almacena bajo la misma clave `PcMicGain`. El valor del control deslizante no se envía a la radio en este estado.
4. Observe el indicador **Level** sobre los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. El indicador se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada de accesorios junto con la fuente de micrófono activa, haga clic en **+ACC** para que se ilumine. Haga clic nuevamente para deshabilitar la mezcla.

## Qué hace cada control

| Control               | Qué hace                                                                                                                                                                                                                                                                          | Valor predeterminado                                                                                                     |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Mic gain**          | Establece el nivel de entrada del micrófono. Cuando Mic source es PC o el modo RADE está activo, el valor se conserva localmente como `PcMicGain` y no se envía a la radio.                                                                                                       | 50                                                                                                                       |
| **+ACC**              | Habilita la mezcla de entrada del micrófono de accesorios junto con la fuente primaria seleccionada.                                                                                                                                                                               | —                                                                                                                        |
| **Level** (indicador) | Muestra el nivel pico de entrada del micrófono en dBFS. Se vuelve rojo por encima de 0 dBFS.                                                                                                                                                                                    | —                                                                                                                        |
| **Compression** (indicador) | Muestra la cantidad de compresión de voz que se está aplicando. El llenado es inverso (completamente a la derecha = sin compresión). En v0.9.7, el indicador está controlado por el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas de la cadena de TX. | —                                                                                                                        |
| **ALC (panel Phone)** | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.                                                                               | Reconfigurado de HWALC (voltaje RCA) al medidor ALC de software en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. |
| **ALC (panel CW)**    | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW.                                                                                                                                                       | Añadido en v26.5.1 (#2552) como parte de la división del medidor ALC de software. Usa el modo HGauge::setFillFromRight.  |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del tono lateral CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único interruptor **Sidetone** y un control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. Activar o desactivar **Sidetone** activa o desactiva ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y la panorámica estéreo siempre siguen automáticamente la configuración `cw_pitch` y `mon_pan_cw` de la radio. No hay controles locales separados de tono o seguimiento.

El bus de tono lateral se comparte con los tonos Quindar; el tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Cambio en v0.9.2.1: controles de tono lateral local separados eliminados

Antes de v0.9.2.1, el subpanel CW incluía un interruptor **Local STn** separado, un control deslizante de volumen local, un interruptor de seguimiento de tono **Follow** y un control deslizante de tono manual. Estos controles se eliminan en v0.9.2.1. El interruptor **Sidetone** y el control deslizante **Sidetone volume** ahora controlan tanto el tono lateral del lado de la radio como el del lado del cliente juntos, y el tono y la panorámica siempre siguen automáticamente a la radio.

Si anteriormente usaba el botón **Local STn** independientemente del interruptor principal **Sidetone**, use el interruptor **Sidetone** en adelante. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté encendido.

### Cambios en v0.9.8: campos de valor QLineEdit

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume y Pitch) ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente. El control deslizante se mueve para coincidir cuando presiona Intro o tabula. Esto coincide con el comportamiento de SmartSDR.

### Controles del subpanel CW

| Control | Qué hace | Valor predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in CW. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–2000). En v0.9.8, el valor se almacena en caché inmediatamente al escribirse para que la emisión de la radio no devuelva el control deslizante (#2428). | 500 ms | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de tecleo CW en palabras por minuto. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (5–100). | 20 WPM | 5–100 WPM | — |
| **Sidetone** | Activa o desactiva el tono lateral CW. Activa/desactiva tanto el monitor alimentado por DAX de la radio como el generador de baja latencia del lado del cliente de forma sincronizada. En Windows, el flujo de tono lateral comienza inmediatamente al conectar (v0.9.3, #2105). El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de tono lateral local simultáneamente. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–100). | 50 | 0–100 | — |
| **L / R pan (CW)** | Establece la panorámica estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador de tono lateral local. Haga doble clic para centrar. | 50 | 0–100 | — |
| **Pitch < / >** | Establece el tono del tono lateral y decodificación CW. Escriba un valor (100–6000) en el campo de texto o haga clic en los botones < y > para avanzar en pasos de 10 Hz. El tono también se sigue automáticamente desde la configuración `cw_pitch` de la radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Activa o desactiva el break-in completo (QSK). En v0.9.7, las rutas de teclado CW y MIDI respetan completamente esta configuración: con Breakin ON (QSK) los bordes de tecla activan TX y el retardo de break-in mantiene el relé; con Breakin OFF las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente PTT automática anterior que enmascaraba Breakin OFF y eliminaba el tiempo de espera QSK se ha eliminado. | — | On / Off | — |
| **Iambic** | Activa o desactiva el manipulador de paletas iámbico. | — | On / Off | — |
| **ALC (panel CW)** | Muestra la lectura del control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Refleja el indicador ALC del panel Phone. | — | -20 a 0 dBFS (rojo > -3 dBFS) | — |

## Consejos

- El indicador **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el indicador se activa cuando transmite. Cuando **Mic source** está configurado en PC, el indicador usa medición del lado del cliente y no está sujeto a esta supresión: aparece inmediatamente al conectar (v0.9.3, #2086). Cuando el modo RADE está activo, el indicador también usa medición del lado del cliente y está activo durante RX.
- El indicador **Compression** lee 0 dB siempre que la radio no esté en el estado de interbloqueo TRANSMITTING (v0.9.7). Esto evita que aparezcan lecturas obsoletas de la cadena de TX durante RX. El indicador se activa tan pronto como transmite con el procesador de voz habilitado.
- Si usa la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía a la radio; es gestionado completamente por AetherSDR. Al cambiar de la fuente PC y volver, se restaura el valor guardado. El modo RADE comparte esta misma configuración `PcMicGain`.
- Con **Breakin** apagado en v0.9.7, las pulsaciones de tecla se ponen en cola y TX no se activa automáticamente. Active PTT manualmente antes de enviar. Si espera una operación QSK completa, confirme que **Breakin** esté iluminado antes de teclear.
- El generador de tono lateral del lado del cliente proporciona aproximadamente 10 ms de latencia, lo cual es útil a velocidades CW más altas donde la latencia de ida y vuelta DAX de la radio se vuelve notable. Debido a que ambos están controlados por el único interruptor **Sidetone**, no hay riesgo de que uno esté activo sin el otro.
- Haga doble clic en **L / R pan (CW)** para devolver la posición de panorámica al centro (50).
- En v0.9.8, los campos de valor Delay, Speed, Sidetone Volume y Pitch aceptan entrada numérica directa. Escriba un valor y presione Intro o tabule; el control deslizante se mueve para coincidir. Los campos validan la entrada y aplican el rango válido automáticamente.
- En v26.5.1, el indicador ALC tanto en el panel Phone como en el CW se actualizó para usar el medidor ALC de software (pico SSB posterior al ALC de software en dBFS) en lugar de la ruta HWALC anterior (voltaje RCA). Ambos indicadores ahora leen de la misma fuente MeterModel::swAlcChanged, por lo que la lectura es consistente entre modos de voz y CW. El rango es de -20 a 0 dBFS, con el indicador llenándose de derecha a izquierda. Los valores fuera de este rango se fijan en el extremo más cercano.

## Solución de problemas

- **El control deslizante Mic gain vuelve a su lugar o lee 0 después de ajustar** — Está usando la fuente PC y la radio reporta `mic_level=0`. Este comportamiento es esperado; AetherSDR mantiene el valor en `PcMicGain` y no lo escribe en la radio. La posición del control deslizante es correcta.
- **El control deslizante Mic gain no actualiza la radio cuando el modo RADE está activo** — Esto es esperado. En modo RADE, el control deslizante actúa como un control de ganancia del lado del cliente almacenado en `PcMicGain`. Enviar el valor a la radio sobrescribiría la configuración del micrófono de hardware. El control deslizante reanudará el comportamiento normal del lado de la radio cuando el modo RADE se desactive.
- **+ACC no tiene efecto** — Confirme que la radio esté en un modo de voz y que el subpanel Phone esté activo. El control +ACC solo está presente en el subpanel Phone; no está disponible cuando el modo CW está activo.
- **El indicador Level no muestra movimiento al hablar** — Si Mic source no es PC y el modo RADE no está activo, el indicador se suprime a −150 dBFS cuando no se transmite y el monitor en recepción está desactivado. Active la radio o habilite el monitor de TX para ver niveles en vivo. Si Mic source es PC o el modo RADE está activo, el indicador debería estar activo inmediatamente; si no lo está, verifique que el dispositivo de audio esté seleccionado y que AetherSDR esté conectado a la radio.
- **El indicador Compression siempre muestra 0 dB** — El indicador Compression está controlado por el estado de interbloqueo TRANSMITTING de la radio (v0.9.7). Solo mostrará una lectura distinta de cero mientras la radio está transmitiendo activamente y el procesador de voz (**PROC**) está habilitado. Confirme que **PROC** esté iluminado y que esté transmitiendo.
- **Breakin OFF no tiene efecto: la radio sigue activando TX con entrada CW** — Este era un error resuelto en v0.9.7. La envolvente PTT automática anterior forzaba TX independientemente de la configuración de Breakin. Actualice a v0.9.7 o posterior. Después de actualizar, con **Breakin** apagado, active PTT manualmente antes de enviar CW.
- **El panel Phone no se actualiza cuando VOX se activa/desactiva mediante un atajo de teclado** — Esto se resolvió en v0.9.3 (#2084). Actualice a v0.9.3 o posterior.
- **El tono lateral no se escucha inmediatamente después de conectar en Windows** — Esto se resolvió en v0.9.3 (#2105) corrigiendo el orden de inicialización de AudioEngine. Actualice a v0.9.3 o posterior.
- **Los controles Local STn / Follow están
