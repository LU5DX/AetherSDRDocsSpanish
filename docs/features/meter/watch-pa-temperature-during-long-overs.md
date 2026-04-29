# Supervisar la temperatura del PA durante transmisiones largas

El applet Meters muestra un indicador en vivo de PA Temp que lee la temperatura del amplificador de potencia del radio en tiempo real. Mantenerlo visible durante transmisiones largas permite detectar acumulación térmica antes de que se convierta en un problema.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el botón de bandeja MTR en la barra lateral derecha del panel de applets.
2. Haga clic en MTR para abrir o cerrar el applet Meters.
3. Lea el indicador **PA Temp** bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha a medida que la temperatura sube. La barra se vuelve amarilla por encima de 55 °C y roja por encima de 70 °C.

## Qué hace cada control

| Etiqueta | Rango | Umbral rojo | Comportamiento |
|-------|-------|---------------|----------|
| PA Temp | 0–120 °C | > 70 °C | Muestra la temperatura del PA reportada por el radio. La barra es verde por debajo de 55 °C, amarilla de 55–70 °C, roja por encima de 70 °C. |
| +13.8V | 10.0–16.0 V | > 15 V | Muestra el voltaje de alimentación. |
| Main Fan | 0–3000 rpm | > 2500 rpm | Muestra la velocidad del ventilador principal de refrigeración. |

Ninguno de estos controles tiene claves de configuración persistente. Son pantallas de telemetría de solo lectura.

## Consejos

- El indicador utiliza balística suavizada, por lo que los picos breves son visibles sin causar parpadeo. Las lecturas sostenidas en zona roja indican una condición térmica real, no un pico transitorio.
- La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA se satura bajo la carga máxima del PA, por lo que se ha omitido intencionalmente.

## Solución de problemas

- **El indicador PA Temp no muestra movimiento** — El applet solo recibe datos cuando está conectado al radio. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...` si es necesario.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Verificar el voltaje de alimentación CC del radio](check-the-radio-s-dc-supply-voltage.md)
- [Monitorear la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
