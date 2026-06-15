# Vigile la temperatura del PA durante transmisiones largas

El applet Meters muestra un indicador de temperatura del PA en vivo que lee la temperatura del amplificador de potencia de la radio en tiempo real. Mantenerlo visible durante transmisiones largas le permite detectar acumulación térmica antes de que se convierta en un problema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el botón MTR en la barra lateral derecha del panel de applets.
2. Haga clic en MTR para abrir el applet Meters.
3. Lea el indicador **PA Temp** bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha a medida que la temperatura aumenta. La barra se vuelve amarilla por encima de 55 °C y roja por encima de 70 °C.

## Función de cada control

| Etiqueta | Rango       | Umbral rojo | Notas                                                                                                                                           |
|----------|-------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| PA Temp  | 0–120 °C    | > 70 °C     | Nombre accesible: "PA temperature".                                                                                                             |
| +13.8V   | 10.0–16.0 V | > 15 V      | La etiqueta del indicador se actualiza dinámicamente para mostrar el voltaje en vivo reportado por la radio (ej. `+13.82V`) en lugar del texto estático `+13.8V`. Nombre accesible: "Supply voltage". |
| Main Fan | 0–3000 rpm  | > 2500 rpm  | Nombre accesible: "Main fan speed".                                                                                                             |

Ninguno de estos controles tiene claves de configuración persistentes. Son visualizaciones de telemetría de solo lectura.

## Consejos

- El indicador usa balística suavizada, por lo que los picos breves son visibles sin causar parpadeo. Lecturas sostenidas en la zona roja indican una condición térmica real, no un pico transitorio.
- La etiqueta del indicador de voltaje de alimentación refleja el valor de voltaje en vivo reportado por la radio. La etiqueta se actualiza cada vez que llega una nueva lectura, por lo que siempre muestra el voltaje actual con dos decimales (por ejemplo, `+13.82V`).
- La corriente del PA no se muestra. En hardware de la serie FLEX-8000, el medidor de corriente del PA satura con la potencia total del PA, por lo que se ha omitido intencionalmente.
- Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "PA temperature", "Supply voltage" y "Main fan speed".

## Solución de problemas

- **El indicador PA Temp no muestra movimiento** — El applet solo recibe datos cuando está conectado a la radio. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...` si es necesario.

## Relacionados

- [Meters overview](overview.md)
- [Check the radio's DC supply voltage](check-the-radio-s-dc-supply-voltage.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
