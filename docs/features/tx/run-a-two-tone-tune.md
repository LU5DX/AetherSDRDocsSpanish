# Ejecutar una prueba de dos tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación al activar el radio manualmente con MOX, mientras se monitorean la potencia directa y la ROS. Use este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra conexión activa).
- El applet TX Controls está visible. Si no lo está, haga clic en el botón TX del panel lateral derecho.
- El transceptor está configurado en modo SSB y opera en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea del radio.

## Pasos

1. En el applet TX Controls, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desea usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada del radio.
5. Haga clic en **MOX**. El botón se pone en rojo y el radio comienza a transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). Ajuste el control deslizante **RF Power** durante la transmisión para alcanzar la potencia de salida deseada.
7. Cuando la prueba haya concluido, haga clic nuevamente en **MOX** para dejar de transmitir. El botón vuelve a su estado apagado.
8. Detenga la fuente de audio de dos tonos.

## Función de cada control

| Control    | Tipo                  | Valor predeterminado |
|------------|-----------------------|----------------------|
| RF Power   | Control deslizante    | 100                  |
| Tune Pwr   | Control deslizante    | 10                   |
| TX Profile | Menú desplegable      | —                    |
| MOX        | Botón de alternancia  | Off                  |
| RF Pwr     | Medidor               | —                    |
| SWR        | Medidor               | —                    |

## Consejos

- Mantenga la ROS por debajo de 2.5 durante la prueba. El medidor SWR se pone en rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono desactivado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias de ATU, considere recuperar una memoria conocida como correcta antes de transmitir para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria de ATU](recall-an-atu-memory.md).

## Comportamiento del botón ATU (v0.9.5.1)

El botón **ATU** ahora alterna entre iniciar un ciclo de ajuste y puentear el sintonizador, reflejando el comportamiento por frecuencia de SmartSDR.

- **Primer clic en una nueva frecuencia** — inicia un nuevo ciclo de ajuste del ATU. El indicador **Success** se ilumina en verde cuando el sintonizador encuentra una coincidencia.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es Successful u OK y no ha cambiado de frecuencia desde el último ajuste, al hacer clic en **ATU** nuevamente se pone el sintonizador en modo puente. El indicador **Byp** se ilumina en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un nuevo ciclo de ajuste, incluso si el estado anterior era Successful u OK.
- **Después del modo puente** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un nuevo ciclo de ajuste independientemente de la frecuencia.

Los botones **ATU** y **MEM** están desactivados cuando TGXL está en modo OPERATE.

## Solución de problemas

- **MOX activa la transmisión pero RF Pwr indica cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada del radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a transmitir.
- **La ROS se pone inmediatamente en rojo al presionar MOX** — La antena no está adaptada. Haga clic en MOX para dejar de transmitir, luego ejecute el ATU o revise el cable coaxial antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al fondo de escala** — El control deslizante RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para dejar de transmitir y luego reduzca el control deslizante RF Power antes de volver a transmitir.
- **El botón ATU inicia un nuevo ajuste en lugar de puentear** — La frecuencia de transmisión cambió desde el último ajuste exitoso. Esto es normal. El botón solo cambiará al modo puente cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez un ajuste exitoso.

## Temas relacionados

- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Configurar la potencia de portadora de ajuste](set-tune-carrier-power.md)
- [Alternar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria de ATU](recall-an-atu-memory.md)
