# Poner el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet Tuner para alternar el 4O3A Tuner Genius XL entre sus tres estados de relé: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Tuner permanece oculto hasta que se detecte un Tuner Genius XL.
- El botón TUN en la bandeja del panel lateral derecho debe estar disponible, lo que confirma que el TGXL ha sido detectado.

## Pasos

1. Haga clic en el botón TUN de la bandeja del panel lateral derecho para abrir el applet Tuner.
2. Localice el botón OPERATE en la parte inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso: OPERATE → BYPASS → STANDBY → OPERATE.

## Qué hace cada control

| Etiqueta del botón | Color | Significado |
|---|---|---|
| OPERATE | Verde | La red del sintonizador está en circuito y realizando ajuste activo. |
| BYPASS | Naranja | El relé del sintonizador está puenteado; la RF pasa sin ajuste. |
| STANDBY | Predeterminado (azul grisáceo) | El sintonizador está en espera; la red de relés no está en circuito ni puenteada activamente. |

La etiqueta y el color del botón se actualizan de inmediato cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el estado que está por seleccionar. Una etiqueta OPERATE en verde significa que el sintonizador ya está en OPERATE; al hacer clic pasará a BYPASS.
- Si acaba de ejecutar un autotune, el sintonizador entra en OPERATE automáticamente. No es necesario hacer clic en OPERATE después de un ciclo de ajuste exitoso.

## Solución de problemas

- **El botón TUN de la bandeja no es visible** — El TGXL no ha sido detectado. Verifique la conexión entre la radio y el sintonizador, y confirme que el sintonizador está encendido.
- **La etiqueta del botón no cambia al hacer clic** — La radio no ha confirmado el cambio de estado. Verifique que la conexión con la radio esté activa mediante `Settings > Connect to Radio...` e intente de nuevo.

## Relacionados

- [Ejecutar un autotune en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Descripción general del sintonizador](overview.md)
