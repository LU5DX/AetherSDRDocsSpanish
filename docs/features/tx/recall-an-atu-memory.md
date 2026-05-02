# Recuperar una memoria del sintonizador automático (ATU)

Use la recuperación de memoria del ATU para aplicar una solución de sintonización previamente almacenada para la banda o frecuencia actual, sin necesidad de ejecutar un ciclo completo de sintonización.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet TX Controls requiere una conexión activa con el equipo.
- El ATU interno del equipo debe tener almacenada al menos una memoria de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, recuperar una no tendrá ningún efecto.
- MEM está deshabilitado cuando el TGXL se encuentra en modo OPERATE.

## Pasos

1. Abra el applet TX Controls. Si no está visible, haga clic en el botón **TX** de la bandeja en la barra lateral derecha.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** en verde confirma que el ATU está utilizando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a apagarse.

## Qué hace cada control

| Control | Tipo               | Comportamiento                                                                                                                                                                      |
|---------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Cuando está activo, el equipo aplica una solución de sintonización almacenada en lugar de ejecutar un nuevo ciclo de sintonización. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Mem     | Indicador          | Se ilumina en verde cuando el ATU está usando una memoria. Apagado cuando la recuperación de memoria está desactivada o no hay ninguna memoria en uso.                              |
| ATU     | Botón de acción    | Inicia o omite el ciclo de sintonización del ATU interno según el estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#atu-button-behavior) a continuación. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Success | Indicador          | Se ilumina en verde cuando el estado del ATU es Successful u OK.                                                                                                                    |
| Byp     | Indicador          | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                  |

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón **ATU** alterna entre sintonización y bypass por frecuencia, siguiendo el comportamiento de SmartSDR.

| Situación | Resultado al hacer clic en ATU |
|-----------|-------------------------------|
| No hay sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Pone el ATU en bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización del ATU. |

**Puntos clave:**

- El equipo recuerda la frecuencia en la que el ATU reportó por última vez una sintonización exitosa. Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de activar el bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entra en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## Sugerencias

- Si **Byp** se ilumina en naranja después de activar **MEM**, el ATU ha vuelto al modo bypass. Ejecute un nuevo ciclo de sintonización con **ATU** para generar una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para poner el ATU en bypass sin ejecutar un nuevo ciclo de sintonización, haga clic en **ATU** por segunda vez en la misma frecuencia donde ocurrió la última sintonización exitosa. El indicador **Byp** se iluminará en naranja para confirmar que el bypass está activo.

## Resolución de problemas

- **El botón MEM aparece atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria no puede activarse o desactivarse en este modo. Verifique el modo de operación del TGXL antes de continuar.
- **El indicador Mem permanece apagado después de hacer clic en MEM** — No existe ninguna memoria del ATU almacenada para la frecuencia actual. Ejecute primero un ciclo completo de sintonización con **ATU** y luego intente con **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ilumine en verde** — El ATU ha entrado en bypass porque no se encontró ninguna memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de activar el bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no activará el bypass hasta que regrese exactamente a la frecuencia que fue sintonizada. Sintonice nuevamente en la frecuencia actual primero.

## Relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)
