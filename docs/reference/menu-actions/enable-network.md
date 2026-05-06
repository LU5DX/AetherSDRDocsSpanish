# Diagnósticos de red

Abra la ventana Network diagnostics para ver el estado de la conexión y la salida del registro en tiempo real para los subsistemas de red de AetherSDR. Úsela para solucionar problemas de conectividad con la radio, fuentes de clúster DX o tecleo CW a través de la red.

## Antes de comenzar

- AetherSDR debe estar en ejecución.

## Pasos

1. Haga clic en `Settings` en la barra de menús.
2. Haga clic en `Network...`.

Se abre el diálogo Network Diagnostics.

3. Haga clic en la pestaña **Logs** para ver la salida del registro en tiempo real.
4. Use las casillas de verificación de filtro por categoría para mostrar u ocultar entradas del registro según la categoría (por ejemplo, `aether.connection`, `aether.dxcluster`, `aether.cw`).

## Qué hace cada control

| Control | Descripción |
|---|---|
| Pestaña **Logs** | Muestra una vista en tiempo real de la salida del registro limitada a las categorías de diagnóstico. Se actualiza cada 500 ms. |
| Casillas de verificación de filtro por categoría | Cada casilla corresponde a una categoría de registro (`aether.connection`, `aether.dxcluster`, `aether.cw`, entre otras). Desmarque una categoría para ocultar sus entradas de la vista en tiempo real. |

## Consejos

- La pestaña **Logs** se actualiza cada 500 ms. No hay un control de actualización manual; la salida se actualiza automáticamente.
- Filtre por una sola categoría, como `aether.connection`, cuando diagnostique fallos de conexión con la radio, para reducir el ruido de subsistemas no relacionados.

## Relacionados

- [Activar conexión a la radio](enable-connect-to-radio.md)
- [Primeros pasos](getting-started.md)
