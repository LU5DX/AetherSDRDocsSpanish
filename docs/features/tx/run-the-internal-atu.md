# Ejecutar el ATU interno

Use los controles del applet TX Controls para ejecutar el sintonizador automático de antena interno del radio Flex y verificar el resultado. Esto reduce la ROE y optimiza la adaptación entre la radio y la antena en la frecuencia actual.

## Antes de comenzar

- Conéctese a una radio Flex. El applet TX Controls requiere una conexión de radio activa.
- Asegúrese de que el applet TX Controls sea visible. Si no lo es, haga clic en el botón TX tray en la barra lateral derecha.
- Verifique que no esté operando con un TGXL en modo OPERATE — ATU y MEM están deshabilitados en ese estado.

## Pasos

1. En el applet TX Controls, ajuste el control deslizante `Tune Pwr` al nivel de potencia que desea que el ATU utilice durante el ciclo de sintonización (predeterminado: 10, rango: 0–100).
2. Haga clic en ATU.
3. Observe los indicadores de estado del ATU — `Success`, `Byp` y `Mem` — para confirmar el resultado:
   - `Success` se ilumina en verde cuando el sintonizador encuentra una adaptación aceptable.
   - `Byp` se ilumina en naranja si el ATU está en bypass o bypass manual.
   - `Mem` se ilumina en verde si el sintonizador aplicó una memoria almacenada en lugar de ejecutar un ciclo de sintonización completo.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ATU | Botón momentáneo | — | — | Inicia el ciclo de sintonización del ATU interno. Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM | Botón de alternancia | — | — | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Tune Pwr | Control deslizante | 10 | 0–100 | Establece el nivel de potencia de la portadora utilizada durante la sintonización. |
| Success | Indicador | apagado | apagado / verde | Se ilumina en verde cuando el estado del ATU es Successful u OK. |
| Byp | Indicador | apagado | apagado / naranja | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. |
| Mem | Indicador | apagado | apagado / verde | Se ilumina en verde cuando el ATU está usando una memoria almacenada. |

## Consejos

- Baje el control deslizante `Tune Pwr` antes de hacer clic en ATU si desea sintonizar con potencia reducida, por ejemplo al usar una antena QRP o para proteger un amplificador lineal.
- Si `Byp` se ilumina al completarse el ciclo, el ATU no pudo encontrar una adaptación y se ha puesto en bypass. Verifique su sistema de antena y la ROE con el medidor `SWR` antes de transmitir.
- Use MEM para permitir que la radio recupere una configuración de ATU previamente almacenada cuando regrese a una frecuencia que ya haya sintonizado, evitando así un ciclo de sintonización completo.

## Solución de problemas

- **El botón ATU no hace nada** — Verifique que no esté ejecutando un TGXL en modo OPERATE. El botón ATU está deshabilitado en esa configuración.
- **`Byp` se ilumina en lugar de `Success`** — El sintonizador no pudo encontrar una adaptación aceptable. Verifique las conexiones de su línea de alimentación y antena, luego intente nuevamente. Consulte [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md) para inspeccionar la ROE antes de reintentar.
- **`Mem` se ilumina pero la ROE es alta** — La memoria recuperada puede estar desactualizada (la antena o la línea de alimentación han cambiado). Haga clic en ATU nuevamente para forzar un ciclo de sintonización nuevo.

## Relacionado

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de la portadora de sintonización](set-tune-carrier-power.md)
- [Descripción general de TX Controls](overview.md)
