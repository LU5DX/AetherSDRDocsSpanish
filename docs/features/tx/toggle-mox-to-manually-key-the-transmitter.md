# Activar MOX para manejar el transmisor manualmente

MOX permite manejar el transmisor sin un pedal ni una línea PTT. Úselo para verificar el audio, probar su señal o transmitir cuando el PTT por hardware no esté disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está desconectada.
- Confirme que su perfil de TX y el nivel de **RF Power** estén configurados correctamente antes de manejar el transmisor.

## Pasos

1. Si el applet TX Controls no está visible, haga clic en el botón **TX** de la bandeja en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para manejar el transmisor. El botón se vuelve rojo mientras la transmisión está activa.
4. Haga clic en **MOX** nuevamente para liberar el transmisor. El botón regresa a su estado apagado.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango |
|---------|---------------|----------------------|-------|
| **MOX** | Activa o desactiva la transmisión manual. El botón se vuelve rojo mientras el transmisor está manualizado. | Off | Off / On (rojo) |
| **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. | 100 | 0–100 |
| Medidor **RF Pwr** | Muestra la potencia directa en la salida del excitador. Se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). | — | 0–120 W / 0–600 W |
| Medidor **SWR** | Muestra la relación de onda estacionaria en el excitador. Se vuelve rojo por encima de 2.5. | — | 1.0–3.0 |

## Consejos

- Observe los medidores **RF Pwr** y **SWR** en cuanto active MOX. Si el SWR supera 2.5 (zona roja), libere el transmisor de inmediato e investigue su sistema de antena.
- Establezca **RF Power** en un valor bajo antes de usar MOX por primera vez en una banda nueva.
- MOX lleva la radio a transmisión a plena potencia en cualquier modo que esté activo. Si solo necesita verificar el SWR o ajustar un ATU, use **TUNE** en su lugar — transmite una portadora al nivel más bajo de **Tune Pwr**.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR está conectado a la radio. El applet TX Controls requiere una conexión de radio activa.
- **El transmisor se activa pero no se muestra potencia de RF** — Verifique que **RF Power** no esté en 0 y que el perfil de TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente de PTT (pedal, VOX, comando CAT) puede estar manteniendo la radio manualizada. Verifique el hardware PTT externo y cualquier cliente CAT conectado.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Hacer su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
