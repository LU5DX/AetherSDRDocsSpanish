# Iniciar una portadora de ajuste para verificar la ROE

Envíe una portadora continua a potencia reducida para leer la ROE (Relación de Onda Estacionaria) en su sistema de antena. Use esta función antes de un QSO o después de cambiar antenas para confirmar una buena adaptación de impedancias.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls solo está activo con una conexión de radio en vivo.
- Asegúrese de que está autorizado para transmitir en la frecuencia (la banda debe estar legalmente disponible para su estación).
- Configure la potencia de ajuste a un nivel apropiado para su sistema de antena. El valor predeterminado es 10; consulte [Configurar la potencia de la portadora de ajuste](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón TX tray en la barra lateral derecha para abrir el applet TX Controls si no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El indicador **SWR** se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa en la salida del excitador.
4. Lea el valor de ROE en el indicador **SWR**.
5. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo desaparece.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Descripción |
|---|---|---|---|---|
| **TUNE** | Botón pulsador | — | — | Inicia o detiene la portadora de ajuste. La etiqueta muestra **TUNING...** con fondo rojo mientras está activo. |
| **Tune Pwr** | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de la portadora de ajuste enviado al radio. |
| **RF Pwr** | Medidor | — | 0–120 W (rojo por encima de 100 W) | Muestra la potencia directa en la salida del excitador durante la transmisión. |
| **SWR** | Medidor | — | 1.0–3.0 (rojo por encima de 2.5) | Muestra la relación de onda estacionaria en el excitador. |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar una ROE razonable.
- El indicador **SWR** se vuelve rojo por encima de 2.5. Si llega al tope en 3.0, detenga la portadora y verifique las conexiones de su línea de alimentación y antena antes de continuar.
- Para usar el sintonizador de antena (ATU) interno en lugar de verificar la ROE manualmente, haga clic en **ATU** después de que la portadora de ajuste confirme que la antena es utilizable. Consulte [Usar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante el ajuste, configúrelas en `Settings > Inhibit during TUNE`.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre el radio como conectado antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede ser cero o cercana a cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en el estado **TUNING...**, verifique la conexión del radio; una conexión interrumpida puede dejar el estado de transmisión sin confirmación.

## Relacionados

- [Configurar la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Activar MOX para transmitir manualmente](toggle-mox-to-manually-key-the-transmitter.md)
