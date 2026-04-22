# Poner el sintonizador en OPERATE, BYPASS o STANDBY

El botón OPERATE hace avanzar el 4O3A Tuner Genius XL por sus tres estados de relé: OPERATE, BYPASS y STANDBY. Use esta función para activar o desactivar la red del sintonizador sin salir del applet.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Tuner permanece oculto hasta que se detecta un Tuner Genius XL.
- Abra el applet Tuner haciendo clic en el botón "TUN" de la bandeja en la barra lateral derecha.

## Pasos

1. Localice el botón "OPERATE" en el área inferior derecha del applet Tuner.
2. Haga clic en el botón una vez para avanzar al siguiente estado. Cada clic avanza un paso: OPERATE → BYPASS → STANDBY → OPERATE.

## Qué hace cada control

| Etiqueta del botón | Color | Significado |
|---|---|---|
| OPERATE | Verde | La red del sintonizador está activa. Los ajustes de relé están en funcionamiento. |
| BYPASS | Naranja | El sintonizador está energizado, pero la red de adaptación está puenteada. |
| STANDBY | Predeterminado (azul grisáceo) | El sintonizador está en espera. La señal de RF pasa sin intervención del sintonizador. |

La etiqueta y el color del botón se actualizan de inmediato para reflejar el nuevo estado tal como lo informa el TGXL.

## Consejos

- Cada clic avanza exactamente un paso. Para pasar de STANDBY directamente a BYPASS, es necesario pasar primero por OPERATE.
- El estado actual que muestra el botón refleja lo que el TGXL ha confirmado, no solo lo que se solicitó. Si la etiqueta no cambia después de un clic, el TGXL aún no ha reconocido el comando.

## Solución de problemas

- **El botón "TUN" de la bandeja no es visible** — El applet Tuner solo aparece cuando se detecta un Tuner Genius XL. Verifique que el TGXL esté conectado y encendido, y que AetherSDR esté conectado al radio.
- **La etiqueta del botón no cambia después de hacer clic** — El applet refleja el estado informado por el TGXL. Una conexión lenta o interrumpida entre el radio y el TGXL puede retrasar o impedir el reconocimiento del comando. Verifique la conexión del TGXL e intente de nuevo.

## Temas relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)
