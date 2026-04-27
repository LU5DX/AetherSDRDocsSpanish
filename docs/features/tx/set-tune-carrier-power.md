# Ajustar la potencia del portador de sintonía

El control deslizante "Tune Pwr" establece el nivel de potencia del portador continuo que se transmite al presionar TUNE. Mantenerlo bajo protege los transistores finales y el sistema de antena durante la sintonía del ATU o las verificaciones de ROE.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX no está disponible sin una conexión de radio activa.
- Abra el applet TX Controls: haga clic en el botón TX del panel lateral derecho si el applet no está visible.

## Pasos

1. Ubique el control deslizante "Tune Pwr:" en el applet TX Controls.
2. Arrastre el control hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia del portador de sintonía. El valor numérico a la derecha del control se actualiza de inmediato.
3. Suelte el control. El nuevo valor se envía al radio.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido |
|---|---|---|---|
| Tune Pwr | Establece el nivel de potencia del portador de sintonía en vatios. | 10 | 0–100 |

## Consejos

- Ajuste "Tune Pwr" al nivel mínimo que permita al ATU encontrar una concordancia. Muchos operadores usan entre 10 y 20 W para la sintonía del ATU.
- El ajuste "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Modificar uno no afecta al otro.
- Puede configurar valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.

## Temas relacionados

- [Iniciar un portador de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
