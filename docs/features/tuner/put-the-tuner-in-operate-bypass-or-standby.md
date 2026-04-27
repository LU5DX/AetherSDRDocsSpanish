# Poner el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet del sintonizador para hacer avanzar el 4O3A Tuner Genius XL por sus tres estados de relé: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet del sintonizador permanece oculto hasta que se detecta un Tuner Genius XL.
- El botón TUN del panel lateral derecho debe estar disponible, lo que indica que el TGXL ha sido detectado.

## Pasos

1. Haga clic en el botón TUN del panel lateral derecho para abrir el applet del sintonizador.
2. Localice el botón OPERATE en la zona inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso:
   - OPERATE → BYPASS
   - BYPASS → STANDBY
   - STANDBY → OPERATE

## Qué hace cada control

| Botón | Color cuando está activo | Significado |
|---|---|---|
| OPERATE | Verde | Los relés del sintonizador están en el circuito y activos. |
| BYPASS | Naranja | El sintonizador está energizado, pero la red de adaptación está puenteada. |
| STANDBY | Predeterminado (azul grisáceo) | El sintonizador no está en funcionamiento. |

La etiqueta y el color del botón se actualizan de inmediato cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el siguiente. Una etiqueta OPERATE en verde significa que el sintonizador ya está en OPERATE.
- Al hacer clic una vez desde STANDBY, el sintonizador vuelve a OPERATE y se restaura el color verde. No es necesario pasar por BYPASS para regresar a OPERATE.

## Solución de problemas

- **El botón TUN no es visible** — El applet del sintonizador permanece oculto hasta que se detecta un Tuner Genius XL en la red. Verifique que el TGXL esté encendido y conectado. Consulte [Descripción general del sintonizador](overview.md).
- **La etiqueta del botón no cambia después de hacer clic** — La etiqueta se actualiza únicamente cuando el TGXL confirma el nuevo estado. Si la etiqueta no cambia, verifique la conexión entre AetherSDR y el TGXL.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer el ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
