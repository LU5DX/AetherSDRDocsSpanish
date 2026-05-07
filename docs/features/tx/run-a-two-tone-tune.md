# Ejecutar una prueba de tono doble

Una prueba de tono doble le permite verificar la linealidad del transmisor y los niveles de excitación activando la radio manualmente con MOX mientras monitorea la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra "connected").
- El applet TX Controls está visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y se encuentra en una frecuencia despejada.
- Una fuente de audio de tono doble (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet TX Controls, ajuste el deslizador **Tune Pwr** al nivel de potencia que desee usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100.
2. Ajuste el deslizador **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100.
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de tono doble desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio activa la transmisión.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). Ajuste el deslizador **RF Power** mientras transmite para alcanzar la salida deseada.
7. Cuando la prueba haya finalizado, haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado sin iluminar.
8. Detenga la fuente de audio de tono doble.

## Función de cada control

| Control    | Tipo                                                        | Valor predeterminado                                                                                                                                                                              |
|------------|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador                                                  | 100                                                                                                                                                                                               |
| Tune Pwr   | Deslizador                                                  | 10                                                                                                                                                                                                |
| TX Profile | Menú desplegable                                            | —                                                                                                                                                                                                 |
| MOX        | Alterna la transmisión manual; el botón se vuelve rojo mientras TX está activado. | En v0.9.7, al hacer clic se enruta a través de `requestPttOn`/`requestPttOff` para que los tonos Quindar (K/BK) se reproduzcan al activar/desactivar en modos de telefonía cuando el chip QUIN está habilitado en Audio Channel Strip. |
| RF Pwr     | Medidor                                                     | —                                                                                                                                                                                                 |
| SWR        | Medidor                                                     | —                                                                                                                                                                                                 |

## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor de ROE se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de tono doble. El procesamiento puede distorsionar la envolvente del tono doble y producir lecturas IMD engañosas.
- Si dispone de memorias de ATU, considere recuperar una memoria conocida antes de activar la transmisión para asegurarse de que la antena esté adaptada. Consulte [Recall an ATU memory](recall-an-atu-memory.md).
- En v0.9.7, si el chip QUIN está habilitado en Audio Channel Strip y el slice TX activo está en un modo de telefonía, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o el slice TX no está en un modo de telefonía, **MOX** se comporta como en versiones anteriores.

## Comportamiento del botón ATU (v0.9.5.1)

El botón **ATU** ahora alterna entre iniciar un ciclo de sintonía y pasar por alto el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se ilumina en verde cuando el sintonizador encuentra una adaptación.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es "Successful" u "OK" y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente cambia el sintonizador a bypass. El indicador **Byp** se ilumina en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era "Successful" u "OK".
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo sin importar la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

## Solución de problemas

- **MOX activa la transmisión pero RF Pwr muestra cero** — Es posible que la fuente de audio de tono doble no esté llegando a la entrada de la radio, o que el modo no sea SSB. Confirme el enrutamiento de audio y la selección de modo antes de volver a activar.
- **La ROE se vuelve roja inmediatamente al presionar MOX** — La antena no está adaptada. Haga clic en MOX para desactivar, luego ejecute el ATU o revise la línea de alimentación antes de continuar. Consulte [Run the internal ATU](run-the-internal-atu.md).
- **El medidor de RF Pwr llega al fondo de escala** — El deslizador RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar, luego reduzca el deslizador RF Power antes de volver a activar.
- **El botón ATU inicia una nueva sintonía en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es normal. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez una sintonía exitosa.
- **Los tonos Quindar se reproducen inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en Audio Channel Strip y el slice TX está en un modo de telefonía. Si no desea tonos Quindar durante esta prueba, deshabilite el chip QUIN en Audio Channel Strip antes de activar la transmisión.

## Relacionados

- [Set RF output power](set-rf-output-power.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Switch TX profiles (e.g. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Run the internal ATU](run-the-internal-atu.md)
- [Recall an ATU memory](recall-an-atu-memory.md)
