# Configurar la potencia de la portadora de sintonía

El control deslizante "Tune Pwr" ajusta el nivel de potencia de la portadora continua transmitida al presionar TUNE. Mantenerlo bajo protege sus etapas finales y su sistema de antena durante la sintonización del ATU o las comprobaciones de ROE.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La applet TX no está disponible sin una conexión activa con la radio.
- Abra la applet TX Controls: haga clic en el botón de la bandeja TX en la barra lateral derecha si la applet aún no está visible.

## Pasos

1. Localice el control deslizante "Tune Pwr:" en la applet TX Controls.
2. Arrastre el control deslizante hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonía. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente.
3. Suelte el control deslizante. El nuevo valor se envía a la radio.

## Función de cada control

| Control    | Descripción                                                | Valor predeterminado |
|------------|------------------------------------------------------------|----------------------|
| Tune Pwr   | Ajusta el nivel de potencia de la portadora de sintonía en vatios. | 10                   |

## Consejos

- Ajuste "Tune Pwr" al nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores usan 10–20 W para la sintonización del ATU.
- La configuración de "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Ajustar una no afecta a la otra.
- Puede establecer valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón ATU alterna entre iniciar un ciclo de sintonía y puentear el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y de su frecuencia de transmisión:

| Situación | Qué hace al hacer clic en ATU |
|---|---|
| No existe una sintonía exitosa para la frecuencia actual | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU informa una coincidencia exitosa y la frecuencia de transmisión no ha cambiado desde esa sintonía | Cambia el ATU a modo bypass. |
| El ATU informa una coincidencia exitosa pero la frecuencia de transmisión ha cambiado desde esa sintonía | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU ya está en modo bypass | Inicia un nuevo ciclo de sintonía del ATU. |

En la práctica, esto significa:

1. Haga clic en ATU en una nueva frecuencia. La radio ejecuta un ciclo de sintonía. El indicador Success se enciende en verde cuando se encuentra una coincidencia.
2. Vuelva a hacer clic en ATU sin cambiar la frecuencia. El sintonizador entra en bypass. El indicador Byp se enciende en naranja y el indicador Success se atenúa.
3. Cambie la frecuencia y haga clic en ATU. La radio ejecuta un nuevo ciclo de sintonía, independientemente del resultado anterior.

Los botones ATU y MEM están deshabilitados cuando TGXL está en modo OPERATE.

## Botón MOX y tonos Quindar (v0.9.7)

A partir de la versión v0.9.7, al hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Esto significa:

- Al **activar**: si Quindar está habilitado en Audio Channel Strip y el slice TX activo está en un modo de telefonía, el tono K suena antes de que el transmisor se active.
- Al **desactivar**: el tono BK suena después de que el transmisor se desactive.
- Si Quindar está deshabilitado, o el slice TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores: el transmisor se activa y desactiva inmediatamente.

El botón MOX continúa mostrando azul (recepción) y rojo (transmisión) como antes. No se necesita configuración en la applet TX Controls; el comportamiento de los tonos Quindar se controla completamente desde Audio Channel Strip.

## Relacionados

- [Iniciar una portadora de sintonía para comprobar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
