# Iniciar una portadora de sintonía para verificar la ROE

Envía una portadora continua a potencia reducida para leer la ROE en su sistema de antena. Utilícelo antes de un QSO o después de cambiar de antenas para confirmar una buena adaptación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls solo está activo con una conexión de radio en vivo.
- Asegúrese de tener permiso para transmitir en la frecuencia (la banda debe estar legalmente abierta para su estación).
- Ajuste la potencia de sintonía a un nivel adecuado para su sistema de antena. El valor predeterminado es 10; consulte [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón de la bandeja TX en la barra lateral derecha para abrir el applet TX Controls si aún no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El indicador **SWR** se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa en la salida del excitador.
4. Lea el valor de ROE del indicador **SWR**.
5. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo desaparece.

## Qué hace cada control

| Control      | Tipo          | Valor predeterminado |
|--------------|---------------|----------------------|
| **TUNE**     | Botón pulsador | —                    |
| **Tune Pwr** | Control deslizante | 10               |
| **RF Pwr**   | Medidor        | —                    |
| **SWR**      | Medidor        | —                    |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar una ROE razonable.
- El indicador **SWR** se vuelve rojo por encima de 2.5. Si llega a 3.0, detenga la portadora y verifique las conexiones de su línea de transmisión y antena antes de continuar.
- Para ejecutar la ATU interna en lugar de verificar la ROE manualmente, haga clic en **ATU** después de que la portadora de sintonía confirme que la antena es utilizable. Consulte [Ejecutar la ATU interna](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, configúrelas en `Settings > Inhibit during TUNE`.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de la v0.9.5.1, el botón **ATU** se comporta como un conmutador que tiene en cuenta la frecuencia, en lugar de iniciar siempre un nuevo ciclo de sintonía. La lógica refleja el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o después de un cambio de frecuencia)** — Inicia un nuevo ciclo de sintonía de la ATU.
- **Segundo clic en la misma frecuencia** — Si la ATU ya ha informado una adaptación exitosa (indicador **Success** o **Mem** encendido) y la frecuencia de transmisión no ha cambiado desde esa sintonía, al hacer clic en **ATU** se cambia el sintonizador a bypass en lugar de iniciar otro ciclo.
- **Después de cualquier cambio de frecuencia** — La frecuencia de sintonía guardada se borra. El siguiente clic en **ATU** siempre inicia un nuevo ciclo de sintonía, incluso si el resultado anterior fue exitoso.

Cuando la ATU entra en bypass, el registro de frecuencia sintonizada también se borra, por lo que el siguiente clic iniciará una nueva sintonía independientemente de la frecuencia.

Este cambio no afecta al botón **MEM** ni a los indicadores de estado de la ATU (**Success**, **Byp**, **Mem**), que continúan comportándose como se describe a continuación.

## MOX y tonos Quindar (v0.9.7)

A partir de la v0.9.7, al hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando el chip QUIN está habilitado en la tira de canal de audio y el slice TX activo está en un modo de telefonía, el tono K suena al activar PTT y el tono BK suena al desactivar PTT. Cuando Quindar está deshabilitado o el slice TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores.

Este cambio afecta solo al botón **MOX** en el applet TX Controls. El PTT por hardware, VOX y otras fuentes de PTT no se ven afectadas.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre la radio como conectada antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede estar en cero o cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en el estado **TUNING...**, verifique la conexión de la radio; una conexión perdida puede dejar el estado de transmisión sin confirmar.
- **El botón ATU pasa por alto el sintonizador en lugar de resintonizar** — Este es un comportamiento esperado cuando la ATU ya tiene una adaptación exitosa en la frecuencia actual. Cambie de frecuencia o espere a que el sintonizador borre su resultado, luego haga clic en **ATU** nuevamente para iniciar un nuevo ciclo de sintonía.
- **MOX activa el transmisor pero no se escuchan tonos Quindar** — Confirme que el chip QUIN esté habilitado en la tira de canal de audio y que el slice TX activo esté configurado en un modo de telefonía (USB, LSB, AM, FM o similar). Los tonos Quindar no se reproducen en modos CW o digitales.

## Relacionados

- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Ejecutar la ATU interna](run-the-internal-atu.md)
- [Recuperar una memoria de la ATU](recall-an-atu-memory.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Activar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
