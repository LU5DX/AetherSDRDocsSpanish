# Ejecutar el ATU interno

Use el sintonizador automático de antena (ATU) interno para encontrar una coincidencia de bajo ROS en su frecuencia actual. Tras un ciclo de sintonía exitoso, el ATU almacena el resultado en memoria para recuperarlo rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX no funciona sin una conexión al radio.
- El TGXL no debe estar en modo OPERATE. El ATU se deshabilita cuando el TGXL está en modo OPERATE.
- Ajuste `Tune Pwr` a un nivel apropiado para su antena antes de ejecutar el ATU. El valor predeterminado es 10.

## Pasos

1. Haga clic en el botón TX del panel lateral derecho para abrir el applet TX Controls si no está visible.
2. Ajuste el control deslizante `Tune Pwr` al nivel de potencia de portadora de sintonía deseado (0–100; predeterminado 10).
3. Haga clic en `ATU` para iniciar el ciclo de sintonía.
4. Espere a que el ciclo de sintonía se complete. Observe los indicadores `Success`, `Byp` y `Mem` para ver el resultado.

## Función de cada control

| Control  | Tipo                  | Comportamiento                                                                                                                                                                                      |
|----------|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ATU      | Botón pulsador        | Inicia o pone en bypass el ATU según el contexto (consulte [Comportamiento del botón ATU](#atu-button-behavior)). Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM      | Botón de alternancia  | Activa o desactiva la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE.                                                                                           |
| Tune Pwr | Control deslizante    | Establece el nivel de potencia de la portadora de sintonía enviada al radio durante la sintonía.                                                                                                    |
| Success  | Indicador             | Se ilumina en verde cuando el resultado de la sintonía del ATU es exitoso u OK.                                                                                                                     |
| Byp      | Indicador             | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                                  |
| Mem      | Indicador             | Se ilumina en verde cuando el ATU utiliza una memoria almacenada.                                                                                                                                   |

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón `ATU` alterna entre iniciar un ciclo de sintonía y poner el sintonizador en bypass, según el estado actual del ATU y la frecuencia de transmisión. Esto refleja el comportamiento de alternancia por frecuencia de SmartSDR.

| Situación | Qué hace el clic en `ATU` |
|---|---|
| No hay sintonía previa en esta frecuencia, o el ATU no está en estado Successful/OK | Inicia un nuevo ciclo de sintonía del ATU. |
| El estado del ATU es Successful u OK, y la frecuencia de TX no ha cambiado desde la última sintonía | Pone el ATU en bypass. |
| El estado del ATU es Successful u OK, pero la frecuencia de TX ha cambiado desde la última sintonía | Inicia un nuevo ciclo de sintonía del ATU. |

En la práctica:
- El primer clic en una frecuencia nueva siempre inicia un ciclo de sintonía.
- Tras una sintonía exitosa, hacer clic en `ATU` nuevamente en la misma frecuencia pone el sintonizador en bypass.
- Cambiar de frecuencia reinicia la alternancia, por lo que el siguiente clic inicia un nuevo ciclo de sintonía independientemente del estado anterior.
- Entrar en bypass borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una nueva sintonía.

## Consejos

- Si `Byp` se ilumina tras el ciclo de sintonía, el ATU no pudo encontrar una coincidencia y se ha puesto en bypass automáticamente. Verifique su sistema de antena y el ROS antes de transmitir a plena potencia.
- Si `Mem` se ilumina, el ATU aplicó una memoria de sintonía almacenada previamente en lugar de ejecutar una sintonía completa. Esto es normal cuando `MEM` está habilitado y existe una memoria válida para la frecuencia actual.
- Para poner manualmente el sintonizador en bypass tras una sintonía exitosa, haga clic en `ATU` una segunda vez sin cambiar la frecuencia.

## Solución de problemas

- **El botón ATU no responde** — El TGXL del radio está en modo OPERATE. El ATU está deshabilitado en este modo. Cambie el TGXL fuera del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se ilumina tras la sintonía** — Es posible que el ATU haya entrado en bypass (verifique `Byp`) o que la potencia de la portadora de sintonía sea demasiado baja para que el ATU funcione con su antena. Aumente `Tune Pwr` e inténtelo de nuevo.
- **Al hacer clic en ATU entra en bypass en lugar de sintonizar** — El estado del ATU es Successful u OK y la frecuencia de TX no ha cambiado desde la última sintonía. Este es el comportamiento de bypass esperado en el segundo clic. Cambie la frecuencia para forzar un nuevo ciclo de sintonía, o deje el sintonizador en su estado actual de coincidencia.

## Relacionados

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Iniciar una portadora de sintonía para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Descripción general de TX Controls](overview.md)
