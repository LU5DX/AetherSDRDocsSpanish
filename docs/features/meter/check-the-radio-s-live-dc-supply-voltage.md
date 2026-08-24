# Compruebe la Tensión de Alimentación de CC en Vivo de la Radio

El applet Meters muestra la tensión de alimentación reportada en vivo por la radio. Úselo para confirmar que su fuente de alimentación de CC se encuentra dentro de un rango saludable durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **MTR** de la bandeja en la barra lateral derecha para abrir el applet Meters.
2. Lea el indicador **+13.8V**. La etiqueta en el centro de la barra se actualiza en vivo para mostrar la tensión actual — por ejemplo, `+13.82V`.

## Función de cada control

| Indicador                | Rango válido                                                                                                                                     | Rojo por encima de                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| PA Temp                  | Muestra la lectura PATEMP de la radio; la etiqueta del indicador muestra el valor en vivo con la unidad seleccionada.                            | La escala y las marcas se vuelven a renderizar al usar el conmutador °C/°F, ajustándose al instante para evitar animaciones al cambiar de unidad. |
| Main Fan                 | Muestra el valor MAINFAN (resuelto de forma diferida por MeterModel::findMeter); la etiqueta muestra las rpm en vivo.                            | PACURRENT se omite intencionalmente: el rango de 10 A del medidor se recorta bajo el consumo máximo de PA en hardware FLEX-8000.        |
| Conmutador °C / °F       | Conmuta la visualización de la temperatura de la PA entre Celsius y Fahrenheit; la elección se guarda en el objeto de configuración 'MtrApplet' (campo tempFahrenheit). | Ubicado en la fila del encabezado junto a la etiqueta de la sección 'Radio Hardware'.                                        |
| +13.8V (tensión de alimentación) | Muestra el medidor de tensión de alimentación; la etiqueta se actualiza dinámicamente para mostrar el valor de tensión en vivo (p. ej. '+13.82V') mediante HGauge::setLabel. |                                                                                                                             |

## Controles de la fila del encabezado

La fila del encabezado **Radio Hardware** incluye un botón de conmutación de unidad de temperatura.

| Control | Etiqueta | Comportamiento | Accesibilidad |
|---------|----------|----------------|---------------|
| Botón de conmutación de unidad de temperatura | `°C` o `°F` | Haga clic para conmutar la visualización de la temperatura de la PA entre Celsius y Fahrenheit. El ajuste se guarda y se restaura en el próximo inicio. | Descripción accesible: "Conmuta la visualización de la temperatura de la PA entre Celsius y Fahrenheit" |

## Configuración persistente

La preferencia de unidad de temperatura se almacena bajo la clave de configuración `MtrApplet`:
- `tempFahrenheit` — se guarda como `"True"` o `"False"` para indicar la visualización en Fahrenheit o Celsius.

## Notas de accesibilidad

Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla:
- Indicador de PA Temp: "Temperatura de la PA"
- Indicador de tensión de alimentación: "Tensión de alimentación"
- Indicador de Main Fan: "Velocidad del ventilador principal"
- Botón de conmutación de unidad de temperatura: la descripción accesible describe su función.

Estos nombres se anuncian cuando el indicador recibe el foco o se navega hasta él con tecnología de asistencia.

## Consejos

- La etiqueta del indicador cambia con cada actualización de telemetría de la radio, por lo que el valor mostrado en el centro de la barra está siempre actualizado — no es un marcador de posición estático.
- La barra se rellena de cian en el rango normal y se vuelve roja por encima de 15 V. Una barra roja indica una tensión de alimentación por encima del rango operativo esperado.
- El indicador de temperatura de la PA se vuelve rojo por encima de 70 °C. Si esto ocurre, reduzca la potencia de transmisión o el ciclo de trabajo.
- Haga clic en el botón de conmutación de unidad de temperatura (junto a "Radio Hardware") para alternar entre Celsius y Fahrenheit. El ajuste se recuerda entre sesiones.
- El indicador de Main Fan se vuelve rojo por encima de 2500 rpm. Esto es normal durante operación de alta potencia e indica que el ventilador de refrigeración funciona según lo esperado.
- La etiqueta del indicador de PA Temp refleja la temperatura actual en la unidad seleccionada (p. ej., `45°C` o `113°F`), y la escala se vuelve a renderizar al instante al conmutar unidades.

## Solución de problemas

- **El indicador no muestra movimiento o tiene una etiqueta fija** — La radio no está conectada o el flujo de telemetría no ha comenzado. Confirme el estado de la conexión y vuelva a conectar mediante `Settings > Connect to Radio...`.
- **El indicador de PA Temp está en blanco o no se actualiza** — La radio no está reportando una lectura de PATEMP. Verifique que la radio esté conectada y que la telemetría de temperatura de la PA esté disponible en su hardware.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Vigile la temperatura de la PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Supervise la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
