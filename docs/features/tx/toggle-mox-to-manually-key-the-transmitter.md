# Activar MOX para teclear el transmisor manualmente

MOX permite teclear el transmisor sin pedal ni línea PTT. Úselo para verificar el audio, probar su señal o transmitir cuando el PTT de hardware no esté disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está desconectada.
- Confirme que su perfil TX y el nivel de RF Power estén configurados correctamente antes de teclear.

## Pasos

1. Si el applet TX Controls no está visible, haga clic en el botón **TX** de la bandeja en la barra lateral derecha para mostrarlo.
2. Ubique el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para teclear el transmisor. El botón se pone rojo mientras TX está activo.
4. Haga clic en **MOX** nuevamente para dejar de teclear. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango |
|---------|----------------|----------------|-------|
| **MOX** | Activa o desactiva la transmisión manual. El botón se pone rojo mientras el transmisor está tecleado. | Off | Off / On (rojo) |
| **RF Power** | Establece el nivel de potencia RF de transmisión enviado a la radio. | 100 | 0–100 |
| Medidor **RF Pwr** | Muestra la potencia directa en la salida del excitador. Se pone rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). | — | 0–120 W / 0–600 W |
| Medidor **SWR** | Muestra la relación de onda estacionaria en el excitador. Se pone rojo por encima de 2.5. | — | 1.0–3.0 |

## Consejos

- Observe los medidores **RF Pwr** y **SWR** en cuanto active MOX. Si el SWR supera 2.5 (zona roja), deje de teclear de inmediato e investigue su sistema de antena.
- Establezca **RF Power** en un valor bajo antes de usar MOX por primera vez en una banda nueva.
- MOX teclea la radio a plena potencia en el modo que esté activo. Si solo necesita verificar el SWR o ajustar un ATU, use **TUNE** en su lugar: transmite una portadora al nivel inferior de **Tune Pwr**.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR está conectado a la radio. El applet TX Controls requiere una conexión de radio activa.
- **El transmisor se teclea pero no se muestra potencia RF** — Verifique que **RF Power** no esté en 0 y que el perfil TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente PTT (pedal, VOX, comando CAT) puede estar manteniendo la radio tecleada. Revise el hardware PTT externo y cualquier cliente CAT conectado.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
