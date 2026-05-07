# Recordar una Memoria del ATU

Use la función de recuperación de memoria del ATU para aplicar una solución de sintonizador previamente almacenada para la banda o frecuencia actual, evitando un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión de radio activa.
- El ATU interno de la radio debe tener al menos una memoria almacenada de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, recuperar una no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet Controles de TX. Si no está visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** verde confirma que el ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve al estado atenuado.

## Función de cada control

| Control | Tipo          | Comportamiento                                                                                                                                                                                          |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Activa/desactiva la recuperación de memoria del ATU. Cuando está activado, la radio aplica una solución de sintonizador almacenada en lugar de ejecutar un nuevo ciclo de sintonización. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Mem     | Indicador     | Se ilumina en verde cuando el ATU está usando una memoria. Atenuado cuando la recuperación de memoria está desactivada o no hay ninguna memoria en uso.                                                    |
| ATU     | Botón pulsador | Inicia o omite el ciclo de sintonización del ATU interno según el estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu) a continuación. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Success | Indicador     | Se ilumina en verde cuando el estado del ATU es Successful u OK.                                                                                                                                       |
| Byp     | Indicador     | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                                      |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón **ATU** alterna entre sintonización y bypass por frecuencia, coincidiendo con el comportamiento de SmartSDR.

| Situación | Resultado al hacer clic en ATU |
|-----------|--------------------------------|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Cambia el ATU a bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización del ATU. |

**Puntos clave:**

- La radio recuerda la frecuencia a la que el ATU reportó por última vez una sintonización exitosa. Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de pasar a bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entre en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de alternar directamente la transmisión. Cuando el chip QUIN está habilitado en la tira de canales de audio y la porción de TX activa está en un modo de telefonía, el tono K suena al activar PTT y el tono BK suena al desactivar PTT. Cuando Quindar está deshabilitado o la porción de TX activa no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores.

No se requiere configuración adicional en el applet Controles de TX. Habilite o deshabilite los tonos Quindar desde el control QUIN de la tira de canales de audio.

## Consejos

- Si **Byp** se ilumina en naranja después de habilitar **MEM**, el ATU ha entrado en bypass. Ejecute un nuevo ciclo de sintonización con **ATU** para crear una nueva memoria para la frecuencia actual.
- Los indicadores **Mem** y **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para omitir el ATU sin ejecutar un nuevo ciclo de sintonización, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonización exitosa. El indicador **Byp** se iluminará en naranja para confirmar que el bypass está activo.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria no se puede alternar en este modo. Verifique el modo de operación del TGXL antes de continuar.
- **El indicador Mem permanece atenuado después de hacer clic en MEM** — No hay ninguna memoria del ATU almacenada para la frecuencia actual. Ejecute primero un ciclo completo de sintonización del ATU usando **ATU**, luego intente **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ponga verde** — El ATU ha entrado en bypass porque no se encontró ninguna memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no omitirá hasta que esté de nuevo en la frecuencia exacta que se sintonizó. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen tonos Quindar** — Confirme que el chip QUIN esté habilitado en la tira de canales de audio y que la porción de TX activa esté configurada en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.

## Relacionado

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Resumen de Controles de TX](overview.md)
