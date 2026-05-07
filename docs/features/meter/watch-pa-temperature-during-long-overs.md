# Supervise la temperatura del PA durante sobretransmisiones largas

El applet Meters muestra un indicador en vivo de la temperatura del PA (PA Temp) que lee en tiempo real la temperatura del amplificador de potencia de la radio. Mantenerlo visible durante sobretransmisiones largas le permite detectar la acumulación térmica antes de que se convierta en un problema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el botón MTR en la barra lateral derecha del panel del applet.
2. Haga clic en MTR para abrir el applet Meters.
3. Lea el indicador **PA Temp** bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha a medida que la temperatura aumenta. La barra se vuelve amarilla por encima de 55 °C y roja por encima de 70 °C.

## Función de cada control

| Etiqueta | Rango       | Umbral rojo | Notas                                                                                                     |
|----------|-------------|-------------|-----------------------------------------------------------------------------------------------------------|
| PA Temp  | 0–120 °C    | > 70 °C     |                                                                                                           |
| +13.8V   | 10.0–16.0 V | > 15 V      | La etiqueta del indicador se actualiza dinámicamente para mostrar el voltaje en vivo reportado por la radio (ej. `+13.82V`) en lugar del texto estático `+13.8V`. |
| Main Fan | 0–3000 rpm  | > 2500 rpm  |                                                                                                           |

Ninguno de estos controles tiene claves de configuración persistidas. Son visualizaciones de telemetría de solo lectura.

## Consejos

- El indicador utiliza balística suavizada, por lo que los picos breves son visibles sin causar parpadeo. Las lecturas sostenidas en la zona roja indican una condición térmica real, no un pico transitorio.
- La etiqueta del indicador de voltaje de alimentación refleja el valor de voltaje en vivo reportado por la radio. La etiqueta se actualiza cada vez que llega una nueva lectura, por lo que siempre muestra el voltaje actual con dos decimales (por ejemplo, `+13.82V`).
- La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA se satura bajo demanda completa del PA, por lo que se ha omitido intencionalmente.

## Solución de problemas

- **El indicador PA Temp no muestra movimiento** — El applet solo recibe datos cuando está conectado a la radio. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...` si es necesario.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Verifique el voltaje de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
- [Supervise la velocidad del ventilador de enfriamiento principal](monitor-the-main-cooling-fan-speed.md)
