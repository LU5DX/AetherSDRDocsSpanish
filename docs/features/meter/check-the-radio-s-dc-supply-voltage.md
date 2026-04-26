# Verificar la tensión de alimentación CC del equipo

El applet Meters muestra en tiempo real la tensión de alimentación CC del equipo. Úselo para confirmar que su fuente de alimentación entrega una tensión estable bajo carga.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet Meters requiere una conexión activa con el equipo.
- El panel de applets debe estar visible. Si no lo está, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón de bandeja **MTR** en la barra lateral derecha para abrir el applet Meters.
2. Lea el indicador **+13.8V** bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha. El indicador se vuelve rojo cuando la lectura supera los 15 V.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Rojo por encima de |
|---|---|---|---|
| +13.8V | Tensión de alimentación CC del equipo | 10.0–16.0 V | 15 V |

No existe ningún ajuste almacenado para este indicador. El valor se lee directamente desde el equipo.

## Consejos

- Observe el indicador **+13.8V** mientras transmite. Una caída de tensión significativa bajo carga de TX puede indicar una fuente de alimentación subdimensionada o en falla.
- El indicador utiliza una respuesta amortiguada, por lo que los transitorios rápidos pueden no ser visibles en su valor de pico instantáneo.

## Relacionado

- [Descripción general de Meters](overview.md)
- [Vigilar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Monitorear la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
