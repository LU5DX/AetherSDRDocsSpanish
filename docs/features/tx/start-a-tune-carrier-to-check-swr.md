# Iniciar una portadora de ajuste para verificar el ROE

Envíe una portadora continua a potencia reducida para leer el ROE (relación de onda estacionaria) en su sistema de antena. Haga esto antes de un QSO o después de cambiar antenas para confirmar una buena adaptación de impedancia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls solo está activo con una conexión de radio en vivo.
- Asegúrese de que puede transmitir en la frecuencia (la banda debe estar legalmente disponible para su estación).
- Establezca la potencia de ajuste en un nivel apropiado para su sistema de antena. El valor predeterminado es 10; consulte [Establecer la potencia de la portadora de ajuste](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón TX tray en la barra lateral derecha para abrir el applet TX Controls si no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se pone rojo mientras la portadora está activa.
   - El indicador **SWR** se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa a la salida del excitador.
4. Lea el valor de ROE en el indicador **SWR**.
5. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo desaparece.

## Qué hace cada control

| Control      | Tipo               | Predeterminado |
|--------------|--------------------|----------------|
| **TUNE**     | Botón pulsador     | —              |
| **Tune Pwr** | Control deslizante | 10             |
| **RF Pwr**   | Medidor            | —              |
| **SWR**      | Medidor            | —              |

## Consejos

- Mantenga **Tune Pwr** en un valor bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar un ROE razonable.
- El indicador **SWR** se pone rojo por encima de 2.5. Si llega al límite de 3.0, detenga la portadora y revise el cable coaxial y las conexiones de antena antes de continuar.
- Para utilizar el ATU interno en lugar de verificar el ROE manualmente, haga clic en **ATU** después de que la portadora de ajuste confirme que la antena es utilizable. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante el ajuste, configúrelas en `Settings > Inhibit during TUNE`.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de la v0.9.5.1, el botón **ATU** funciona como un conmutador con memoria por frecuencia en lugar de iniciar siempre un nuevo ciclo de ajuste. La lógica refleja el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o después de un cambio de frecuencia)** — Inicia un ciclo de ajuste ATU nuevo.
- **Segundo clic en la misma frecuencia** — Si el ATU ya ha reportado una adaptación exitosa (indicador **Success** o **Mem** encendido) y la frecuencia de transmisión no ha cambiado desde ese ajuste, hacer clic en **ATU** coloca el sintonizador en bypass en lugar de iniciar otro ciclo.
- **Después de cualquier cambio de frecuencia** — La frecuencia de ajuste guardada se borra. El siguiente clic en **ATU** siempre inicia un ciclo de ajuste nuevo, incluso si el resultado anterior fue exitoso.

Cuando el ATU entra en bypass, el registro de frecuencia ajustada también se borra, por lo que el siguiente clic iniciará un ajuste nuevo independientemente de la frecuencia.

Este cambio no afecta al botón **MEM** ni a los indicadores de estado del ATU (**Success**, **Byp**, **Mem**), que continúan funcionando como se describe a continuación.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre la radio como conectada antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede ser cero o estar cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en estado **TUNING...**, revise la conexión de radio; una conexión interrumpida puede dejar el estado de transmisión sin confirmar.
- **El botón ATU coloca el sintonizador en bypass en lugar de reajustar** — Este es el comportamiento esperado cuando el ATU ya tiene una adaptación exitosa en la frecuencia actual. Cambie de frecuencia o espere a que el sintonizador borre su resultado, luego haga clic en **ATU** nuevamente para iniciar un ciclo de ajuste nuevo.

## Temas relacionados

- [Establecer la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Usar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
