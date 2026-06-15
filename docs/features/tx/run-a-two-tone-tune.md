# Ejecutar una sintonía de dos tonos

Una sintonía de dos tonos le permite verificar la linealidad y los niveles de excitación del transmisor activando manualmente la radio con MOX mientras monitorea la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra conectado).
- El applet de Controles de TX está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y se encuentra en una frecuencia despejada.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet de Controles de TX, ajuste el deslizador **Tune Pwr** al nivel de potencia que desee utilizar para la prueba. El valor predeterminado es 10; el rango válido es 0–100. Mientras arrastra el control del deslizador, una información sobre herramientas muestra el valor de potencia en porcentaje (ej., "10%").
2. Ajuste el deslizador **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100. Mientras arrastra el control del deslizador, una información sobre herramientas muestra el valor de potencia en porcentaje (ej., "100%").
3. Si desea utilizar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio se activa para transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de disminuir hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente cuando desactiva la transmisión. Ajuste el deslizador **RF Power** mientras transmite para alcanzar su potencia de salida objetivo.
7. Cuando la prueba esté completa, haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado sin iluminación.
8. Detenga la fuente de audio de dos tonos.

## Función de cada control

| Control    | Tipo                                                                                                                                                                                                                                        | Valor predeterminado                                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador                                                                                                                                                                                                                                  | 100                                                                                                                                                |
| Tune Pwr   | Deslizador                                                                                                                                                                                                                                  | 10                                                                                                                                                 |
| TX Profile | Menú desplegable                                                                                                                                                                                                                            | —                                                                                                                                                  |
| MOX        | Botón de alternancia                                                                                                                                                                                                                        | —                                                                                                                                                  |
| RF Pwr     | Medidor                                                                                                                                                                                                                                     | —                                                                                                                                                  |
| SWR        | Medidor                                                                                                                                                                                                                                     | —                                                                                                                                                  |
| TUNE       | Inicia/detiene la portadora de sintonía; el texto se vuelve 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de onda portadora (Mono Tone / Two Tone) para el próximo ciclo de sintonía.                  | El menú contextual del clic derecho (showTuneContextMenu) es transitorio de un solo uso: no se persiste nada; la radio vuelve a single_tone al reiniciar. |
| ATU        | Inicia el ciclo de sintonía del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido de pre-sintonía y borrado de memorias del ATU.    | Deshabilitado cuando TGXL está en modo OPERATE. El menú contextual del clic derecho (showAtuContextMenu) expone el barrido de banda de pre-sintonía (#2624) y Borrar memorias del ATU. |
| MEM        | Botón de alternancia                                                                                                                                                                                                                        | —                                                                                                                                                  |
| APD        | Botón de alternancia                                                                                                                                                                                                                        | —                                                                                                                                                  |
| Active     | Indicador (verde)                                                                                                                                                                                                                           | atenuado                                                                                                                                           |
| Cal        | Indicador (verde)                                                                                                                                                                                                                           | atenuado                                                                                                                                           |
| Avail      | Indicador (verde)                                                                                                                                                                                                                           | atenuado                                                                                                                                           |
| Success    | Indicador (verde)                                                                                                                                                                                                                           | atenuado                                                                                                                                           |
| Byp        | Indicador (naranja)                                                                                                                                                                                                                         | atenuado                                                                                                                                           |
| Mem        | Indicador (verde)                                                                                                                                                                                                                           | atenuado                                                                                                                                           |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor de ROE se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil de TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias del ATU, considere recuperar una memoria conocida como buena antes de activar la transmisión para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria del ATU](recall-an-atu-memory.md).
- Si el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de fonía, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o el slice de TX no está en un modo de fonía, **MOX** se comporta como en versiones anteriores.

## Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y puentear el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía del ATU nuevo. El indicador **Success** se enciende en verde cuando el sintonizador encuentra una adaptación.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es Successful o OK y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente se cambia el sintonizador a bypass. El indicador **Byp** se enciende en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era Successful o OK.
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

## Menú de clic derecho del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-tune bands…** — Abre el diálogo de Pre-sintonía para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias del ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú aparece atenuado con una información sobre herramientas que sugiere habilitar MEM primero.
- **Clear ATU memories…** — Borra todas las memorias del ATU almacenadas después de un diálogo de confirmación.

## Menú de clic derecho del botón TUNE

Haga clic derecho en el botón **TUNE** para seleccionar la forma de onda portadora para el próximo ciclo de sintonía:

- **Mono Tone** — Tono único, la forma de onda portadora predeterminada.
- **Two Tone** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se conserva al reiniciar. El modo de sintonía de la radio vuelve al tono único por sí mismo al reiniciar. Una marca de verificación junto a cada entrada muestra el modo de sintonía actual de la radio.

## APD (Predistorsión adaptativa)

El botón de alternancia **APD** activa o desactiva la predistorsión adaptativa en la radio. Cuando está activado, los tres indicadores de estado debajo del botón muestran el estado actual:

- **Active** — Se enciende en verde cuando el ecualizador se aplica activamente.
- **Cal** — Se enciende en verde cuando la radio aún está calibrando.
- **Avail** — Se enciende en verde cuando hay una calibración disponible pero aún no se ha aplicado.

Los indicadores progresan a través de Cal → Avail → Active a medida que el sistema APD completa su ciclo de calibración.

## Solución de problemas

- **MOX se activa pero RF Pwr marca cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a activar la transmisión.
- **La ROE se vuelve roja inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para desactivar la transmisión, luego ejecute el ATU o verifique la línea de alimentación antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr marca a fondo de escala** — El deslizador RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar la transmisión, luego reduzca el deslizador RF Power antes de volver a activarla.
- **El botón ATU inicia una nueva sintonía en lugar de puentear** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es normal. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU informó por última vez una sintonía exitosa.
- **Los tonos Quindar se reproducen inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en la tira de canales de audio y el slice de TX está en un modo de fonía. Si no desea los tonos Quindar durante esta prueba, deshabilite el chip QUIN en la tira de canales de audio antes de activar la transmisión.

## Relacionados

- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- Pre-sintonizar bandas para el ATU
- Borrar memorias del ATU
