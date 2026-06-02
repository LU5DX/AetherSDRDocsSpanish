# Ajustar la ganancia del micrófono y habilitar la mezcla del accesorio

Use esta página para configurar el nivel de entrada del micrófono y mezclar la entrada del accesorio junto con la fuente de micrófono principal en modo Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible. Si el slice está en modo CW, se muestra el subpanel CW en su lugar.

## Pasos

1. Abra el applet Phone/CW en el Panel de Applets de la barra lateral derecha. Si no es visible, haga clic en el botón de la bandeja **P/CW**.
2. Localice el cuadro combinado **Mic source**. Confirme que la fuente que desea ajustar esté seleccionada (por ejemplo, MIC, BAL, LINE, ACC o PC).
3. Arrastre el control deslizante **Mic gain** hacia la izquierda o la derecha para ajustar el nivel de entrada. La lectura numérica a la derecha del control deslizante se actualiza mientras arrastra. El rango válido es 0–100; el valor predeterminado es 50.
   - Cuando **Mic source** está configurado en PC, el valor se almacena en el lado del cliente como `PcMicGain`. La radio siempre informa `mic_level=0` para la fuente PC; AetherSDR conserva el valor localmente.
   - Cuando el modo RADE está activo, el control deslizante también actúa como un control de ganancia RADE del lado del cliente y se almacena bajo la misma clave `PcMicGain`. El valor del control deslizante no se envía a la radio en este estado.
4. Observe el indicador **Level** sobre los controles. Apunte a picos entre −20 y −10 dBFS durante el habla normal. El indicador se vuelve rojo por encima de 0 dBFS.
5. Para mezclar la entrada del accesorio junto con la fuente de micrófono activa, haga clic en **+ACC** para que se ilumine. Vuelva a hacer clic para deshabilitar la mezcla.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado |
|---|---|---|
| **Mic gain** | Configura el nivel de entrada del micrófono. Cuando la fuente del micrófono es PC o el modo RADE está activo, el valor se persiste localmente como `PcMicGain` y no se envía a la radio. | 50 |
| **+ACC** | Habilita la mezcla de entrada del micrófono accesorio junto con la fuente primaria seleccionada. | — |
| Indicador **Level** | Muestra el nivel pico de entrada del micrófono en dBFS. Se vuelve rojo por encima de 0 dBFS. | — |
| Indicador **Compression** | Muestra la cantidad de compresión de voz que se está aplicando. El llenado está invertido (completamente a la izquierda = 0 dB, sin compresión; completamente a la derecha = -25 dB, compresión máxima). En v0.9.7, el indicador está controlado por el estado de interbloqueo TRANSMITTING de la radio y la habilitación del procesador de voz: lee 0 dB durante RX para evitar lecturas obsoletas de la cadena TX. En v26.5.3, el valor del medidor está invertido con respecto a la visualización anterior: MeterModel expone la compresión como una cantidad positiva de 0–25 dB, y el indicador la convierte a la visualización invertida (0 en el borde derecho, -25 en el borde izquierdo). | — |
| **ALC (panel Phone)** | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. En v26.5.3, el indicador se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la pantalla. | — |
| **ALC (panel CW)** | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para obtener lecturas consistentes en voz y CW. En v26.5.3, el indicador se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la pantalla. | — |

## Controles de tono lateral CW

Cuando el slice activo está en modo CW, el subpanel CW reemplaza al subpanel Phone. Los siguientes controles rigen el comportamiento del tono lateral CW.

### Cómo funciona el tono lateral (v0.9.1 y posteriores)

Un único conmutador **Sidetone** y un control deslizante **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente (`CwSidetoneGenerator`, aproximadamente 10 ms de latencia) de forma sincronizada. Habilitar o deshabilitar **Sidetone** habilita o deshabilita ambos simultáneamente. Mover **Sidetone volume** establece tanto `mon_gain_cw` en la radio como el volumen del generador local al mismo tiempo.

