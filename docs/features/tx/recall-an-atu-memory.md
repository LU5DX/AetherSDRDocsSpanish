# Recordar una memoria del ATU

Use la función de recordar memoria del ATU para aplicar una solución de sintonizador previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La applet TX Controls requiere una conexión activa al radio.
- El ATU interno del radio debe tener al menos una memoria almacenada de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, recordar una no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra la applet TX Controls. Si no está visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar el recordatorio de memoria del ATU.
3. Confirme que el indicador **Mem** se enciende en verde. Un indicador **Mem** verde confirma que el ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a un estado atenuado.

## Qué hace cada control

| Control | Tipo          | Comportamiento                                                                                                                                                                                  |
|---------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Activa/desactiva el recordatorio de memoria del ATU. Cuando está activado, el radio aplica una solución de sintonizador almacenada en lugar de ejecutar un nuevo ciclo de sintonización. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Mem     | Indicador     | Se enciende en verde cuando el ATU está usando una memoria. Atenuado cuando el recordatorio de memoria está desactivado o no hay ninguna memoria en uso.                                        |
| ATU     | Botón pulsador | Inicia o omite el ciclo de sintonización del ATU interno dependiendo del estado actual y la frecuencia. Consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu) a continuación. Deshabilitado cuando el TGXL está en modo OPERATE. |
| Success | Indicador     | Se enciende en verde cuando el estado del ATU es Successful u OK.                                                                                                                               |
| Byp     | Indicador     | Se enciende en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                             |

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** alterna entre sintonización y bypass por frecuencia, coincidiendo con el comportamiento de SmartSDR. Haga clic derecho en el botón **ATU** para acceder a opciones adicionales de gestión del ATU.

| Situación | Resultado al hacer clic en ATU |
|-----------|--------------------------------|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Cambia el ATU a bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización del ATU. |

**Puntos clave:**

- El radio recuerda la frecuencia en la que el ATU reportó por última vez una sintonización exitosa. Si cambia la frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de pasar a bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entra en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales, coincidiendo con SmartSDR Windows:

| Acción | Descripción |
|--------|-------------|
| **Pre-tune bands…** | Abre un diálogo para ejecutar un barrido de presintonización en las bandas seleccionadas. Esta acción solo está disponible cuando el recordatorio de memoria del ATU (MEM) está habilitado. Si MEM está desactivado, la acción aparece atenuada con una sugerencia que indica que habilite MEM primero. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias almacenadas del ATU en el radio. |

## MOX y tonos Quindar (v0.9.7)

A partir de la v0.9.7, al hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de alternar directamente la transmisión. Cuando el chip QUIN está habilitado en la tira de canales de audio y la slice TX activa está en un modo de telefonía, el tono K se reproduce al activar PTT y el tono BK se reproduce al desactivar PTT. Cuando Quindar está deshabilitado o la slice TX activa no está en un modo de telefonía, el comportamiento es idéntico a versiones anteriores.

No se requiere configuración adicional en la applet TX Controls. Habilite o deshabilite los tonos Quindar desde el control QUIN en la tira de canales de audio.

## Menú contextual de TUNE (v26.5.2.1)

Haga clic derecho en el botón **TUNE** para establecer la forma de la portadora para el próximo ciclo de sintonización. Esta es una selección de un solo uso: el modo de sintonización del radio se almacena en un estado volátil y no se conserva entre ciclos de encendido ni se guarda en la configuración de AetherSDR.

| Opción del menú | Descripción |
|-------------|-------------|
| **Mono Tone** | Establece la portadora de sintonización en un solo tono. Este es el comportamiento predeterminado. |
| **Two Tone** | Establece la portadora de sintonización en un patrón de dos tonos. |

El modo de sintonización actualmente activo se muestra con una marca de verificación. Seleccionar una opción la aplica inmediatamente para la próxima pulsación de TUNE.

## Indicador de pico y retención de potencia directa (v26.5.2.1)

El medidor **RF Pwr** ahora incluye una barra de pico y retención que rastrea la potencia de pico de envolvente (PEP). El valor pico se mantiene durante 2 segundos, luego decae suavemente hacia el nivel de potencia actual. La tasa de decaimiento se escala al rango completo de la escala del medidor (120 W sin amplificador o 600 W con el excitador Aurora 500W), por lo que la sensación visual permanece consistente.

- El valor de pico y retención se restablece a cero inmediatamente cuando el radio desactiva la transmisión, evitando que una lectura PEP retenida persista entre sobres.
- El comportamiento de pico y retención coincide con la barra de pico y retención de SmartSDR y el patrón de pico y retención del S-meter de recepción.

## Consejos

- Si **Byp** se enciende en naranja después de habilitar **MEM**, el ATU ha vuelto a bypass. Ejecute un nuevo ciclo de sintonización con **ATU** para crear una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar encendidos al mismo tiempo; **Mem** confirma que una memoria está en uso, mientras que **Success** confirma que la solución almacenada es válida.
- Para omitir el ATU sin ejecutar un nuevo ciclo de sintonización, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonización exitosa. El indicador **Byp** se encenderá en naranja para confirmar que el bypass está activo.
- Para borrar las memorias del ATU en todas las bandas, haga clic derecho en **ATU** y seleccione **Clear ATU memories…**. Use **Pre-tune bands…** para reconstruir las memorias para las bandas de uso frecuente.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. El recordatorio de memoria no se puede alternar en este modo. Verifique el modo de operación del TGXL antes de continuar.
- **El indicador Mem permanece atenuado después de hacer clic en MEM** — No existe una memoria del ATU almacenada para la frecuencia actual. Ejecute un ciclo completo de sintonización del ATU usando **ATU** primero, luego intente **MEM** nuevamente.
- **Byp se enciende en naranja en lugar de que Mem se ponga verde** — El ATU ha entrado en bypass porque no se encontró ninguna memoria útil. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no pasará a bypass hasta que vuelva a la frecuencia exacta que fue sintonizada. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen tonos Quindar** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que la slice TX activa está configurada en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **Pre-tune bands… está atenuado** — Habilite MEM primero haciendo clic en el botón **MEM**. El barrido de presintonización requiere que el recordatorio de memoria esté activo.

## Relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Resumen de TX Controls](overview.md)
