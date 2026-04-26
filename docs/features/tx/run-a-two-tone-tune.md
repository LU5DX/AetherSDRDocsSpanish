# Ejecutar una prueba de dos tonos

Una prueba de dos tonos le permite activar el transmisor a un nivel de potencia controlado para verificar la linealidad, ajustar la excitación o comprobar el SWR antes de operar. Para ello, establezca un nivel de potencia de sintonía y active la portadora de sintonía mediante TUNE o MOX desde el applet TX Controls.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Use `Settings > Connect to Radio...` si aún no está conectado.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón TX tray en la barra lateral derecha.
- Confirme que opera dentro de una frecuencia y un nivel de potencia permitidos por su licencia y las regulaciones locales.
- Notifique a otros en la frecuencia antes de transmitir.

## Pasos

1. En el applet TX Controls, localice el control deslizante **Tune Pwr**.
2. Ajuste **Tune Pwr** al nivel de potencia de portadora deseado. El valor predeterminado es 10; el rango válido es 0–100.
3. Confirme que el control deslizante **RF Power** está en el nivel que desea para la operación a plena potencia (predeterminado 100, rango 0–100). Esto no afecta la potencia de la portadora de sintonía, pero verificarlo ahora evita sorpresas después de sintonizar.
4. Observe el indicador **SWR** (rango 1.0–3.0; rojo por encima de 2.5) y el indicador **RF Pwr** (rango 0–120 W sin amplificador externo, rojo por encima de 100 W) — ambos se actualizan en tiempo real durante la transmisión.
5. Haga clic en **TUNE**. La etiqueta del botón cambia a **TUNING...** con fondo rojo mientras la portadora está activa.
6. Observe los indicadores **RF Pwr** y **SWR**. Cuando haya obtenido las lecturas que necesita, haga clic en **TUNE** nuevamente para detener. El botón regresa a **TUNE**.

De forma alternativa, para activar el transmisor de manera continua a plena potencia RF para una prueba de dos tonos o IMD usando audio externo:

1. Ajuste **RF Power** al nivel de excitación deseado.
2. Haga clic en **MOX**. El botón se pone rojo mientras el transmisor está activado.
3. Aplique su fuente de audio de dos tonos a través de la entrada de audio del radio.
4. Haga clic en **MOX** nuevamente para volver a recepción. El botón regresa a su estado apagado.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| **RF Pwr** | Indicador | — | 0–120 W (sin amplificador externo); rojo por encima de 100 W | Muestra la potencia directa en la salida del excitador. |
| **SWR** | Indicador | — | 1.0–3.0; rojo por encima de 2.5 | Muestra la relación de onda estacionaria en el excitador. |
| **RF Power** | Deslizador | 100 | 0–100 | Establece el nivel de potencia RF de transmisión. |
| **Tune Pwr** | Deslizador | 10 | 0–100 | Establece el nivel de potencia de la portadora de sintonía. |
| **TUNE** | Botón | — | TUNE / TUNING... | Inicia o detiene la portadora de sintonía. La etiqueta cambia a **TUNING...** con fondo rojo mientras está activo. |
| **MOX** | Botón de alternancia | Off | Off (azul) / On (rojo) | Activa el transmisor manualmente. El botón se pone rojo durante la transmisión. |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) cuando use la portadora de sintonía para la operación del sintonizador de antena, a fin de proteger el amplificador final.
- Si necesita ejecutar el ATU interno antes de la prueba de dos tonos, haga clic en **ATU** primero. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- El indicador **SWR** se pone rojo por encima de 2.5. Si el SWR es alto durante la portadora de sintonía, detenga la transmisión y verifique su sistema de antena antes de aumentar la potencia.

## Solución de problemas

- **El botón TUNE no hace nada** — Confirme que el radio está conectado. El applet TX Controls requiere una conexión de radio activa.
- **El indicador RF Pwr marca cero durante TUNING...** — Verifique que **Tune Pwr** esté por encima de 0. Si el deslizador está en 0, no se transmite ninguna portadora.
- **SWR indica un valor alto de inmediato** — La antena o el cable de alimentación pueden tener una falla. Reduzca **Tune Pwr**, corrija el problema de la antena y vuelva a intentarlo.
- **MOX activa pero no se transmite audio** — Verifique que su fuente de audio de dos tonos esté enrutada a la entrada de audio correcta del radio. El enrutamiento de audio está fuera del applet TX Controls; consulte la configuración de audio de su sistema.

## Relacionado

- [Iniciar una portadora de sintonía para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
