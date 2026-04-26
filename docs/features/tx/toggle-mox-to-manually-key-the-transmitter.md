# Activar MOX para transmitir manualmente

MOX permite activar el transmisor de forma manual, sin pedal ni línea PTT. Úselo cuando necesite portadora continua para pruebas, llamadas en red o cualquier situación en la que desee control directo por software del TX.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. MOX requiere una conexión de radio activa.
- Abra el applet TX Controls. Haga clic en el botón TX del área de notificación en la barra lateral derecha, o confirme que el applet ya es visible en el Applet Panel.

## Pasos

1. En el applet TX Controls, ubique la fila que contiene TUNE, MOX, ATU y MEM.
2. Haga clic en MOX para activar el transmisor. El botón se pone rojo para confirmar que el TX está activo.
3. Haga clic en MOX de nuevo para volver a recepción. El botón regresa a su estado predeterminado (azul apagado).

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| MOX | Botón de alternancia | Alterna la transmisión manual. Rojo cuando el TX está activo; azul (apagado) cuando está en recepción. |
| RF Pwr | Medidor | Muestra la potencia directa en la salida del excitador. Escala: 0–120 W (sin amplificador); rojo por encima de 100 W. |
| SWR | Medidor | Muestra la relación de onda estacionaria. Rojo por encima de 2.5. |

## Consejos

- Observe los medidores RF Pwr y SWR mientras MOX esté activo para confirmar la potencia esperada y un SWR seguro.
- MOX activa el transmisor independientemente del modo. Asegúrese de que el micrófono, el manipulador o la fuente de audio estén configurados antes de activar MOX en una frecuencia en uso.
- Para transmitir una portadora limpia en verificaciones de SWR, use TUNE con el control deslizante Tune Pwr en lugar de MOX. Consulte [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md).

## Resolución de problemas

- **El botón MOX no responde** — Es posible que la conexión de radio esté inactiva. Verifique el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...`.
- **MOX se activa pero RF Pwr indica cero** — Es posible que el control deslizante RF Power esté en 0. Auméntelo antes de activar la transmisión.
- **MOX permanece en rojo después de hacer clic** — Una actualización del protocolo SmartSDR proveniente de la radio puede estar manteniendo el estado de TX. Haga clic en MOX una vez más para desactivarlo; si el botón permanece en rojo, verifique si hay una fuente de PTT bloqueada en la radio.

## Temas relacionados

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
