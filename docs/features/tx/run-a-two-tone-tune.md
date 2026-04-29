# Ejecutar una prueba de dos tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación presionando la tecla del radio manualmente con MOX, mientras se monitorean la potencia directa y el ROS. Use este procedimiento cuando el equipo esté en modo SSB y desee verificar la salida sin transmitir audio real.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador del radio muestra conexión activa).
- El applet TX Controls está visible. Si no lo está, haga clic en el botón TX del panel lateral derecho.
- El transceptor está configurado en modo SSB y se encuentra en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o línea del radio.

## Pasos

1. En el applet TX Controls, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desea usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada del radio.
5. Haga clic en **MOX**. El botón se pone rojo y el radio comienza a transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). Ajuste el control deslizante **RF Power** mientras transmite para alcanzar la potencia de salida deseada.
7. Cuando la prueba haya concluido, haga clic en **MOX** nuevamente para dejar de transmitir. El botón regresa a su estado apagado.
8. Detenga la fuente de audio de dos tonos.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|---|
| RF Power | Deslizador | 100 | 0–100 | Establece el nivel de potencia RF de transmisión. |
| Tune Pwr | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de ajuste (no se usa durante MOX, pero configúrelo antes de cambiar de modo). |
| TX Profile | Menú desplegable | — | Proviene del radio | Carga el perfil de transmisión seleccionado. |
| MOX | Botón de alternancia | Off | Off / On (rojo) | Activa el transmisor manualmente. El botón se pone rojo mientras TX está activo. |
| RF Pwr | Medidor | — | 0–120 W; rojo > 100 W | Muestra la potencia directa en la salida del excitador. |
| SWR | Medidor | — | 1.0–3.0; rojo > 2.5 | Muestra la relación de onda estacionaria en el excitador. |

## Consejos

- Mantenga el ROS por debajo de 2.5 durante la prueba. El medidor SWR se pone rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX con el procesamiento de micrófono desactivado antes de realizar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias del ATU, considere recuperar una memoria conocida como válida antes de transmitir para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria del ATU](recall-an-atu-memory.md).

## Solución de problemas

- **MOX activa la transmisión pero RF Pwr indica cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada del radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a transmitir.
- **El SWR se pone rojo inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para dejar de transmitir, luego active el ATU o verifique la línea de alimentación antes de continuar. Consulte [Activar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al límite máximo** — El control deslizante RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para dejar de transmitir, luego reduzca el control deslizante RF Power antes de volver a transmitir.

## Relacionados

- [Configurar la potencia de salida RF](set-rf-output-power.md)
- [Configurar la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Alternar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Activar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
