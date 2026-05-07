# Verifique la Tensión de Alimentación en Vivo de la Radio

El applet Meters muestra la tensión de alimentación reportada en vivo por la radio. Úselo para confirmar que su fuente de alimentación de CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **MTR** de la bandeja en la barra lateral derecha para abrir el applet Meters.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en vivo para mostrar la tensión actual; por ejemplo, `+13.82V`.

## Función de cada control

| Indicador | Rango válido | Rojo por encima de | Comportamiento |
|-----------|--------------|--------------------|----------------|
| +13.8V | 10.0–16.0 V | 15 V | Muestra la tensión de alimentación reportada por la radio. La etiqueta del indicador se actualiza dinámicamente para reflejar el valor en vivo (p. ej., `+13.82V`). |

No existe una clave de configuración persistente para este indicador. No tiene un valor predeterminado configurable.

## Consejos

- La etiqueta del indicador cambia con cada actualización de telemetría de la radio, por lo que el valor mostrado en el centro de la barra siempre es actual; no es un marcador de posición estático.
- La barra se llena en cian dentro del rango normal y se vuelve roja por encima de 15 V. Una barra roja indica una tensión de alimentación que supera el rango de operación esperado.

## Solución de problemas

- **El indicador no se mueve o muestra una etiqueta fija** — La radio no está conectada o el flujo de telemetría no ha comenzado. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...`.

## Relacionados

- [Resumen de Meters](overview.md)
- [Vigile la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Supervise la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
