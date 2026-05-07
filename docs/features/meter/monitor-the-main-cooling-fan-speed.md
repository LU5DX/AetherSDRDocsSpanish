# Supervisar la velocidad del ventilador principal de refrigeración

Utilice el applet Meters para observar en tiempo real la velocidad del ventilador principal de refrigeración de la FLEX-8600. Esto le ayuda a confirmar que el ventilador está funcionando y a detectar velocidades inusualmente altas que pueden indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para abrir el applet Meters.
3. Lea el indicador **Main Fan** bajo el encabezado de la sección **Radio Hardware**.

## Qué indica cada control

| Indicador    | Qué muestra                                                              | Rango válido |
|--------------|--------------------------------------------------------------------------|--------------|
| **PA Temp**  | Temperatura del PA en °C, leída del medidor PATEMP de la radio           | 0–120 °C     |
| **+13.8V**   | Voltaje de alimentación en voltios. La etiqueta del indicador se actualiza dinámicamente para mostrar el valor en vivo reportado por la radio (por ejemplo, **+13.82V**) en lugar del texto estático **+13.8V**. | 10.0–16.0 V  |
| **Main Fan** | Velocidad actual del ventilador de refrigeración en rpm, leída del medidor MAINFAN de la radio | 0–3000 rpm   |

Las barras de los indicadores son de color cian en el rango de operación normal. El indicador **PA Temp** se vuelve rojo por encima de 70 °C, el indicador **+13.8V** se vuelve rojo por encima de 15 V y el indicador **Main Fan** se vuelve rojo por encima de 2500 rpm.

## Consejos

- El indicador **Main Fan** se actualiza conforme la radio reporta nuevos valores de los medidores. Puede haber una breve demora después de abrir el applet mientras se resuelve el índice del medidor.
- El indicador utiliza una animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas aparecerán como un barrido suave en lugar de un salto instantáneo.
- La etiqueta del indicador **+13.8V** refleja el valor de voltaje en vivo reportado por la radio. La etiqueta se actualiza cada vez que la radio envía una nueva lectura del medidor, por lo que el voltaje mostrado (por ejemplo, **+13.82V**) siempre está actualizado.

## Solución de problemas

- **El indicador Main Fan no muestra movimiento después de abrir el applet** — El índice del medidor del ventilador se resuelve de forma diferida en la primera actualización. Espere unos segundos a que la radio emita una lectura del medidor. Si el indicador permanece en cero, verifique que la conexión con la radio esté activa mediante `Settings > Connect to Radio...`.

## Relacionados

- [Meters overview](overview.md)
- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Check the radio's DC supply voltage](check-the-radio-s-dc-supply-voltage.md)
