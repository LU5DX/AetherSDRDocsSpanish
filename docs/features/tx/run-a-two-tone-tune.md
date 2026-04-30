# Ejecutar un Ajuste de Dos Tonos

Un ajuste de dos tonos le permite verificar la linealidad del transmisor y los niveles de potencia al activar la radio manualmente con MOX mientras supervisa la potencia reflejada y el ROS. Use este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra conexión).
- El applet TX Controls es visible. Si no lo es, haga clic en el botón TX tray en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y está en una frecuencia despejada.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o línea de la radio.

## Pasos

1. En el applet TX Controls, configure el regulador **Tune Pwr** al nivel de potencia que desea usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Configure el regulador **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que esté alimentando la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio se activa.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1,0–3,0, rojo por encima de 2,5). Ajuste el regulador **RF Power** mientras transmite para alcanzar su salida objetivo.
7. Cuando la prueba se complete, haga clic en **MOX** nuevamente para desactivar el transmisor. El botón regresa a su estado apagado.
8. Detenga la fuente de audio de dos tonos.

## Qué hace cada control

| Control    | Tipo          | Predeterminado |
|------------|---------------|---------|
| RF Power   | Regulador     | 100     |
| Tune Pwr   | Regulador     | 10      |
| TX Profile | Menú desplegable | —       |
| MOX        | Botón de alternar | Apagado |
| RF Pwr     | Medidor       | —       |
| SWR        | Medidor       | —       |

## Consejos

- Mantenga el ROS por debajo de 2,5 durante la prueba. El medidor SWR se vuelve rojo por encima de 2,5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas de IMD engañosas.
- Si tiene memorias ATU disponibles, considere recuperar una memoria conocida como buena antes de activar para asegurar que la antena esté acoplada. Consulte [Recuperar una memoria ATU](recall-an-atu-memory.md).

## Solución de problemas

- **MOX se activa pero RF Pwr marca cero** — La fuente de audio de dos tonos puede no estar llegando a la entrada de la radio, o el modo no es SSB. Confirme el enrutamiento de audio y la selección de modo antes de reactivar.
- **SWR se vuelve inmediatamente rojo cuando se presiona MOX** — La antena está desacoplada. Haga clic en MOX para desactivar, luego ejecute el ATU o verifique la línea de transmisión antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al máximo** — El regulador RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar, luego reduzca el regulador RF Power antes de reactivar.

## Relacionado

- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Establecer la potencia de portadora de ajuste](set-tune-carrier-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria ATU](recall-an-atu-memory.md)
