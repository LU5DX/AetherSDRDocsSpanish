# Monitorizar la velocidad del ventilador principal

Utilice el applet Meters para observar en tiempo real la velocidad del ventilador principal de la FLEX-8600. Esto le ayuda a confirmar que el ventilador está funcionando y detectar velocidades inusualmente altas que pueden indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón **MTR** en la barra lateral derecha del panel del applet.
2. Haga clic en **MTR** para abrir el applet Meters.
3. Lea el indicador **Main Fan** bajo el encabezado de sección **Radio Hardware**.

## Qué hace cada control

| Indicador    | Qué muestra                                                                                                                               | Rango válido |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| **PA Temp**  | Temperatura del PA en °C, leída del medidor PATEMP de la radio. El indicador tiene un nombre accesible de "PA temperature" para compatibilidad con lectores de pantalla. | 0–120 °C     |
| **+13.8V**   | Tensión de alimentación en voltios. La etiqueta del indicador se actualiza dinámicamente para mostrar el valor en vivo informado por la radio (por ejemplo, **+13.82V**) en lugar del texto estático **+13.8V**. El indicador tiene un nombre accesible de "Supply voltage" para lectores de pantalla. | 10.0–16.0 V  |
| **Main Fan** | Velocidad actual del ventilador de refrigeración en rpm, leída del medidor MAINFAN de la radio. El indicador tiene un nombre accesible de "Main fan speed" para lectores de pantalla. | 0–3000 rpm   |

Las barras de los indicadores son cian en el rango de funcionamiento normal. El indicador **PA Temp** se vuelve rojo por encima de 70 °C, el indicador **+13.8V** se vuelve rojo por encima de 15 V y el indicador **Main Fan** se vuelve rojo por encima de 2500 rpm.

## Consejos

- El indicador **Main Fan** se actualiza a medida que la radio reporta nuevos valores del medidor. Puede haber un breve retraso después de abrir el applet mientras se resuelve el índice del medidor.
- El indicador utiliza una animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas aparecerán como un barrido suave en lugar de un salto instantáneo.
- La etiqueta del indicador **+13.8V** refleja el valor de tensión en vivo informado por la radio. La etiqueta se actualiza cada vez que la radio envía una nueva lectura del medidor, por lo que la tensión mostrada (por ejemplo, **+13.82V**) siempre está actualizada.

## Accesibilidad

- Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla:
  - **PA Temp** — "PA temperature"
  - **+13.8V** — "Supply voltage"
  - **Main Fan** — "Main fan speed"

## Solución de problemas

- **El indicador Main Fan no muestra movimiento después de abrir el applet** — El índice del medidor del ventilador se resuelve diferido en la primera actualización. Espere unos segundos a que la radio emita una lectura del medidor. Si el indicador permanece en cero, verifique que la conexión a la radio esté activa mediante `Settings > Connect to Radio...`.
- **El applet Meters no se muestra correctamente con ciertos temas** — El applet ahora aplica el estilo del tema mediante la configuración del contenedor `applet/meter`. Si experimenta problemas visuales, asegúrese de utilizar un tema compatible en `Settings > Appearance`.

## Relacionados

- [Resumen de Meters](overview.md)
- [Supervisar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar la tensión de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
