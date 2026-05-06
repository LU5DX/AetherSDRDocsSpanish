# Verificar el voltaje de alimentación CC del radio en tiempo real

El applet Meters muestra el voltaje de alimentación que reporta el radio en tiempo real. Úselo para confirmar que su fuente de alimentación CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión activa con el radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón de bandeja **MTR** en la barra lateral derecha para abrir el applet Meters.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en tiempo real para mostrar el voltaje actual — por ejemplo, `+13.82V`.

## Qué hace cada control

| Indicador | Rango válido | Rojo por encima de | Comportamiento |
|-----------|--------------|-------------------|----------------|
| +13.8V | 10.0–16.0 V | 15 V | Muestra el voltaje de alimentación reportado por el radio. La etiqueta del indicador se actualiza dinámicamente para reflejar el valor en tiempo real (p. ej., `+13.82V`). |

No existe una clave de configuración persistente para este indicador. No tiene valor predeterminado configurable.

## Consejos

- La etiqueta del indicador cambia en cada actualización de telemetría proveniente del radio, por lo que el valor mostrado en el centro de la barra es siempre el actual — no es un marcador estático.
- La barra se llena de color cian en el rango normal y se vuelve roja por encima de 15 V. Una barra roja indica un voltaje de alimentación que supera el rango de operación esperado.

## Solución de problemas

- **El indicador no muestra movimiento o la etiqueta permanece fija** — El radio no está conectado, o el flujo de telemetría no ha comenzado. Confirme el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de Meters](overview.md)
- [Monitorear la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Monitorear la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
