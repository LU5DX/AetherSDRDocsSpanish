# Vigile la temperatura del PA durante transmisiones largas

El applet Meters muestra un indicador en vivo de PA Temp que lee la temperatura del amplificador de potencia de la radio en tiempo real. Mantenerlo visible durante transmisiones largas le permite detectar la acumulación de calor antes de que se convierta en un problema.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, use `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el botón MTR en la barra lateral derecha del panel de applets.
2. Haga clic en MTR para alternar la apertura del applet Meters.
3. Lea el indicador **PA Temp** bajo el encabezado de sección **Radio Hardware**.

La barra se llena de izquierda a derecha a medida que la temperatura sube. La barra se vuelve roja por encima de 70 °C (158 °F). Puede alternar la visualización de temperatura entre Celsius (°C) y Fahrenheit (°F) usando el botón de unidades en la fila del encabezado.

## Qué hace cada control

| Etiqueta                | Rango                                                                                                                                             | Comportamiento / Notas                                                                                                                                                                         |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PA Temp                 | 0–120 °C o 32–248 °F (rojo > 70 °C / 158 °F)                                                                                                      | Muestra la lectura del medidor PATEMP de la radio; la etiqueta del indicador muestra el valor en vivo con la unidad seleccionada. La escala y las marcas se vuelven a renderizar al usar la alternancia °C/°F, ajustándose de inmediato para evitar animaciones a través del salto de unidades. |
| Alternancia °C / °F     | °C / °F                                                                                                                                           | Alterna la visualización de temperatura del PA entre Celsius y Fahrenheit; la elección se guarda en el objeto de configuración `MtrApplet` (campo `tempFahrenheit`). Se encuentra en la fila del encabezado junto a la etiqueta de sección **Radio Hardware**. |
| +13.8V (tensión de alimentación) | 10.0–16.0 V (rojo > 15)                                                                                                                            | Muestra el medidor de tensión de alimentación; la etiqueta se actualiza dinámicamente para mostrar el valor de tensión en vivo (p. ej. `+13.82V`) mediante `HGauge::setLabel`.              |
| Main Fan                | 0–3000 rpm (rojo > 2500)                                                                                                                            | Muestra el valor del medidor MAINFAN (resuelto de forma diferida por `MeterModel::findMeter`); la etiqueta muestra las rpm en vivo. PACURRENT se omite intencionalmente: el rango del medidor de 10 A se satura con la demanda total del PA en hardware FLEX-8000. |

Ninguno de estos controles tiene claves de configuración persistentes (excepto la alternancia °C/°F). Son pantallas de telemetría de solo lectura.

## Alternancia de unidad de temperatura

Un botón **°C/°F** aparece en la fila del encabezado **Radio Hardware**. Haga clic en él para alternar el indicador PA Temp entre Celsius y Fahrenheit. La configuración persiste entre sesiones.

- Al alternar a Fahrenheit, las marcas del indicador, la etiqueta y el valor mostrado se actualizan para mostrar °F.
- El nombre accesible y la fuente de datos subyacente permanecen sin cambios; solo se convierte la presentación.
- La escala del indicador se vuelve a renderizar de inmediato al alternar, sin animaciones a través del cambio de unidades.

## Consejos

- El indicador usa balística suavizada, por lo que los picos breves son visibles sin causar parpadeo. Lecturas sostenidas en la zona roja indican una condición térmica real, no un pico transitorio.
- La etiqueta del indicador de tensión de alimentación refleja el valor de tensión en vivo reportado por la radio. La etiqueta se actualiza cada vez que llega una nueva lectura, por lo que siempre muestra la tensión actual con dos decimales (por ejemplo, `+13.82V`).
- La corriente del PA no se muestra. En hardware de la serie FLEX-8000, el medidor de corriente del PA se satura con la demanda total del PA, por lo que se ha omitido intencionalmente.
- Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "PA temperature", "Supply voltage" y "Main fan speed".
- La configuración de unidad de temperatura se almacena en la configuración de la aplicación bajo la clave `MtrApplet.tempFahrenheit`.

## Solución de problemas

- **El indicador PA Temp no muestra movimiento** — El applet solo recibe datos cuando está conectado a la radio. Verifique el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...` si es necesario.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Compruebe la tensión de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
- [Supervise la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
