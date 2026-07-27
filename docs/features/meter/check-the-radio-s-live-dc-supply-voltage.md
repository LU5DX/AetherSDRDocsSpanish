# Verificar el Voltaje de Alimentación de CC en Vivo de la Radio

El applet de Medidores muestra el voltaje de alimentación reportado en vivo por la radio. Úselo para confirmar que su fuente de alimentación de CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Medidores requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **MTR** de la bandeja en la barra lateral derecha para abrir el applet de Medidores.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en vivo para mostrar el voltaje actual, por ejemplo, `+13.82V`.

## Qué hace cada control

| Indicador | Rango válido | Rojo por encima de | Comportamiento | Accesibilidad |
|-----------|-------------|-----------|----------|---------------|
| +13.8V | 10.0–16.0 V | 15 V | Muestra el voltaje de alimentación reportado por la radio. La etiqueta del indicador se actualiza dinámicamente para reflejar el valor en vivo (ej. `+13.82V`). | Nombre accesible: "Supply voltage" |
| PA Temp | 0–120 °C | 70 °C | Muestra la lectura del medidor PATEMP de la radio. La unidad de temperatura (°C o °F) se alterna con el botón junto al encabezado "Radio Hardware". | Nombre accesible: "PA temperature" |
| Main Fan | 0–3000 rpm | 2500 rpm | Muestra el valor del medidor MAINFAN de la radio. | Nombre accesible: "Main fan speed" |

## Controles de la fila de encabezado

La fila de encabezado **Radio Hardware** incluye un botón para alternar la unidad de temperatura.

| Control | Etiqueta | Comportamiento | Accesibilidad |
|---------|-------|----------|---------------|
| Botón de alternancia de unidad de temperatura | `°C` o `°F` | Haga clic para alternar la visualización de la temperatura del PA entre Celsius y Fahrenheit. La configuración se conserva y restaura en el próximo inicio. | Descripción accesible: "Toggles PA temperature display between Celsius and Fahrenheit" |

## Configuraciones persistentes

La preferencia de unidad de temperatura se almacena bajo la clave de configuración `MtrApplet`:
- `tempFahrenheit` — almacenado como `"True"` o `"False"` para indicar visualización en Fahrenheit o Celsius.

## Notas de accesibilidad

Cada indicador tiene un nombre accesible establecido para compatibilidad con lectores de pantalla:
- Indicador de temperatura del PA: "PA temperature"
- Indicador de voltaje de alimentación: "Supply voltage"
- Indicador del ventilador principal: "Main fan speed"
- Botón de alternancia de unidad de temperatura: La descripción accesible describe su función.

Estos nombres se anuncian cuando el indicador recibe el foco o se navega hacia él con tecnología de asistencia.

## Consejos

- La etiqueta del indicador cambia con cada actualización de telemetría de la radio, por lo que el valor mostrado en el centro de la barra siempre está actualizado; no es un marcador de posición estático.
- La barra se llena en color cian en el rango normal y se vuelve roja por encima de 15 V. Una barra roja indica un voltaje de alimentación que está por encima del rango de operación esperado.
- El indicador de temperatura del PA se vuelve rojo por encima de 70 °C. Si esto ocurre, reduzca la potencia de transmisión o el ciclo de trabajo.
- Haga clic en el botón de alternancia de unidad de temperatura (junto a "Radio Hardware") para cambiar entre Celsius y Fahrenheit. La configuración se recuerda entre sesiones.
- El indicador del ventilador principal se vuelve rojo por encima de 2500 rpm. Esto es normal durante la operación de alta potencia e indica que el ventilador de refrigeración está funcionando según lo esperado.

## Solución de problemas

- **El indicador no se mueve o muestra una etiqueta fija** — La radio no está conectada o el flujo de telemetría no ha comenzado. Confirme el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...`.

## Relacionados

- [Meters overview](overview.md)
- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
