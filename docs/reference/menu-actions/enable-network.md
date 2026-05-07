# Diagnóstico de red

Abra la ventana de diagnóstico de red para ver el estado de la conexión y el registro de salida en vivo de los subsistemas de red de AetherSDR. Úsela al solucionar problemas de conectividad de radio, fuentes de datos del DX Cluster o tecleado CW a través de la red.

## Antes de comenzar

- AetherSDR debe estar en ejecución.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Network...`.

Se abre el diálogo de Diagnóstico de red.

3. Haga clic en la pestaña **Logs** para ver la salida de registro en vivo.
4. Use las casillas de verificación de filtro por categoría para mostrar u ocultar entradas del registro según la categoría (por ejemplo, `aether.connection`, `aether.dxcluster`, `aether.cw`).

## Función de cada control

| Control | Descripción |
|---|---|
| Pestaña **Logs** | Muestra una cola en vivo de la salida del registro limitada a las categorías de diagnóstico. Se actualiza cada 500 ms. |
| Casillas de verificación de filtro por categoría | Cada casilla corresponde a una categoría de registro (`aether.connection`, `aether.dxcluster`, `aether.cw` y otras). Desmarque una categoría para ocultar sus entradas de la cola de registro. |

## Consejos

- La pestaña Logs se actualiza cada 500 ms. No hay un control de actualización manual; la salida se actualiza automáticamente.
- Filtre por una sola categoría, como `aether.connection`, al diagnosticar fallos de conexión de radio para reducir el ruido de subsistemas no relacionados.

## Relacionado

- [Habilitar conexión a la radio](enable-connect-to-radio.md)
- [Primeros pasos](getting-started.md)
