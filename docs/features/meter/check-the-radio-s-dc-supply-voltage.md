# Verificar el voltaje de alimentación CC del radio

El applet Meters muestra un indicador en vivo del voltaje de alimentación +13.8V obtenido directamente del radio. Úselo para confirmar que su fuente de alimentación entrega el voltaje adecuado antes o durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión activa con el radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para alternar la apertura del applet Meters.
3. Lea el indicador **+13.8V** bajo el encabezado de sección **Radio Hardware**.

## Qué hace cada control

| Etiqueta | Qué muestra | Rango válido | Rojo por encima de |
|----------|-------------|-------------|-------------------|
| +13.8V | Voltaje de alimentación CC desde la entrada de energía del radio | 10.0–16.0 V | 15 V |

La barra del indicador se llena en color cian dentro del rango de operación normal y se vuelve roja cuando la lectura supera los 15 V. La pantalla se actualiza en tiempo real con balística suavizada.

## Consejos

- Una fuente de alimentación en buen estado normalmente indica cerca de 13.8 V en condiciones de recepción y puede bajar ligeramente bajo carga pesada de TX. Una lectura consistentemente por debajo de 12 V o por encima de 15 V justifica revisar la fuente de alimentación.
- Las marcas de escala del indicador están en 10.5, 12, 13.8 y 15 V para una referencia visual rápida.

## Solución de problemas

- **El indicador +13.8V no muestra movimiento o marca 0** — El radio no está conectado o los datos del medidor aún no se han recibido. Verifique el estado de la conexión y vuelva a conectar mediante `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de Meters](overview.md)
- [Observar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Monitorear la velocidad del ventilador principal](monitor-the-main-cooling-fan-speed.md)
