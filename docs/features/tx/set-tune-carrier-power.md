# Establecer la potencia de portadora de sintonización

El regulador "Tune Pwr" establece el nivel de potencia de la portadora continua transmitida cuando presiona TUNE. Mantener este valor bajo protege sus finales y sistema de antena durante la sintonización del ATU o las pruebas de ROS.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX no está disponible sin una conexión de radio activa.
- Abra el applet TX Controls: haga clic en el botón TX tray en la barra lateral derecha si el applet aún no es visible.

## Pasos

1. Localice el regulador "Tune Pwr:" en el applet TX Controls.
2. Arrastre el regulador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonización. El valor numérico a la derecha del regulador se actualiza inmediatamente.
3. Suelte el regulador. El nuevo valor se envía a la radio.

## Qué hace cada control

| Control  | Descripción                                        | Predeterminado |
|----------|----------------------------------------------------|---------|
| Tune Pwr | Establece el nivel de potencia de la portadora de sintonización en vatios. | 10      |

## Consejos

- Establezca "Tune Pwr" en el nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores utilizan 10–20 W para la sintonización del ATU.
- La configuración "Tune Pwr" es independiente de "RF Power", que controla la potencia normal de transmisión. Ajustar una no afecta a la otra.
- Puede establecer valores predeterminados de potencia de sintonización por banda en `Settings > TX Band Settings...`.

## Relacionado

- [Iniciar una portadora de sintonización para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
