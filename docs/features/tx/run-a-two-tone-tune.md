# Ejecutar una Prueba de Dos Tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación activando manualmente el equipo con MOX mientras se monitorean la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra "connected").
- El applet TX Controls está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y en una frecuencia despejada.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet TX Controls, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desee usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en vatios (ej. "10 W").
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en vatios (ej. "100 W").
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio se activa para transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de decaer hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente cuando desactiva la transmisión. Ajuste el control deslizante **RF Power** mientras transmite para alcanzar la salida deseada.
7. Cuando la prueba haya terminado, haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado sin iluminación.
8. Detenga la fuente de audio de dos tonos.

## Función de cada control

| Control    | Tipo                                                        | Valor predeterminado                                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Control deslizante                                          | 100                                                                                                                                                                                                                                              |
| Tune Pwr   | Control deslizante                                          | 10                                                                                                                                                                                                                                               |
| TX Profile | Menú desplegable                                            | —                                                                                                                                                                                                                                                |
| MOX        | Alterna la transmisión manual; el botón se vuelve rojo mientras TX está activo. | En v0.9.7, el clic se enruta a través de `requestPttOn`/`requestPttOff` para que los tonos Quindar (K/BK) se reproduzcan al activar/desactivar en modos de telefonía cuando el chip QUIN está habilitado en el Audio Channel Strip. |
| RF Pwr     | Medidor                                                     | —                                                                                                                                                                                                                                                |
| SWR        | Medidor                                                     | —                                                                                                                                                                                                                                                |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor SWR se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono deshabilitado antes de realizar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas IMD engañosas.
- Si dispone de memorias ATU, considere recuperar una memoria conocida antes de activar la transmisión para asegurarse de que la antena esté acoplada. Consulte [Recall an ATU memory](recall-an-atu-memory.md).
- En v0.9.7, si el chip QUIN está habilitado en el Audio Channel Strip y el slice TX activo está en un modo de telefonía, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o el slice TX no está en un modo de telefonía, **MOX** se comporta como en versiones anteriores.

## Comportamiento del botón ATU (v0.9.5.1)

El botón **ATU** ahora alterna entre iniciar un ciclo de sintonía y puentear el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una nueva frecuencia** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se enciende en verde cuando el sintonizador encuentra una coincidencia.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es "Successful" u "OK" y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente, el sintonizador se pone en modo bypass. El indicador **Byp** se enciende en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era "Successful" u "OK".
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando el TGXL está en modo OPERATE.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-tune bands…** — Abre el diálogo Pre-Tune para realizar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú aparece atenuado con una información sobre herramientas que sugiere habilitar MEM primero.
- **Clear ATU memories…** — Borra todas las memorias ATU almacenadas después de un diálogo de confirmación.

## Menú contextual del botón TUNE (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para seleccionar la forma de la portadora para el próximo ciclo de sintonía:

- **Mono Tone** — Tono único, la forma de portadora predeterminada.
- **Two Tone** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se conserva entre ciclos de alimentación. El modo de sintonía de la radio vuelve al tono único por sí solo entre ciclos de alimentación. Una marca de verificación junto a cada entrada muestra el modo de sintonía actual de la radio.

## Solución de problemas

- **MOX activa pero RF Pwr marca cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a activar la transmisión.
- **SWR se pone rojo inmediatamente al presionar MOX** — La antena no está acoplada. Haga clic en MOX para desactivar, luego ejecute el ATU o revise la línea de alimentación antes de continuar. Consulte [Run the internal ATU](run-the-internal-atu.md).
- **El medidor RF Pwr marca a fondo de escala** — El control deslizante RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar, luego reduzca el control deslizante RF Power antes de volver a activar la transmisión.
- **El botón ATU inicia una nueva sintonía en lugar de puentear** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es normal. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez una sintonía exitosa.
- **Los tonos Quindar se reproducen inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en el Audio Channel Strip y el slice TX está en un modo de telefonía. Si no desea tonos Quindar durante esta prueba, deshabilite el chip QUIN en el Audio Channel Strip antes de activar la transmisión.

## Relacionados

- [Set RF output power](set-rf-output-power.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Switch TX profiles (e.g. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Run the internal ATU](run-the-internal-atu.md)
- [Recall an ATU memory](recall-an-atu-memory.md)
- Pre-tune bands for the ATU
- Clear ATU memories
