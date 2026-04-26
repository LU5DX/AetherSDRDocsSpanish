# Leer la ROS inmediatamente después de sintonizar

Después de hacer clic en TUNE, el applet Tuner captura la ROS final estabilizada del 4O3A Tuner Genius XL y la muestra brevemente en el botón TUNE para que pueda confirmar la concordancia sin mirar el medidor de ROS.

## Antes de comenzar

- AetherSDR debe haber detectado un Tuner Genius XL. El botón TUN en la bandeja del panel derecho aparece únicamente cuando el TGXL está presente.
- El applet Tuner debe estar abierto. Haga clic en el botón TUN de la bandeja para abrirlo si aún no está visible.
- El sintonizador debe estar en estado OPERATE (el botón OPERATE se muestra en verde). Consulte [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md).

## Pasos

1. Haga clic en TUNE. El botón se vuelve rojo y su etiqueta cambia a `TUNING...`.
2. Espere. Cuando el ciclo de sintonía automática finaliza, la etiqueta del botón cambia a `SWR x.xx`, donde `x.xx` es la ROS estabilizada reportada por el TGXL.
3. Lea el valor de ROS directamente en el botón TUNE. El valor se muestra durante 2.5 segundos y luego el botón regresa a `TUNE`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango válido |
|---------|------|----------------|--------------|
| TUNE | Botón | Inicia la sintonía automática. La etiqueta avanza: `TUNE` → `TUNING...` → `SWR x.xx` (parpadea durante 2.5 s) → `TUNE`. | — |
| SWR | Medidor | Muestra la ROS reportada por el TGXL en tiempo real durante toda la sesión. Rojo por encima de 2.5. | 1.0–3.0 |

## Consejos

- El valor `SWR x.xx` en el botón TUNE refleja la lectura estabilizada posterior a la sintonía, no una muestra tomada a mitad del barrido. AetherSDR espera 400 ms después de que termina el ciclo de sintonía antes de fijar el valor, dándole tiempo al TGXL para reportar su ROS final estabilizada por TCP.
- Si no alcanza a ver el destello de 2.5 segundos, el medidor de ROS muestra la ROS en vivo en todo momento.

## Solución de problemas

- **El botón TUNE regresa a `TUNE` sin mostrar un valor de ROS** — Es posible que el ciclo de sintonía se haya interrumpido antes de que llegara una lectura de ROS válida. Haga clic en TUNE nuevamente para ejecutar una nueva sintonía automática.
- **El botón TUN de la bandeja no es visible** — AetherSDR no ha detectado un Tuner Genius XL. Verifique la conexión del TGXL y que el firmware del equipo sea la versión 4.1.5.

## Relacionados

- [Ejecutar una sintonía automática en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
