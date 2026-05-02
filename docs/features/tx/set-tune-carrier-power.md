# Ajustar la potencia del portador de ajuste

El control deslizante "Tune Pwr" establece el nivel de potencia del portador continuo que se transmite al presionar TUNE. Mantenerlo bajo protege los transistores finales y el sistema de antena durante el ajuste del ATU o las verificaciones de ROE.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX no está disponible sin una conexión de radio activa.
- Abra el applet TX Controls: haga clic en el botón TX del área de notificación en la barra lateral derecha si el applet no está visible.

## Pasos

1. Localice el control deslizante "Tune Pwr:" en el applet TX Controls.
2. Arrastre el control hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia del portador de ajuste. El valor numérico a la derecha del control se actualiza de inmediato.
3. Suelte el control. El nuevo valor se envía al radio.

## Función de cada control

| Control  | Descripción                                                  | Valor predeterminado |
|----------|--------------------------------------------------------------|----------------------|
| Tune Pwr | Establece el nivel de potencia del portador de ajuste en W. | 10                   |

## Consejos

- Ajuste "Tune Pwr" al nivel mínimo que permita al ATU encontrar una concordancia. Muchos operadores usan entre 10 y 20 W para el ajuste del ATU.
- El ajuste de "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Modificar uno no afecta al otro.
- Puede establecer valores predeterminados de potencia de ajuste por banda en `Settings > TX Band Settings...`.

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón ATU alterna entre iniciar un ciclo de ajuste y puentear el sintonizador, reflejando el comportamiento por frecuencia de SmartSDR.

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y de la frecuencia de transmisión:

| Situación | Qué hace el clic en ATU |
|---|---|
| No existe un ajuste exitoso para la frecuencia actual | Inicia un nuevo ciclo de ajuste del ATU. |
| El ATU reporta una concordancia exitosa y la frecuencia de transmisión no ha cambiado desde ese ajuste | Pone el ATU en modo puente (bypass). |
| El ATU reporta una concordancia exitosa pero la frecuencia de transmisión ha cambiado desde ese ajuste | Inicia un nuevo ciclo de ajuste del ATU. |
| El ATU ya está en modo puente (bypass) | Inicia un nuevo ciclo de ajuste del ATU. |

En la práctica esto significa:

1. Haga clic en ATU en una frecuencia nueva. El radio ejecuta un ciclo de ajuste. El indicador Success se ilumina en verde cuando se encuentra una concordancia.
2. Haga clic en ATU nuevamente sin cambiar la frecuencia. El sintonizador entra en modo puente. El indicador Byp se ilumina en naranja y el indicador Success se apaga.
3. Cambie la frecuencia y haga clic en ATU. El radio ejecuta un nuevo ciclo de ajuste independientemente del resultado anterior.

El botón ATU y el botón MEM quedan deshabilitados cuando TGXL está en modo OPERATE.

## Temas relacionados

- [Iniciar un portador de ajuste para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
