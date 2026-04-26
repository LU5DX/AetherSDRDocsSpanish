# Recuperar una memoria del ATU

La función de memoria del ATU permite que el radio recupere una solución de sintonía almacenada previamente para la frecuencia actual, omitiendo una re-sintonía completa. Úsela cuando regrese a una banda o frecuencia que haya sintonizado antes y desee que el sintonizador aplique la coincidencia almacenada de inmediato.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión de radio activa.
- El ATU interno debe haber completado previamente una sintonía exitosa en o cerca de la frecuencia objetivo, para que exista una memoria almacenada.
- El botón de bandeja TX debe estar habilitado para que el applet TX Controls sea visible en el Panel de Applets.

## Pasos

1. Abra el applet TX Controls. Haga clic en el botón de bandeja **TX** en la barra lateral derecha si el applet no está visible.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Verifique el indicador **Mem**. Se ilumina en verde cuando el ATU está utilizando activamente una memoria almacenada para la frecuencia actual.

Para desactivar la recuperación de memoria, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a estar apagado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| **MEM** | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. | Desactivado |
| **Mem** | Indicador | Se ilumina en verde cuando el ATU utiliza una memoria almacenada. Apagado cuando la recuperación de memoria está desactivada o no aplica ninguna memoria. | Apagado |
| **Success** | Indicador | Se ilumina en verde cuando el estado del ATU es Successful u OK. | Apagado |
| **Byp** | Indicador | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. | Apagado |

## Consejos

- Si **Mem** no se ilumina después de habilitar **MEM**, no existe ninguna memoria almacenada para la frecuencia actual. Ejecute primero el ATU con el botón **ATU** y luego habilite **MEM** la próxima vez que visite esa frecuencia.
- **MEM** y **ATU** están ambos deshabilitados cuando el TGXL está en modo OPERATE. Si alguno de los botones aparece en gris, verifique el modo de su TGXL.

## Solución de problemas

- **El botón MEM aparece en gris** — El TGXL está en modo OPERATE. La recuperación de memoria del ATU no está disponible en este modo. Cambie el TGXL fuera del modo OPERATE para volver a habilitar el control.
- **El indicador Mem permanece apagado después de habilitar MEM** — No existe ninguna memoria del ATU para la frecuencia actual. Ejecute una sintonía completa del ATU con **ATU** y luego active **MEM**.

## Temas relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)
