# Habilitar Conexión a la Radio

`Settings > Connect to Radio...` abre el diálogo de conexión donde puede descubrir y conectarse a radios FLEX-8600 en su red. Use esta página para conectarse a una radio manualmente o para configurar si AetherSDR se conecta automáticamente al inicio.

## Antes de empezar

- AetherSDR está instalado y ejecutándose.
- Su FLEX-8600 está encendida y accesible en la misma red.

## Pasos

1. Haga clic en `Settings > Connect to Radio...`.
2. Se abre el diálogo de conexión y escanea la red en busca de radios FLEX-8600 disponibles.
3. Seleccione su radio de la lista descubierta.
4. Haga clic en `Connect`.

Para cambiar el comportamiento de conexión al inicio:

1. Haga clic en `Settings > Connect to Radio...`.
2. Marque o desmarque `Connect to last radio on start up`.
   - **Marcado (predeterminado):** AetherSDR intenta conectarse automáticamente al inicio usando descubrimiento por difusión y una sonda de radio enrutada.
   - **Desmarcado:** AetherSDR omite todos los intentos de conexión automática al inicio y abre el diálogo de conexión inmediatamente para que pueda seleccionar una radio manualmente.

## Qué hace cada control

| Control | Descripción | Predeterminado | Clave AppSettings |
|---|---|---|---|
| `Connect to last radio on start up` | Cuando está marcado, AetherSDR se conecta automáticamente al inicio. Cuando está desmarcado, el diálogo de conexión se abre al inicio para selección manual. | True | `AutoConnectToLastRadio` |

## Consejos

- Si desmarca `Connect to last radio on start up`, el diálogo de conexión se lanza automáticamente cada vez que AetherSDR se inicia, por lo que no necesita navegar a `Settings > Connect to Radio...` manualmente en inicios posteriores.

## Solución de problemas

- **No aparecen radios en el diálogo de conexión** — Confirme que la FLEX-8600 está encendida y conectada al mismo segmento de red que su computadora. Verifique que ningún cortafuegos esté bloqueando el tráfico UDP de difusión. Consulte [`enable-network.md`](enable-network.md) para diagnósticos de red.

## Relacionados

- [Getting Started](getting-started.md)
- [Enable Network](enable-network.md)
