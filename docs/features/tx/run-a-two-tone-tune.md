# Ejecutar una prueba de dos tonos

Una prueba de dos tonos permite verificar la linealidad del transmisor y los niveles de excitación activando el radio manualmente con MOX, mientras se monitorean la potencia directa y el ROS. Utilice este procedimiento cuando el equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador del radio muestra conexión activa).
- El applet TX Controls está visible. Si no lo está, haga clic en el botón TX tray en la barra lateral derecha.
- El transceptor está configurado en modo SSB y se encuentra en una frecuencia libre.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o línea del radio.

## Pasos

1. En el applet TX Controls, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desea usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea utilizar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada del radio.
5. Haga clic en **MOX**. El botón se pone en rojo y el radio comienza a transmitir.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). Ajuste el control deslizante **RF Power** mientras transmite para alcanzar la potencia de salida deseada.
7. Cuando la prueba haya concluido, haga clic nuevamente en **MOX** para dejar de transmitir. El botón vuelve a su estado apagado.
8. Detenga la fuente de audio de dos tonos.

## Función de cada control

| Control | Tipo | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|---|
| RF Power | Deslizador | 100 | 0–100 | Establece el nivel de potencia de RF en transmisión. |
| Tune Pwr | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía (no se usa durante MOX, pero configúrelo antes de cambiar de modo). |
| TX Profile | Menú desplegable | — | Cargado desde el radio | Carga el perfil de transmisión seleccionado. |
| MOX | Botón de alternancia | Off | Off / On (rojo) | Activa el transmisor manualmente. El botón se pone en rojo mientras TX está activo. |
| RF Pwr | Medidor | — | 0–120 W; rojo > 100 W | Muestra la potencia directa en la salida del excitador. |
| SWR | Medidor | — | 1.0–3.0; rojo > 2.5 | Muestra la relación de ondas estacionarias en el excitador. |

## Consejos

- Mantenga el ROS por debajo de 2.5 durante la prueba. El medidor SWR se pone en rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX con el procesamiento de micrófono desactivado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de los dos tonos y producir lecturas de IMD engañosas.
- Si dispone de memorias del ATU, considere recuperar una memoria conocida como válida antes de activar el transmisor para asegurarse de que la antena esté adaptada. Consulte [Recuperar una memoria del ATU](recall-an-atu-memory.md).

## Resolución de problemas

- **MOX activa el transmisor pero RF Pwr indica cero** — Es posible que la fuente de audio de dos tonos no esté llegando a la entrada del radio, o que el modo no sea SSB. Verifique el enrutamiento de audio y la selección de modo antes de volver a transmitir.
- **El SWR se pone en rojo inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para dejar de transmitir, luego use el ATU o revise la línea de alimentación antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al límite máximo** — El control deslizante RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para dejar de transmitir y luego reduzca el control deslizante RF Power antes de volver a transmitir.

## Temas relacionados

- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
