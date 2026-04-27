# Monitorear la Velocidad del Ventilador Principal de Enfriamiento

Use el applet Meters para observar en tiempo real la velocidad del ventilador principal de enfriamiento del FLEX-8600. Esto le permite confirmar que el ventilador está en funcionamiento y detectar velocidades inusualmente altas que puedan indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet Meters requiere una conexión activa con el equipo.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para abrir o cerrar el applet Meters.
3. Lea el indicador **Main Fan** bajo el encabezado de sección **Radio Hardware**.

## Qué hace cada control

| Indicador | Qué muestra | Rango válido | Zona roja |
|---|---|---|---|
| **Main Fan** | Velocidad actual del ventilador de enfriamiento en rpm, leída desde el medidor MAINFAN del equipo | 0–3000 rpm | Por encima de 2500 rpm |

La barra del indicador es de color cian en el rango de operación normal y se torna roja por encima de 2500 rpm.

## Consejos

- El indicador **Main Fan** se actualiza a medida que el equipo reporta nuevos valores de medición. Puede haber un breve retraso tras abrir el applet por primera vez, mientras se resuelve el índice del medidor.
- El indicador utiliza animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas se mostrarán como un barrido suave en lugar de un salto instantáneo.

## Solución de problemas

- **El indicador Main Fan no muestra movimiento al abrir el applet** — El índice del medidor de ventilador se resuelve de forma diferida en la primera actualización. Espere unos segundos para que el equipo emita una lectura del medidor. Si el indicador permanece en cero, verifique que la conexión con el equipo esté activa mediante `Settings > Connect to Radio...`.

## Relacionados

- [Descripción general de Meters](overview.md)
- [Observar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación DC del equipo](check-the-radio-s-dc-supply-voltage.md)
