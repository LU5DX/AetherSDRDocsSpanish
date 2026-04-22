# Leer el ROS Inmediatamente Después de un Ajuste Automático

Tras completarse un ajuste automático, AetherSDR muestra brevemente el valor final estabilizado de ROS directamente en el botón TUNE, lo que le proporciona una lectura inmediata de aprobado/rechazado sin necesidad de consultar el indicador de ROS.

## Antes de comenzar

- El applet Tuner debe estar visible. Si no lo está, haga clic en el botón de bandeja TUN en la barra lateral derecha. El botón de bandeja TUN solo aparece cuando se detecta un Tuner Genius XL.
- La radio debe estar conectada.

## Pasos

1. Haga clic en TUN en la barra lateral derecha para abrir el applet Tuner.
2. Haga clic en TUNE.
3. Observe el botón TUNE. Se vuelve rojo y muestra TUNING... mientras se ejecuta el barrido de ajuste automático.
4. Cuando el ajuste finaliza, el botón regresa a su apariencia normal y muestra brevemente `SWR x.xx`, donde `x.xx` es el valor final estabilizado de ROS reportado por el TGXL.
5. Lea el valor de ROS en la etiqueta del botón. La pantalla vuelve a mostrar TUNE tras 2.5 segundos.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango válido |
|---|---|---|---|
| TUNE | Botón | Inicia el ajuste automático. La etiqueta alterna: TUNE → TUNING... → SWR x.xx → TUNE. | — |
| SWR | Medidor | Muestra el ROS reportado por el TGXL en tiempo real de forma continua. | 1.0–3.0 (rojo por encima de 2.5) |

## Consejos

- El ROS posterior al ajuste que se muestra en el botón TUNE se captura después de un breve período de estabilización al finalizar el barrido. Esto garantiza que el valor refleje la posición final del relé del sintonizador, y no una lectura tomada durante el barrido.
- Si no alcanza a ver la pantalla durante los 2.5 segundos, el medidor de ROS muestra el ROS actual en tiempo real en todo momento.

## Solución de problemas

- **El botón TUNE vuelve a mostrar TUNE sin mostrar un valor de ROS** — El TGXL no devolvió una lectura de ROS válida. Verifique que el sintonizador esté en modo OPERATE (no en BYPASS ni en STANDBY) y que la antena esté conectada.
- **El medidor de ROS muestra un valor superior a 2.5 (rojo) después del ajuste** — El ajuste automático no encontró una adaptación aceptable en la frecuencia actual. Pruebe con una antena diferente o revise la línea de alimentación.

## Relacionados

- [Ejecutar un ajuste automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Descripción general del sintonizador](overview.md)
