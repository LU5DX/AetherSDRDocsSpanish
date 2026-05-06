# Habilitar la conexión a la radio

`Settings > Connect to Radio...` abre el diálogo de conexión, donde puede descubrir y conectarse a radios FLEX-8600 en su red. Use esta página para conectarse a una radio manualmente o para configurar si AetherSDR se conecta automáticamente al iniciar.

## Antes de comenzar

- AetherSDR está instalado y en ejecución.
- Su FLEX-8600 está encendido y es accesible en la misma red.

## Pasos

1. Haga clic en `Settings > Connect to Radio...`.
2. El diálogo de conexión se abre y escanea la red en busca de radios FLEX-8600 disponibles.
3. Seleccione su radio de la lista de dispositivos encontrados.
4. Haga clic en `Connect`.

Para cambiar el comportamiento de conexión al inicio:

1. Haga clic en `Settings > Connect to Radio...`.
2. Active o desactive `Connect to last radio on start up`.
   - **Activado (predeterminado):** AetherSDR intenta conectarse automáticamente al iniciar mediante descubrimiento por difusión y una sonda de radio enrutada.
   - **Desactivado:** AetherSDR omite todos los intentos de conexión automática al iniciar y abre el diálogo de conexión de inmediato para que pueda seleccionar una radio manualmente.

## Qué hace cada control

| Control | Descripción | Predeterminado | Clave de AppSettings |
|---|---|---|---|
| `Connect to last radio on start up` | Cuando está activado, AetherSDR se conecta automáticamente al iniciar. Cuando está desactivado, el diálogo de conexión se abre al inicio para selección manual. | True | `AutoConnectToLastRadio` |

## Consejos

- Si desactiva `Connect to last radio on start up`, el diálogo de conexión se abre automáticamente cada vez que AetherSDR inicia, por lo que no es necesario navegar a `Settings > Connect to Radio...` manualmente en los inicios posteriores.

## Solución de problemas

- **No aparecen radios en el diálogo de conexión** — Confirme que el FLEX-8600 está encendido y conectado al mismo segmento de red que su computadora. Verifique que ningún cortafuegos esté bloqueando el tráfico UDP de difusión. Consulte [`enable-network.md`](enable-network.md) para diagnósticos de red.

## Relacionados

- [Primeros pasos](getting-started.md)
- [Habilitar red](enable-network.md)
