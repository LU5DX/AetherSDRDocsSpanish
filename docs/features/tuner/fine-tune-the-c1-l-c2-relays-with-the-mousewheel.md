# Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Use la rueda del ratón sobre las barras de relé C1, L o C2 para incrementar o decrementar las posiciones de los relés manualmente. Esto permite ajustar la red del sintonizador después de un autotune o establecer un punto de partida de forma manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Se debe detectar un sintonizador 4O3A Tuner Genius XL; el botón TUN de la bandeja aparece en la barra lateral derecha únicamente cuando hay uno presente.
- El TGXL debe estar conectado mediante una conexión directa TGXL. El desplazamiento con la rueda del ratón sobre las barras de relé está deshabilitado cuando solo hay una conexión mediada por radio activa.

## Pasos

1. Haga clic en el botón TUN de la bandeja en la barra lateral derecha para abrir el applet del sintonizador.
2. Confirme que las barras de relé C1, L y C2 son visibles en la sección inferior izquierda del applet.
3. Coloque el puntero del ratón sobre la barra C1, L o C2 que desea ajustar.
4. Desplace la rueda del ratón hacia arriba para incrementar la posición del relé, o hacia abajo para decrementarla.
5. Repita el proceso para cada barra que desee ajustar.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Valor predeterminado |
|---------|-------------|--------------|----------------------|
| C1 | Posición del banco de relés C1 | 0–255 | 0 |
| L | Posición del banco de relés L | 0–255 | 0 |
| C2 | Posición del banco de relés C2 | 0–255 | 0 |

Ninguno de estos controles almacena una clave de configuración; los valores reflejan el estado en tiempo real reportado por el TGXL.

## Consejos

- El ajuste con la rueda del ratón solo está disponible cuando hay una conexión directa TGXL activa. Si al desplazar las barras no se produce ningún efecto, verifique el estado de la conexión TGXL.
- Las barras de relé se actualizan en tiempo real a medida que el TGXL confirma cada paso. Observe el medidor de ROE mientras desplaza la rueda para encontrar una ROE más baja de forma manual.
- Para restablecer un estado de red conocido, ejecute primero un autotune y luego use la rueda del ratón para realizar el ajuste fino a partir del resultado.

## Solución de problemas

- **Desplazar la barra de relé no tiene efecto** — La conexión directa TGXL no está activa. La entrada de la rueda del ratón está deshabilitada cuando solo hay una conexión mediada por radio presente. Verifique la conexión directa TGXL e intente de nuevo.

## Relacionados

- [Ejecutar un autotune en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
