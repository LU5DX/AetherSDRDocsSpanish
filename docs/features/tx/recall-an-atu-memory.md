# Recuperar una memoria del ATU

Use la recuperación de memoria del ATU para aplicar una solución de sintonización previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- El ATU interno del radio debe tener almacenada al menos una memoria de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, recuperar una no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet TX Controls. Si no está visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** en verde confirma que el ATU está utilizando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a apagarse.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| MEM | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Cuando está activo, el radio aplica una solución de sintonización almacenada en lugar de ejecutar un nuevo ciclo de sintonización. Deshabilitado cuando el TGXL está en modo OPERATE. | Off |
| Mem | Indicador | Se ilumina en verde cuando el ATU está usando una memoria. Apagado cuando la recuperación de memoria está desactivada o no hay ninguna memoria en uso. | Apagado |
| Success | Indicador | Se ilumina en verde cuando el estado del ATU es Successful u OK. | Apagado |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. | Apagado |

## Consejos

- Si **Byp** se ilumina en naranja después de habilitar **MEM**, el ATU ha vuelto al modo bypass. Ejecute un nuevo ciclo de sintonización con **ATU** para crear una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que hay una memoria en uso, mientras que **Success** confirma que la solución almacenada es válida.

## Solución de problemas

- **El botón MEM aparece en gris y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria no puede alternarse en este modo. Verifique el modo de operación del TGXL antes de continuar.
- **El indicador Mem permanece apagado después de hacer clic en MEM** — No existe ninguna memoria ATU almacenada para la frecuencia actual. Primero ejecute un ciclo completo de sintonización del ATU usando **ATU** y luego intente **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ponga verde** — El ATU ha entrado en bypass porque no se encontró ninguna memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.

## Relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de prueba para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)
