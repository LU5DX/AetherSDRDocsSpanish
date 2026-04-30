# Recuperar una memoria del ATU

Use la recuperación de memoria del ATU para aplicar una solución de sintonización almacenada previamente para la banda o frecuencia actual, omitiendo un ciclo de sintonización completo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls requiere una conexión de radio activa.
- El ATU interno de la radio debe tener almacenada al menos una memoria de un ciclo de sintonización anterior. Si no existe memoria para la frecuencia actual, recuperar una no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet TX Controls. Si no es visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** verde confirma que el ATU está utilizando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a oscurecerse.

## Qué hace cada control

| Control | Tipo          | Comportamiento                                                                                                                                                          |
|---------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Activa/desactiva la recuperación de memoria del ATU. Cuando está activado, la radio aplica una solución de sintonización almacenada en lugar de ejecutar un nuevo ciclo de sintonización. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Mem     | Indicador     | Se ilumina en verde cuando el ATU está utilizando una memoria. Oscuro cuando la recuperación de memoria está desactivada o no hay memoria en uso.                                                                |
| Success | Indicador     | Se ilumina en verde cuando el estado del ATU es Successful (Exitoso) u OK.                                                                                                                 |
| Byp     | Indicador     | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                          |

## Consejos

- Si **Byp** se ilumina en naranja después de habilitar **MEM**, el ATU ha vuelto al bypass. Ejecute un ciclo de sintonización nuevo con **ATU** para crear una memoria nueva para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que se está utilizando una memoria, mientras que **Success** confirma que la solución almacenada es válida.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria no se puede alternar en este modo. Verifique el modo de funcionamiento del TGXL antes de continuar.
- **El indicador Mem permanece oscuro después de hacer clic en MEM** — No existe memoria del ATU almacenada para la frecuencia actual. Ejecute primero un ciclo de sintonización completo del ATU usando **ATU**, luego intente **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ilumine en verde** — El ATU ha entrado en bypass porque no se encontró memoria utilizable. Use **ATU** para sintonizar y almacenar una solución nueva.

## Relacionado

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar un portadora de sintonización para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)
