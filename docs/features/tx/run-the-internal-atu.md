# Ejecutar el sintonizador interno (ATU)

Utilice el sintonizador automático de antena interno (ATU) para encontrar una adaptación de baja ROE en su frecuencia actual. Después de un ciclo de sintonización exitoso, el ATU almacena el resultado en la memoria para recuperarlo rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La applet de TX no funciona sin una conexión al radio.
- El TGXL no debe estar en modo OPERATE. El ATU está deshabilitado cuando el TGXL está en modo OPERATE.
- Ajuste `Tune Pwr` a un nivel adecuado para su antena antes de ejecutar el ATU. El valor predeterminado es 10.

## Pasos

1. Haga clic en el botón de la bandeja TX en la barra lateral derecha para abrir la applet TX Controls si aún no está visible.
2. Ajuste el deslizador `Tune Pwr` al nivel de potencia de portadora de sintonización deseado (0–100; valor predeterminado 10).
3. Haga clic en `ATU` para iniciar el ciclo de sintonización.
4. Espere a que el ciclo de sintonización se complete. Supervise los indicadores `Success`, `Byp` y `Mem` para conocer el resultado.

## Qué hace cada control

| Control   | Tipo            | Comportamiento                                                                                                                                          |
|-----------|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| ATU       | Botón pulsador  | Inicia o pasa por alto el ATU según el contexto (consulte [Comportamiento del botón ATU](#comportamiento-del-botón-atu)). Deshabilitado cuando TGXL está en modo OPERATE. |
| MEM       | Botón de alternancia | Activa/desactiva la recuperación de memoria del ATU. Deshabilitado cuando TGXL está en modo OPERATE.                                             |
| Tune Pwr  | Deslizador      | Establece el nivel de potencia de portadora de sintonización enviado al radio durante la sintonización.                                                  |
| Success   | Indicador       | Se ilumina en verde cuando el resultado de la sintonización del ATU es exitoso u OK.                                                                         |
| Byp       | Indicador       | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                       |
| Mem       | Indicador       | Se ilumina en verde cuando el ATU está usando una memoria almacenada.                                                                                    |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón `ATU` alterna entre iniciar un ciclo de sintonización y cambiar el sintonizador a bypass, dependiendo del estado actual del ATU y la frecuencia de transmisión. Esto refleja el comportamiento de alternancia por frecuencia en SmartSDR.

| Situación                                                                                                      | Qué hace al hacer clic en `ATU`                                  |
|----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| No hay sintonización previa en esta frecuencia, o el ATU no está en estado Successful/OK                                     | Inicia un nuevo ciclo de sintonización del ATU.                  |
| El estado del ATU es Successful u OK, y la frecuencia de TX no ha cambiado desde la última sintonización.                  | Cambia el ATU a bypass.                                          |
| El estado del ATU es Successful u OK, pero la frecuencia de TX ha cambiado desde la última sintonización.                  | Inicia un nuevo ciclo de sintonización del ATU.                  |

En la práctica:
- El primer clic en una frecuencia nueva siempre inicia un ciclo de sintonización.
- Después de una sintonización exitosa, al hacer clic en `ATU` nuevamente en la misma frecuencia se pasa por alto el sintonizador.
- Cambiar la frecuencia restablece la alternancia, por lo que el siguiente clic inicia un nuevo ciclo de sintonización independientemente del estado anterior.
- Al entrar en bypass se borra la frecuencia sintonizada almacenada, por lo que el siguiente clic siempre inicia una nueva sintonización.

## MOX y tonos Quindar (v0.9.7)

A partir de v0.9.7, al hacer clic en `MOX` se enruta a través del coordinador de tonos Quindar en lugar de activar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y la slice de TX activa está en un modo de telefonía, al hacer clic en `MOX` para activar la transmisión se reproduce el tono K y al hacer clic nuevamente para desactivarla se reproduce el tono BK. Cuando Quindar está deshabilitado o la slice de TX activa no está en un modo de telefonía, `MOX` se comporta como antes y activa/desactiva la transmisión directamente.

## Consejos

- Si `Byp` se ilumina después del ciclo de sintonización, el ATU no pudo encontrar una adaptación y se ha puesto en bypass. Verifique su sistema de antena y la ROE antes de transmitir a máxima potencia.
- Si `Mem` se ilumina, el ATU aplicó una memoria de sintonización previamente almacenada en lugar de ejecutar una sintonización completa. Esto es normal cuando `MEM` está habilitado y existe una memoria válida para la frecuencia actual.
- Para forzar manualmente el sintonizador a bypass después de una sintonización exitosa, haga clic en `ATU` una segunda vez sin cambiar la frecuencia.

## Solución de problemas

- **El botón ATU no responde** — El TGXL del radio está en modo OPERATE. El ATU está deshabilitado en este modo. Cambie el TGXL fuera del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se ilumina después de la sintonización** — Es posible que el ATU haya entrado en bypass (verifique `Byp`) o que la potencia de portadora de sintonización sea demasiado baja para que el ATU funcione con su antena. Aumente `Tune Pwr` e intente nuevamente.
- **Al hacer clic en ATU se pasa por alto en lugar de sintonizar** — El estado del ATU es Successful u OK y la frecuencia de TX no ha cambiado desde la última sintonización. Este es el comportamiento esperado del segundo clic de bypass. Cambie la frecuencia para forzar un nuevo ciclo de sintonización o deje el sintonizador en su estado de adaptación actual.
- **Los tonos Quindar no se reproducen en MOX** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que la slice de TX activa está configurada en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.

## Relacionado

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de la portadora de sintonización](set-tune-carrier-power.md)
- [Descripción general de TX Controls](overview.md)
