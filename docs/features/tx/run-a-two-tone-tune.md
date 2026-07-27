# Ejecutar una Prueba de Dos Tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación activando manualmente la radio con MOX mientras se monitorea la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra "conectado").
- El applet Controles de TX está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet Controles de TX, ajuste el deslizador **Tune Pwr** al nivel de potencia que desee usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (p. ej., "10%").
2. Ajuste el deslizador **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (p. ej., "100%").
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio se activa para transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de disminuir hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente cuando desactiva la transmisión. Ajuste el deslizador **RF Power** mientras transmite para alcanzar la salida deseada.
   - Coloque el ratón sobre el medidor RF Pwr para ver la potencia exacta en una información sobre herramientas (p. ej., "47 W").
   - Coloque el ratón sobre el medidor SWR para ver la relación exacta en una información sobre herramientas (p. ej., "1.35:1").
7. Cuando la prueba haya finalizado, haga clic en **MOX** nuevamente para desactivar la transmisión. El botón vuelve a su estado apagado con un borde y acento de texto color ámbar.
8. Detenga la fuente de audio de dos tonos.

## Qué hace cada control

| Control    | Tipo                                                                                                                                                                                            | Valor predeterminado                                                                                                                                                  |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador                                                                                                                                                                                      | 100                                                                                                                                                                   |
| Tune Pwr   | Deslizador                                                                                                                                                                                      | 10                                                                                                                                                                    |
| TX Profile | Menú desplegable                                                                                                                                                                                | —                                                                                                                                                                     |
| MOX        | Botón de alternancia                                                                                                                                                                            | —                                                                                                                                                                     |
| RF Pwr     | Muestra la potencia directa en la salida del excitador con retención de pico PEP (2 s de retención, luego disminuye al valor suavizado actual en ~2.5 s). El pico se restablece inmediatamente al desactivar la transmisión. Coloque el ratón encima para ver la potencia exacta. | La escala cambia según el modelo de radio mediante setPowerScale. La dinámica de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del S-meter en SMeterWidget (#2561). |
| SWR        | Medidor                                                                                                                                                                                         | —                                                                                                                                                                     |
| TUNE       | Inicia/detiene la portadora de sintonía; el texto cambia a 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Tono único / Dos tonos) para el próximo ciclo de sintonía. | El menú contextual del clic derecho (showTuneContextMenu) es transitorio de un solo uso; no se conserva nada; la radio vuelve a single_tone al reiniciar.              |
| ATU        | Inicia el ciclo de sintonía del ATU interno. Si el estado es Exitoso/OK en la misma frecuencia, un segundo clic envía una orden de bypass. El clic derecho abre las acciones de barrido de presintonía y Borrar memorias ATU. | Deshabilitado cuando TGXL está en modo OPERATE. El menú contextual del clic derecho (showAtuContextMenu) expone el barrido de presintonía de banda (#2624) y Borrar memorias ATU. |
| MEM        | Botón de alternancia                                                                                                                                                                            | —                                                                                                                                                                     |
| APD        | Botón de alternancia                                                                                                                                                                            | —                                                                                                                                                                     |
| Active     | Indicador (verde)                                                                                                                                                                               | atenuado                                                                                                                                                              |
| Cal        | Indicador (verde)                                                                                                                                                                               | atenuado                                                                                                                                                              |
| Avail      | Indicador (verde)                                                                                                                                                                               | atenuado                                                                                                                                                              |
| Success    | Indicador (verde)                                                                                                                                                                               | atenuado                                                                                                                                                              |
| Byp        | Indicador (naranja)                                                                                                                                                                             | atenuado                                                                                                                                                              |
| Mem        | Indicador (verde)                                                                                                                                                                               | atenuado                                                                                                                                                              |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor SWR se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil de TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias ATU, considere recuperar una memoria conocida antes de activar la transmisión para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria ATU](recall-an-atu-memory.md).
- Si el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de teléfono, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o el slice de TX no está en un modo de teléfono, **MOX** se comporta como en versiones anteriores.
- Los deslizadores RF Power y Tune Pwr ahora también actualizan su valor mostrado desde el modelo cuando suelta el control deslizante. Esto asegura que el valor mostrado siempre coincida con la configuración real de la radio.

## Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y pasar por alto el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se enciende en verde cuando el sintonizador encuentra una adaptación.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es Exitoso o OK y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente se cambia el sintonizador a bypass. El indicador **Byp** se enciende en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era Exitoso o OK.
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-sintonizar bandas…** — Abre el diálogo de presintonía para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú se muestra atenuado con una información sobre herramientas que sugiere habilitar MEM primero.
- **Borrar memorias ATU…** — Borra todas las memorias ATU almacenadas después de un diálogo de confirmación.

## Menú contextual del botón TUNE

Haga clic derecho en el botón **TUNE** para seleccionar la forma de la portadora para el próximo ciclo de sintonía:

- **Tono único** — Un solo tono, la forma de portadora predeterminada.
- **Dos tonos** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se conserva al reiniciar la radio. El modo de sintonía de la radio vuelve a tono único por sí solo al reiniciar. Una marca de verificación junto a cada entrada muestra el modo de sintonía actual de la radio.

## APD (Predistorsión Adaptativa)

El botón de alternancia **APD** habilita o deshabilita la predistorsión adaptativa en la radio. Cuando está habilitado, los tres indicadores de estado debajo del botón muestran el estado actual:

- **Active** — Se enciende en verde cuando el ecualizador está aplicado activamente.
- **Cal** — Se enciende en verde cuando la radio aún está calibrando.
- **Avail** — Se enciende en verde cuando hay una calibración disponible pero aún no aplicada.

Los indicadores progresan a través de Cal → Avail → Active a medida que el sistema APD completa su ciclo de calibración.

## Acento del botón MOX en reposo

Cuando no está transmitiendo (estado inactivo), el botón **MOX** muestra un borde y acento de texto color ámbar que lo distingue de los botones neutros TUNE, ATU y MEM. Este acento se puede editar en el Editor de temas bajo los tokens `color.tx.mox.*`, reflejando el acento del chip LIVE en el waterfall.

## Solución de problemas

- **MOX se activa pero RF Pwr marca cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de reactivar la transmisión.
- **SWR se vuelve rojo inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para desactivar la transmisión, luego ejecute el ATU o verifique la línea de alimentación antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al fondo de escala** — El deslizador RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar la transmisión, luego reduzca el deslizador RF Power antes de reactivar.
- **El botón ATU inicia una nueva sintonía en lugar de hacer bypass** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es esperado. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU informó por última vez una sintonía exitosa.
- **Los tonos Quindar suenan inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en la tira de canales de audio y el slice de TX está en un modo de teléfono. Si no desea los tonos Quindar durante esta prueba, deshabilite el chip QUIN en la tira de canales de audio antes de activar la transmisión.

## Relacionado

- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria ATU](recall-an-atu-memory.md)
- Presintonizar bandas para el ATU
- Borrar memorias ATU
