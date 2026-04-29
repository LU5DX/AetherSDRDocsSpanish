# Supervisar la velocidad del ventilador principal de refrigeración

Use el applet Meters para observar en tiempo real la velocidad del ventilador principal de refrigeración del FLEX-8600. Esto le permite confirmar que el ventilador está en funcionamiento y detectar velocidades inusualmente altas que podrían indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para alternar la apertura del applet Meters.
3. Lea el indicador **Main Fan** bajo el encabezado de sección **Radio Hardware**.

## Qué hace cada control

| Indicador | Qué muestra | Rango válido | Zona roja |
|---|---|---|---|
| **Main Fan** | Velocidad actual del ventilador de refrigeración en rpm, leída desde el medidor MAINFAN del radio | 0–3000 rpm | Por encima de 2500 rpm |

La barra del indicador es de color cian en el rango de operación normal y se vuelve roja por encima de 2500 rpm.

## Consejos

- El indicador **Main Fan** se actualiza a medida que el radio reporta nuevos valores de medición. Puede haber un breve retraso tras la primera apertura del applet mientras se resuelve el índice del medidor.
- El indicador utiliza animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas aparecerán como un movimiento continuo en lugar de un salto instantáneo.

## Solución de problemas

- **El indicador Main Fan no muestra movimiento tras abrir el applet** — El índice del medidor del ventilador se resuelve de forma diferida en la primera actualización. Espere unos segundos para que el radio emita una lectura del medidor. Si el indicador permanece en cero, verifique que la conexión de radio esté activa mediante `Settings > Connect to Radio...`.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Supervisar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación CC del radio](check-the-radio-s-dc-supply-voltage.md)