El tono y la panorámica estéreo siempre siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` de la radio. No hay controles locales separados de tono o seguimiento.

El bus de tono lateral se comparte con los tonos Quindar; el tono lateral y los tonos Quindar son mutuamente excluyentes a nivel de modo.

### Cambio en v0.9.2.1: controles de tono lateral locales separados eliminados

Antes de v0.9.2.1, el subpanel CW incluía un conmutador **Local STn** separado, un control deslizante de volumen local, un conmutador de seguimiento de tono **Follow** y un control deslizante de tono manual. Estos controles se eliminaron en v0.9.2.1. El conmutador **Sidetone** y el control deslizante **Sidetone volume** ahora conducen juntos tanto el tono lateral del lado de la radio como el del lado del cliente, y el tono y la panorámica siempre siguen automáticamente a la radio.

Si anteriormente usaba el botón **Local STn** independientemente del conmutador principal **Sidetone**, use el conmutador **Sidetone** en adelante. El generador local de baja latencia permanece disponible y activo siempre que **Sidetone** esté encendido.

### Cambios en v0.9.8: campos de valor QLineEdit

En v0.9.8, las cuatro etiquetas de valor CW (Delay, Speed, Sidetone Volume y Pitch) ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente. El control deslizante se mueve para coincidir cuando presiona Enter o tabula para salir. Esto coincide con el comportamiento de SmartSDR.

### Cambios en v26.5.3: enrutamiento de salida de audio del tono lateral

En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). Esto asegura que el tono lateral se escuche en el mismo dispositivo que ha seleccionado para otras transmisiones de audio, en lugar de usar siempre la salida de audio predeterminada del sistema.

### Cambios en v26.6.1: soporte de temas

En v26.6.1, el applet Phone/CW adopta completamente el sistema de temas de AetherSDR. Todos los elementos visuales (incluidas las ranuras y manijas de los controles deslizantes, el texto de las etiquetas y los fondos de los botones pulsadores) ahora utilizan los colores del tema en lugar de valores codificados. El contenedor del applet está diseñado con la clase de tema `applet/digi`, lo que garantiza una apariencia consistente en todos los temas compatibles.

### Controles del subpanel CW

| Control | Qué hace | Valor predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **Delay (CW)** | Establece el retardo de break-in de CW. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–2000). En v0.9.8, el valor se almacena en caché inmediatamente cuando se escribe para que la emisión de radio no devuelva el control deslizante (#2428). | 500 ms | 0–2000 ms (paso 10) | — |
| **Speed (CW)** | Establece la velocidad de manipulacion CW en palabras por minuto. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (5–100). | 20 WPM | 5–100 WPM | — |
| **Sidetone** | Activa el tono lateral de CW. Habilita/deshabilita tanto el monitor alimentado por DAX de la radio como el generador de baja latencia del lado del cliente de forma sincronizada. En Windows, la transmisión de tono lateral comienza inmediatamente al conectar (v0.9.3, #2105). El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). En v26.5.3, el tono lateral se enruta a la salida de audio seleccionada por el usuario (#2899). | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla tanto `mon_gain_cw` en la radio como el volumen del generador de tono lateral local simultáneamente. Arrastre el control deslizante o haga clic en el campo de valor y escriba un número (0–100). | 50 | 0–100 | — |
| **L / R pan (CW)** | Establece la panorámica estéreo del monitor CW. Se aplica tanto al monitor del lado de la radio como al generador de tono lateral local. Haga doble clic para volver a centrar. | 50 | 0–100 | — |
| **Pitch < / >** | Establece el tono lateral y el tono de decodificación de CW. Escriba un valor (100–6000) en el campo de texto o haga clic en los botones < y > para avanzar en pasos de 10 Hz. El tono también se sigue automáticamente desde la configuración `cw_pitch` de la radio. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Breakin** | Activa el break-in completo (QSK). En v0.9.7, las rutas del teclado CW y MIDI respetan completamente esta configuración: con Breakin ON (QSK) los bordes de la tecla activan TX y el retardo de break-in mantiene el relé; con Breakin OFF las teclas se ponen en cola y el operador activa PTT manualmente. La envolvente PTT automática anterior que enmascaraba Breakin OFF y eliminaba el tiempo de espera de QSK ha sido eliminada. | — | On / Off | — |
| **Iambic** | Activa el manipulador de paleta iámbico. | — | On / Off | — |
| **ALC (panel CW)** | Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Refleja el indicador ALC del panel Phone. En v26.5.3, el indicador se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo para evitar parpadeos transitorios en la pantalla. | — | -20 a 0 dBFS (rojo > -3 dBFS) | — |

## Consejos

- El indicador **Level** se suprime a −150 dBFS cuando la radio no está transmitiendo y el monitor en recepción está desactivado. Esto es normal; el indicador se activa cuando transmite. Cuando **Mic source** está configurado en PC, el indicador usa la medición del lado del cliente y no está sujeto a esta supresión: aparece inmediatamente al conectar (v0.9.3, #2086). Cuando el modo RADE está activo, el indicador también usa la medición del lado del cliente y está activo durante RX.
- El indicador **Compression** lee 0 dB siempre que la radio no esté en el estado de interbloqueo TRANSMITTING (v0.9.7). Esto evita que aparezcan lecturas obsoletas de la cadena TX durante RX. El indicador se activa tan pronto como transmite con el procesador de voz habilitado. En v26.5.3, el valor del medidor de compresión está invertido: MeterModel expone la compresión como una cantidad positiva de 0–25 dB, y el indicador la convierte a la visualización invertida (0 en el borde derecho, -25 en el borde izquierdo). El indicador ahora muestra correctamente compresión cero a 0 dB y compresión máxima a -25 dB.
- Si usa la fuente PC, tenga en cuenta que el valor `PcMicGain` no se envía a la radio; AetherSDR lo gestiona completamente. Cambiar de la fuente PC y volver restaura el valor guardado. El modo RADE comparte esta misma configuración `PcMicGain`.
- Con **Breakin** desactivado en v0.9.7, las pulsaciones de teclas se ponen en cola y TX no se activa automáticamente. Active PTT manualmente antes de enviar. Si espera una operación QSK completa, confirme que **Breakin** esté iluminado antes de manipular.
- El generador de tono lateral del lado del cliente proporciona aproximadamente 10 ms de latencia, lo cual es útil a velocidades CW más altas donde la latencia de ida y vuelta DAX de la radio se vuelve notable. Debido a que ambos están controlados por el único conmutador **Sidetone**, no hay riesgo de que uno esté activo sin el otro.
- Haga doble clic en **L / R pan (CW)** para devolver la posición panorámica al centro (50).
- En v0.9.8, los campos de valor Delay, Speed, Sidetone Volume y Pitch aceptan entrada numérica directa. Escriba un valor y presione Enter o tabule para salir: el control deslizante se mueve para coincidir. Los campos validan la entrada y aplican el rango válido automáticamente.
- En v26.5.1, el indicador ALC en los paneles Phone y CW se actualizó para usar el medidor ALC de software (pico SSB posterior al ALC de software en dBFS) en lugar de la ruta HWALC (voltaje RCA) anterior. Ambos indicadores ahora leen de la misma fuente MeterModel::swAlcChanged, por lo que la lectura es consistente en los modos de voz y CW. El rango es de -20 a 0 dBFS, con el indicador llenándose de derecha a izquierda. Los valores fuera de este rango se fijan en el extremo más cercano.
- En v26.5.3, el indicador ALC en ambos paneles se inicializa a -20 dBFS en la construcción y se establece inmediatamente a su valor mínimo. Esto evita un parpadeo transitorio que podría aparecer al inicio antes de que llegue la primera actualización del medidor desde la radio.
- En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada. Si no escucha el tono lateral después de la actualización, verifique que el dispositivo de salida de audio deseado esté seleccionado en la configuración de audio de AetherSDR.
- En v26.6.1, todos los elementos visuales en el applet Phone/CW usan colores del tema. Si cambia el tema activo, el applet se actualiza automáticamente para coincidir. Las manijas de los controles deslizantes, los fondos de los botones pulsadores y los colores de las etiquetas responden a la configuración del tema actual.

## Solución de problemas

- **El control deslizante de ganancia del micrófono vuelve a su posición
