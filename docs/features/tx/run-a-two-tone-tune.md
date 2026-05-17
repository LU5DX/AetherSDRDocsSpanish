# Ejecutar una Tono de Dos Tonos

Una prueba de dos tonos le permite comprobar la linealidad del transmisor y los niveles de excitación activando la radio manualmente con MOX mientras monitorea la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra conectado).
- El applet Controles de TX está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y se encuentra en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet Controles de TX, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desee usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio activa la transmisión.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de disminuir hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente cuando desactiva la transmisión. Ajuste el control deslizante **RF Power** mientras transmite para alcanzar su salida objetivo.
7. Cuando la prueba esté completa, haga clic en **MOX** nuevamente para desactivar la transmisión. El botón vuelve a su estado sin iluminar.
8. Detenga la fuente de audio de dos tonos.

## Qué hace cada control

| Control    | Tipo                                                        | Predeterminado                                                                                                                                                                                                                                  |
|------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Control deslizante                                          | 100                                                                                                                                                                                                                                             |
| Tune Pwr   | Control deslizante                                          | 10                                                                                                                                                                                                                                              |
| TX Profile | Menú desplegable                                            | —                                                                                                                                                                                                                                               |
| MOX        | Activa/desactiva la transmisión manual; el botón se vuelve rojo mientras TX está activa. | En v0.9.7, el clic se enruta a través de `requestPttOn`/`requestPttOff` para que los tonos Quindar (K/BK) suenen al activar/desactivar en modos de teléfono cuando el chip QUIN está habilitado en la tira de canales de audio. |
| RF Pwr     | Medidor                                                     | —                                                                                                                                                                                                                                               |
| SWR        | Medidor                                                     | —                                                                                                                                                                                                                                               |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor SWR se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas IMD engañosas.
- Si dispone de memorias ATU, considere recuperar una memoria conocida como buena antes de activar la transmisión para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria ATU](recall-an-atu-memory.md).
- En v0.9.7, si el chip QUIN está habilitado en la tira de canales de audio y la división TX activa está en un modo de teléfono, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o la división TX no está en un modo de teléfono, **MOX** se comporta como en versiones anteriores.

## Comportamiento del botón ATU (v0.9.5.1)

El botón **ATU** ahora alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se ilumina en verde cuando el sintonizador encuentra una adaptación.
- **Segundo clic en la misma frecuencia** — si el estado de ATU ya es Exitoso u OK y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente el sintonizador cambia a modo de omisión. El indicador **Byp** se ilumina en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era Exitoso u OK.
- **Después de la omisión** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-tune bands…** — Abre el diálogo de Pre-sintonía para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú aparece atenuado con una sugerencia que indica que primero habilite MEM.
- **Clear ATU memories…** — Borra todas las memorias ATU almacenadas después de un diálogo de confirmación.

## Menú contextual del botón TUNE (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para seleccionar la forma de la portadora para el siguiente ciclo de sintonía:

- **Mono Tone** — Tono único, la forma de portadora predeterminada.
- **Two Tone** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se conserva entre ciclos de encendido. El modo de sintonía de la radio vuelve al tono único por sí solo entre ciclos de encendido. Una marca de verificación junto a cada entrada muestra el modo de sintonía actual de la radio.

## Solución de problemas

- **MOX activa pero RF Pwr lee cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a activar la transmisión.
- **SWR se vuelve rojo inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para desactivar la transmisión, luego ejecute el ATU o verifique la línea de alimentación antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr marca a fondo de escala** — El control deslizante RF Power está ajustado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar la transmisión, luego reduzca el control deslizante RF Power antes de volver a activar la transmisión.
- **El botón ATU inicia una nueva sintonía en lugar de omitir** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es esperado. El botón solo cambiará a omisión cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez una sintonía exitosa.
- **Los tonos Quindar suenan inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en la tira de canales de audio y la división TX está en un modo de teléfono. Si no desea tonos Quindar durante esta prueba, deshabilite el chip QUIN en la tira de canales de audio antes de activar la transmisión.

## Relacionados

- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (ej. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria ATU](recall-an-atu-memory.md)
- [Pre-sintonizar bandas para el ATU](pre-tune-bands-for-the-atu.md)
- [Borrar memorias ATU](clear-atu-memories.md)
