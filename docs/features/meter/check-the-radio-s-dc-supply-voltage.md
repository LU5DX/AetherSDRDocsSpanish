# Compruebe la Tensión de Alimentación CC de la Radio

El applet Meters muestra un indicador en vivo de la tensión de alimentación obtenida directamente de la radio. Úselo para confirmar que su fuente de alimentación está suministrando la tensión adecuada antes o durante la operación. A partir de la v0.9.7, la etiqueta del indicador se actualiza dinámicamente para mostrar la tensión exacta reportada por la radio (por ejemplo, **+13.82V**) en lugar del marcador estático **+13.8V**.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívalo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón **MTR** en la barra lateral derecha del panel del applet.
2. Haga clic en **MTR** para abrir el applet Meters.
3. Lea el indicador de tensión de alimentación bajo el encabezado de sección **Radio Hardware**. La etiqueta del indicador muestra el valor de tensión en vivo, por ejemplo **+13.82V**.

## Qué hace cada control

| Etiqueta | Qué muestra | Rango válido |
|----------|-------------|--------------|
| +13.8V | Muestra la tensión de alimentación reportada por la radio. En v0.9.7 y posteriores, la etiqueta del indicador se actualiza en tiempo real para reflejar el valor de tensión en vivo (por ejemplo, **+13.82V**) en lugar del marcador estático **+13.8V**. | 10.0–16.0 V (rojo por encima de 15 V) |
| PA Temp | Muestra la temperatura del amplificador de potencia reportada por la radio. | 0–120 °C (rojo por encima de 70 °C) |
| Main Fan | Muestra la velocidad del ventilador de refrigeración principal reportada por la radio. | 0–3000 rpm (rojo por encima de 2500 rpm) |

La barra del indicador se llena de color cian en el rango de funcionamiento normal y se vuelve roja cuando la lectura supera los 15 V. La visualización se actualiza en tiempo real con balística suavizada.

## Consejos

- Una fuente de alimentación saludable suele leer cerca de 13.8 V en condiciones de recepción y puede caer ligeramente bajo una carga pesada de TX. Una lectura constantemente por debajo de 12 V o por encima de 15 V requiere atención a su fuente de alimentación.
- Las marcas de la escala del indicador están en 10.5, 12, 13.8 y 15 V para una referencia visual rápida.

## Solución de problemas

- **La etiqueta del indicador muestra +13.8V y no se actualiza** — Esto indica que puede estar ejecutando una versión anterior a la v0.9.7. Verifique su versión de AetherSDR y actualice si es necesario.
- **El indicador de tensión de alimentación no muestra movimiento o lee 0** — La radio no está conectada o los datos del medidor aún no se han recibido. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...`.

## Relacionados

- [Meters overview](overview.md)
- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
