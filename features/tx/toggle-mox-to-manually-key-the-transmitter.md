# Activar MOX para teclear manualmente el transmisor

MOX le permite teclear el transmisor sin una entrada PTT ni actividad de micrófono. Úselo cuando necesite mantener el radio en transmisión — por ejemplo, para verificar la ROE, probar el audio o enviar una portadora manual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. MOX no tiene efecto cuando el radio está desconectado.
- Confirme que el nivel de potencia de RF está configurado de manera apropiada antes de teclear. Consulte [Configurar la potencia de salida de RF](set-rf-output-power.md).

## Pasos

1. Si el applet TX Controls no está visible, haga clic en el botón TX del área de bandeja en la barra lateral derecha para abrirlo.
2. Haga clic en MOX.
   - El botón se pone rojo y el radio teclea inmediatamente.
3. Haga clic en MOX nuevamente para dejar de teclear.
   - El botón vuelve a su estado predeterminado (azul) y el radio regresa a recepción.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango |
|---|---|---|---|---|
| MOX | Botón de alternancia | Teclea o deja de teclear el transmisor manualmente. Rojo mientras la transmisión está activa. | Apagado (azul) | Apagado / Encendido (rojo) |
| RF Pwr | Medidor | Muestra la potencia directa en la salida del excitador durante la transmisión. | — | 0–120 W; rojo por encima de 100 W (sin amplificador) / 0–600 W; rojo por encima de 500 W (Aurora 500W) |
| SWR | Medidor | Muestra la relación de onda estacionaria en el excitador durante la transmisión. | — | 1.0–3.0; rojo por encima de 2.5 |

## Consejos

- Observe los medidores RF Pwr y SWR mientras MOX está activo. Si la ROE indica rojo (por encima de 2.5), deje de teclear y revise el sistema de antena antes de continuar.
- MOX y TUNE son controles independientes. TUNE envía una portadora constante al nivel de Tune Pwr; MOX teclea el radio al nivel de RF Power usando su modo activo y audio.

## Solución de problemas

- **El botón MOX está visible pero el radio no teclea** — Confirme que AetherSDR está conectado al radio. El applet requiere una conexión de radio activa.
- **El radio permanece tecleado después de hacer clic en MOX por segunda vez** — Es posible que el estado del botón haya perdido sincronía con el radio. Haga clic en MOX una vez más para forzar la alternancia, o reinicie la conexión.

## Relacionados

- [Iniciar una portadora de ajuste para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Descripción general de TX Controls](overview.md)
