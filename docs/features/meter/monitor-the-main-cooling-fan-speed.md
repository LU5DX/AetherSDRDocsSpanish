# Monitorear la velocidad del ventilador de refrigeración principal

El applet Meters muestra un indicador en tiempo real de la velocidad del ventilador de refrigeración principal del radio Flex. Úselo para confirmar que el ventilador está girando y para detectar velocidades anormalmente altas que puedan indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Meters requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si está oculto, haga clic en el botón MTR de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón MTR de la barra lateral derecha. El applet Meters se abre.
2. Observe el indicador "Main Fan" bajo el encabezado "Radio Hardware". La barra muestra la velocidad actual del ventilador en rpm.

## Qué hace cada control

| Etiqueta | Rango | Zona roja | Notas |
|---|---|---|---|
| Main Fan | 0–3000 rpm | por encima de 2500 rpm | La barra se vuelve roja cuando la velocidad del ventilador supera las 2500 rpm. Sin ajuste persistente. |

El indicador se llena de izquierda a derecha. La barra es verde por debajo de 2500 rpm y se vuelve roja por encima de 2500 rpm. Las etiquetas de escala a lo largo de la parte superior muestran 0, 500, 1k, 1.5k, 2k y 3k.

## Consejos

- La velocidad del ventilador se lee desde el medidor MAINFAN del radio. El valor se actualiza en tiempo real a medida que el radio reporta nuevas lecturas; no existe actualización manual.
- Una lectura en 0 rpm o cercana a 0 rpm mientras el radio está encendido y transmitiendo requiere atención. Verifique las conexiones físicas y la ventilación del radio.
- Compare la velocidad del ventilador con el indicador PA Temp en el mismo applet. Una temperatura en aumento junto con una velocidad alta del ventilador es normal durante transmisiones prolongadas; una temperatura alta con una velocidad baja del ventilador no lo es.

## Solución de problemas

- **El indicador Main Fan no muestra movimiento o permanece en 0** — El índice del medidor se resuelve de forma diferida después de la conexión. Espere unos segundos para que el radio reporte su primera lectura MAINFAN. Si el indicador permanece en 0 mientras el radio está encendido y caliente, verifique que la conexión del radio esté activa en `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de Meters](overview.md)
- [Monitorear la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación de CC del radio](check-the-radio-s-dc-supply-voltage.md)
