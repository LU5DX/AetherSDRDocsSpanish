# Ponga el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet del sintonizador para cambiar el 4O3A Tuner Genius XL entre sus tres estados de relé: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL.
- El botón de bandeja TUN debe estar disponible en la barra lateral derecha, lo que indica que se ha detectado el TGXL.

## Pasos

1. Haga clic en el botón de bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el botón OPERATE en el área inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso:
   - OPERATE → BYPASS
   - BYPASS → STANDBY
   - STANDBY → OPERATE

## Qué hace cada control

| Botón | Color cuando está activo | Significado |
|---|---|---|
| OPERATE | Verde | Los relés del sintonizador están en el circuito y activos. |
| BYPASS | Naranja | El sintonizador está energizado pero la red de adaptación está puenteada. |
| STANDBY | Predeterminado (depende del tema) | El sintonizador no está operando. |

La etiqueta y el color del botón se actualizan inmediatamente cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el siguiente. Una etiqueta verde OPERATE significa que el sintonizador ya está en OPERATE.
- Un solo clic desde STANDBY devuelve el sintonizador a OPERATE y restaura el color verde. No es necesario pasar por BYPASS para volver a OPERATE.

## Solución de problemas

- **El botón de bandeja TUN no es visible** — El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL en la red. Verifique que el TGXL esté encendido y conectado. Consulte [Tuner overview](overview.md).
- **La etiqueta del botón no cambia después de hacer clic** — La etiqueta se actualiza solo cuando el TGXL confirma el nuevo estado. Si la etiqueta permanece igual, verifique la conexión entre AetherSDR y el TGXL.

## Relacionado

- [Tuner overview](overview.md)
- [Run an autotune on the external TGXL](run-an-autotune-on-the-external-tgxl.md)
- [Read SWR immediately after a tune](read-swr-immediately-after-a-tune.md)
- [Fine-tune the C1/L/C2 relays with the mousewheel](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
