# Activar MOX para transmitir manualmente

MOX le permite transmitir sin un pedal de control o línea PTT. Úselo para verificar el audio, probar su señal o transmitir cuando el PTT por hardware no está disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está desconectada.
- Confirme que su perfil de TX y el nivel de RF Power están configurados correctamente antes de transmitir.

## Pasos

1. Si la ventana TX Controls no es visible, haga clic en el botón **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para transmitir. El botón se vuelve rojo mientras TX está activo.
4. Haga clic en **MOX** nuevamente para dejar de transmitir. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control          | Comportamiento                                                                                               | Predeterminado |
|------------------|--------------------------------------------------------------------------------------------------------|---------|
| **MOX**          | Activa o desactiva la transmisión manual. El botón se vuelve rojo mientras el transmisor está activo.                     | Off     |
| **RF Power**     | Establece el nivel de potencia RF de transmisión enviado a la radio.                                                    | 100     |
| **RF Pwr** meter | Muestra la potencia directa en la salida del excitador. Se vuelve rojo por encima de 100 W (barefoot) o 500 W (Aurora 500W). | —       |
| **SWR** meter    | Muestra la relación de ondas estacionarias en el excitador. Se vuelve rojo por encima de 2.5.                                      | —       |

## Consejos

- Vigile los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si el SWR supera 2.5 (zona roja), desactive inmediatamente e investigue su sistema de antena.
- Establezca **RF Power** a un valor bajo antes de usar MOX por primera vez en una banda nueva.
- MOX activa la radio en transmisión a potencia completa en el modo que esté activo. Si solo necesita verificar SWR o sintonizar un ATU, use **TUNE** en su lugar — transmite una portadora a un nivel **Tune Pwr** más bajo.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR está conectado a la radio. La ventana TX Controls requiere una conexión activa a la radio.
- **El transmisor se activa pero no muestra potencia RF** — Verifique que **RF Power** no esté establecido en 0 y que el perfil TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX una segunda vez** — Otra fuente PTT (pedal, VOX, comando CAT) puede estar manteniendo la radio activa. Verifique el hardware PTT externo y cualquier cliente CAT conectado.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de sintonización para verificar SWR](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
