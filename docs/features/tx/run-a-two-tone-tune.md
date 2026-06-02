# Ejecutar una Prueba de Dos Tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación activando la radio manualmente con MOX mientras se monitorean la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado a la FLEX-8600 (el indicador de radio muestra conectado).
- El applet de Controles de TX está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y se encuentra en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet de Controles de TX, ajuste el deslizador **Tune Pwr** al nivel de potencia que desee utilizar para la prueba. El valor predeterminado es 10; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (por ejemplo, "10%").
2. Ajuste el deslizador **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (por ejemplo, "100%").
3. Si desea utilizar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio se activa para transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de disminuir hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente cuando desactiva la transmisión. Ajuste el deslizador **RF Power** mientras transmite para alcanzar su potencia de salida objetivo.
7. Cuando la prueba esté completa, haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado sin iluminación.
8. Detenga la fuente de audio de dos tonos.

## Función de cada control

| Control       | Tipo                                                        | Predeterminado | Notas                                                                                                                                                                                                                        |
|---------------|-------------------------------------------------------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power      | Deslizador                                                  | 100            | Establece el nivel de potencia de RF de transmisión (porcentaje del máximo).                                                                                                                                                 |
| Tune Pwr      | Deslizador                                                  | 10             | Establece el nivel de potencia de la portadora de sintonía (porcentaje del máximo).                                                                                                                                          |
| TX Profile    | Menú desplegable                                            | —              | Al seleccionar un perfil, se carga desde la radio.                                                                                                                                                                           |
| MOX           | Botón de alternancia                                        | —              | Activa/desactiva la transmisión manual; el botón se vuelve rojo mientras TX está activo. Se enruta a través del coordinador de tono Quindar para que los tonos K/BK se reproduzcan al activar/desactivar cuando Quindar está habilitado en modos de telefonía. |
| RF Pwr        | Medidor                                                     | —              | Muestra la potencia directa en la salida del excitador (0–120 W sin amplificador, 0–600 W con Aurora 500W). Rojo por encima de 100 W / 500 W.                                                                                |
| SWR           | Medidor                                                     | —              | Muestra la relación de onda estacionaria en el excitador (1.0–3.0, rojo por encima de 2.5).                                                                                                                                  |
| TUNE          | Botón pulsador                                              | —              | Inicia/detiene la portadora de sintonía; el texto se vuelve "TUNING..." con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Mono Tone / Two Tone) para el siguiente ciclo de sintonía (disparo único transitorio). |
| ATU           | Botón pulsador                                              | —              | Inicia el ciclo de sintonía del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía un bypass en su lugar. El clic derecho abre las acciones de barrido de pre-sintonía y borrado de memorias del ATU. |
| MEM           | Botón de alternancia                                        | —              | Activa/desactiva la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE.                                                                                                                         |
| APD           | Botón de alternancia                                        | —              | Activa/desactiva la predistorsión adaptativa en la radio.                                                                                                                                                                    |
| Active        | Indicador (verde)                                           | apagado        | Iluminado cuando APD está activado y el ecualizador se aplica activamente.                                                                                                                                                   |
| Cal           | Indicador (verde)                                           | apagado        | Iluminado cuando APD está activado y aún está calibrando.                                                                                                                                                                    |
| Avail         | Indicador (verde)                                           | apagado        | Iluminado cuando APD está activado y hay una calibración disponible pero aún no aplicada.                                                                                                                                    |
| Success       | Indicador (verde)                                           | apagado        | Se ilumina en verde cuando el estado del ATU es Successful u OK.                                                                                                                                                             |
| Byp           | Indicador (naranja)                                         | apagado        | Se ilumina en naranja cuando el ATU está en modo Bypass o ManualBypass.                                                                                                                                                      |
| Mem           | Indicador (verde)                                           | apagado        | Se ilumina en verde cuando el ATU está usando una memoria.                                                                                                                                                                   |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor de ROE se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil de TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias del ATU, considere recuperar una memoria conocida como buena antes de activar la transmisión para asegurarse de que la antena esté adaptada. Consulte [Recall an ATU memory](recall-an-atu-memory.md).
- Si el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de telefonía, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o el slice de TX no está en un modo de telefonía, **MOX** se comporta como en versiones anteriores.

## Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y pasar por alto el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se ilumina en verde cuando el sintonizador encuentra una adaptación.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es Successful u OK y no ha cambiado la frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente, el sintonizador cambia a bypass. El indicador **Byp** se ilumina en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era Successful u OK.
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-tune bands…** — Abre el diálogo de Pre-Sintonía para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias del ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú aparece atenuado con una información sobre herramientas que sugiere habilitar MEM primero.
- **Clear ATU memories…** — Borra todas las memorias del ATU almacenadas después de un diálogo de confirmación.

## Menú contextual del botón TUNE

Haga clic derecho en el botón **TUNE** para seleccionar la forma de la portadora para el siguiente ciclo de sintonía:

- **Mono Tone** — Tono único, la forma de portadora predeterminada.
- **Two Tone** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se conserva al reiniciar. El modo de sintonía de la radio vuelve al tono único por sí solo al reiniciar. Una marca de verificación junto a cada opción muestra el modo de sintonía actual de la radio.

## APD (Predistorsión Adaptativa)

El botón de alternancia **APD** activa o desactiva la predistorsión adaptativa en la radio. Cuando está activado, los tres indicadores de estado debajo del botón muestran el estado actual:

- **Active** — Iluminado en verde cuando el ecualizador se aplica activamente.
- **Cal** — Iluminado en verde cuando la radio aún está calibrando.
- **Avail** — Iluminado en verde cuando hay una calibración disponible pero aún no aplicada.

Los indicadores avanzan a través de Cal → Avail → Active a medida que el sistema APD completa su ciclo de calibración.

## Solución de problemas

- **MOX se activa pero RF Pwr lee cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de reactivar la transmisión.
- **La ROE se vuelve roja inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para desactivar, luego ejecute el ATU o verifique la línea de alimentación antes de continuar. Consulte [Run the internal ATU](run-the-internal-atu.md).
- **El medidor RF Pwr llega al fondo de escala** — El deslizador RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar, luego reduzca el deslizador RF Power antes de reactivar la transmisión.
- **El botón ATU inicia una nueva sintonía en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es esperado. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez una sintonía exitosa.
- **Los tonos Quindar se reproducen inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en la tira de canales de audio y el slice de TX está en un modo de telefonía. Si no desea tonos Quindar durante esta prueba, deshabilite el chip QUIN en la tira de canales de audio antes de activar la transmisión.

## Relacionados

- [Set RF output power](set-rf-output-power.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Switch TX profiles (e.g. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Run the internal ATU](run-the-internal-atu.md)
- [Recall an ATU memory](recall-an-atu-memory.md)
- Pre-tune bands for the ATU
- Clear ATU memories
