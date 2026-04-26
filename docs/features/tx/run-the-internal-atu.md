# Ejecutar el ATU interno

Use esta página para iniciar un ciclo del sintonizador automático de antena (ATU) en el FLEX-8600. El ATU encuentra una red de adaptación que minimiza la ROE en la frecuencia actual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls solo está activo cuando hay una conexión de radio presente.
- El radio no debe estar en modo TGXL OPERATE. El ATU está deshabilitado en ese modo.
- Ajuste la potencia de sintonía a un nivel apropiado antes de comenzar. Consulte [Establecer la potencia del portador de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón TX del panel lateral derecho para abrir TX Controls si no está visible todavía.
2. Ajuste el control deslizante `Tune Pwr` a la potencia de portador deseada (predeterminado: 10, rango: 0–100).
3. Haga clic en `ATU`.

El radio transmite un portador y ejecuta el ciclo de sintonía. Observe los indicadores `Success`, `Byp` y `Mem` debajo del selector TX Profile para seguir el resultado.

## Qué hace cada control

| Control | Tipo | Descripción | Predeterminado | Rango |
|---|---|---|---|---|
| ATU | Botón momentáneo | Inicia el ciclo de sintonía del ATU interno. Deshabilitado en modo TGXL OPERATE. | — | — |
| Tune Pwr | Control deslizante | Establece la potencia del portador utilizada durante la sintonía. | 10 | 0–100 |
| Success | Indicador | Se ilumina en verde cuando el resultado de la sintonía del ATU es exitoso. | Apagado | Apagado / verde |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en bypass o bypass manual. | Apagado | Apagado / naranja |
| Mem | Indicador | Se ilumina en verde cuando el ATU utiliza una memoria almacenada. | Apagado | Apagado / verde |
| MEM | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado en modo TGXL OPERATE. | — | On / Off |

## Consejos

- Si `Byp` se ilumina tras el ciclo, el ATU no pudo encontrar una adaptación y se ha puesto en bypass. Revise el sistema de antena o pruebe con una frecuencia diferente.
- Si `Mem` se ilumina inmediatamente después de hacer clic en ATU, el radio aplicó una memoria almacenada en lugar de ejecutar un ciclo de sintonía completo. Consulte [Recuperar una memoria del ATU](recall-an-atu-memory.md) para más detalles sobre la gestión de memorias.
- Mantenga la potencia de sintonía lo suficientemente baja para cumplir con las condiciones de su licencia y los requisitos del amplificador. El valor predeterminado del control deslizante `Tune Pwr` es 10.

## Solución de problemas

- **El botón ATU aparece desactivado** — El radio está en modo TGXL OPERATE. El ATU no puede iniciarse en este modo. Primero cambie el TGXL fuera del modo OPERATE.
- **El indicador Success no se ilumina tras la sintonía** — El ATU no pudo encontrar una adaptación aceptable. Revise la conexión de antena y la ROE en el indicador `SWR`. Intente reducir la desviación de frecuencia respecto al punto de resonancia de la antena.
- **Byp se ilumina en lugar de Success** — El ATU se ha puesto en bypass. Es posible que el sistema de antena esté fuera del rango de adaptación del sintonizador.

## Temas relacionados

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Establecer la potencia del portador de sintonía](set-tune-carrier-power.md)
- [Iniciar un portador de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
