# Recuperar una memoria del ATU

Use el botón MEM para activar la recuperación de memoria del ATU, lo que permite que el equipo aplique una solución de sintonía previamente almacenada para la frecuencia actual en lugar de ejecutar un ciclo de sintonía completo.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. MEM no está disponible sin una conexión activa al equipo.
- Debe existir una memoria ATU almacenada para la frecuencia actual. Si no hay ninguna disponible, ejecute primero un ciclo de sintonía ATU completo.
- El applet TX debe estar visible. Si no lo está, haga clic en el botón TX del panel lateral derecho para mostrarlo.
- MEM está desactivado cuando el TGXL se encuentra en modo OPERATE. Asegúrese de que el TGXL no esté en modo OPERATE antes de continuar.

## Pasos

1. Abra el applet TX haciendo clic en el botón TX del panel lateral derecho si aún no está visible.
2. Haga clic en MEM en la fila de botones TUNE / MOX / ATU / MEM.
3. Confirme que el indicador Mem se ilumina en verde. Esto confirma que el ATU está utilizando activamente una memoria almacenada para la frecuencia actual.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| MEM | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Cuando está activado, el equipo aplica una solución de sintonía almacenada para la frecuencia actual. | Desactivado |
| Mem | Indicador | Se ilumina en verde cuando el ATU está usando una memoria. Tenue cuando la recuperación de memoria está desactivada o no aplica ninguna memoria. | Tenue |
| Success | Indicador | Se ilumina en verde cuando el estado del ATU es Successful u OK. | Tenue |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. | Tenue |

## Consejos

- Si el indicador Mem no se ilumina después de hacer clic en MEM, no existe ninguna memoria ATU almacenada para la frecuencia actual. Haga clic en ATU para ejecutar un ciclo de sintonía completo y almacenar una nueva memoria, y luego haga clic en MEM nuevamente.
- Hacer clic en MEM por segunda vez desactiva la recuperación de memoria. El botón vuelve a su estado apagado y el indicador Mem se apaga.

## Solución de problemas

- **El botón MEM aparece en gris y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria del ATU está desactivada en este modo. Verifique la configuración de su TGXL.
- **El indicador Mem permanece tenue después de hacer clic en MEM** — No existe ninguna memoria ATU almacenada para la frecuencia actual. Ejecute primero un ciclo de sintonía ATU usando el botón ATU y luego reactive MEM.
- **El indicador Byp se ilumina en lugar de Mem** — El ATU ha retrocedido al modo bypass. Esto puede ocurrir si la memoria almacenada ya no es válida para las condiciones actuales de la antena. Ejecute un nuevo ciclo de sintonía.

## Temas relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de los controles TX](overview.md)
