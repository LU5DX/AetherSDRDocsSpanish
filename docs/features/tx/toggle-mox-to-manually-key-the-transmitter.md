# Activar MOX para accionar manualmente el transmisor

MOX permite accionar el transmisor sin usar el PTT del micrófono ni un pedal de pie. Úselo para mantener el equipo en transmisión durante pruebas, ajuste de audio o cualquier situación en la que necesite control manual de TX.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. MOX requiere una conexión activa con el equipo.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón TX tray en la barra lateral derecha.

## Pasos

1. En el applet TX Controls, localice la fila de cuatro botones: TUNE, MOX, ATU, MEM.
2. Haga clic en MOX.
3. El botón se pone rojo y el equipo acciona el transmisor.
4. Haga clic en MOX nuevamente para desaccionar. El botón vuelve a su apariencia predeterminada (azul) y el equipo regresa a recepción.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| MOX | Botón de alternancia | Activa y desactiva la transmisión manual. Rojo mientras TX está accionado; azul (apagado) mientras está en recepción. |
| RF Pwr | Medidor | Muestra la potencia directa a la salida del excitador. Escala: 0–120 W (sin amplificador); rojo por encima de 100 W. Modelo Aurora 500W: 0–600 W, rojo por encima de 500 W. |
| SWR | Medidor | Muestra la relación de onda estacionaria en el excitador. Escala: 1.0–3.0; rojo por encima de 2.5. |
| RF Power | Control deslizante | Establece el nivel de potencia RF de transmisión. Valor predeterminado: 100. Rango: 0–100. |

## Consejos

- Observe los medidores RF Pwr y SWR mientras MOX está activo para confirmar que el equipo está transmitiendo y que el sistema de antena se encuentra dentro de límites aceptables.
- MOX y TUNE son controles independientes. Si ya hay una portadora de ajuste en curso (TUNE muestra "TUNING..."), deténgala antes de usar MOX.

## Solución de problemas

- **El botón MOX no responde** — El applet TX Controls requiere una conexión activa con el equipo. Verifique que AetherSDR esté conectado al FLEX-8600 mediante `Settings > Connect to Radio...`.
- **El equipo transmite pero RF Pwr indica cero** — Verifique que el control deslizante RF Power no esté ajustado en 0.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
