# Poner el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet del sintonizador para ciclar el 4O3A Tuner Genius XL a través de sus tres estados de relé: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL.
- El botón TUN en la bandeja debe estar disponible en la barra lateral derecha, indicando que se ha detectado el TGXL.

## Pasos

1. Haga clic en el botón TUN de la bandeja en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el botón OPERATE en el área inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso:
   - OPERATE → BYPASS
   - BYPASS → STANDBY
   - STANDBY → OPERATE

## Qué hace cada control

| Botón | Color cuando está activo | Significado |
|---|---|---|
| OPERATE | Verde | Los relés del sintonizador están en circuito y activos. |
| BYPASS | Naranja | El sintonizador está energizado pero la red de adaptación está puenteada. |
| STANDBY | Predeterminado (azul-gris) | El sintonizador no está operando. |

La etiqueta y el color del botón se actualizan inmediatamente cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el siguiente. Una etiqueta verde OPERATE significa que el sintonizador ya está en OPERATE.
- Al hacer clic una vez desde STANDBY, el sintonizador vuelve a OPERATE y restaura el color verde. No es necesario pasar por BYPASS para regresar a OPERATE.

## Solución de problemas

- **El botón TUN de la bandeja no es visible** — El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL en la red. Verifique que el TGXL esté encendido y conectado. Consulte [Descripción general del sintonizador](overview.md).
- **La etiqueta del botón no cambia después de hacer clic** — La etiqueta se actualiza solo cuando el TGXL confirma el nuevo estado. Si la etiqueta permanece igual, verifique la conexión entre AetherSDR y el TGXL.

## Relacionado

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de una sintonía](read-swr-immediately-after-a-tune.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
