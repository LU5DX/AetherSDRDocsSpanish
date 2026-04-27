# Iniciar una portadora de ajuste para verificar la ROE

Envíe una portadora continua a potencia reducida para leer la ROE (relación de onda estacionaria) en su sistema de antena. Utilice este procedimiento antes de un QSO o después de cambiar antenas para confirmar una buena adaptación de impedancia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls solo está activo con una conexión de radio en vivo.
- Asegúrese de que la frecuencia esté libre para transmitir (la banda debe estar legalmente disponible para su estación).
- Configure la potencia de ajuste a un nivel apropiado para su sistema de antena. El valor predeterminado es 10; consulte [Configurar la potencia de la portadora de ajuste](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón TX del panel lateral derecho para abrir el applet TX Controls si aún no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El indicador **SWR** se actualiza en tiempo real. La escala va de 1,0 a 3,0; las lecturas superiores a 2,5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa a la salida del excitador.
4. Lea el valor de ROE en el indicador **SWR**.
5. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo desaparece.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Descripción |
|---|---|---|---|---|
| **TUNE** | Botón pulsador | — | — | Inicia o detiene la portadora de ajuste. La etiqueta muestra **TUNING...** con fondo rojo mientras está activo. |
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de la portadora de ajuste enviado a la radio. |
| **RF Pwr** | Medidor | — | 0–120 W (rojo por encima de 100 W) | Muestra la potencia directa a la salida del excitador durante la transmisión. |
| **SWR** | Medidor | — | 1,0–3,0 (rojo por encima de 2,5) | Muestra la relación de onda estacionaria en el excitador. |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar una ROE razonable.
- El indicador **SWR** se vuelve rojo por encima de 2,5. Si llega al límite de 3,0, detenga la portadora y verifique el cable coaxial y las conexiones de la antena antes de continuar.
- Para utilizar el ATU interno en lugar de verificar la ROE manualmente, haga clic en **ATU** después de que la portadora de ajuste confirme que la antena es utilizable. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante el ajuste, configúrelas en `Settings > Inhibit during TUNE`.

## Solución de problemas

- **El botón TUNE no responde** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre la radio como conectada antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede estar en cero o muy cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en estado **TUNING...**, verifique la conexión de radio; una conexión interrumpida puede dejar el estado de transmisión sin confirmar.

## Relacionado

- [Configurar la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Activar MOX para manipular manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
