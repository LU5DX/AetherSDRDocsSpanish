# Inicio automático de TCI al abrir la aplicación

Configure AetherSDR para iniciar el servidor WebSocket TCI automáticamente cada vez que se abra la aplicación, de modo que programas de terceros como Log4OM o las herramientas SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El servidor TCI requiere una conexión de radio activa.
- Abra el applet del servidor TCI haciendo clic en el botón TCI de la bandeja en la barra lateral derecha si desea verificar el estado del servidor después de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento del menú muestra una marca de verificación. El inicio automático está habilitado y se guarda como `AutoStartTCI`.
3. Reinicie AetherSDR. El servidor TCI se inicia automáticamente en el puerto almacenado en `TciPort` (predeterminado: `50001`).
4. En el applet del servidor TCI, confirme que el estado del servidor indica `:<port> (0 clients)` o un número mayor una vez que se conecte un cliente. El botón Enable aparecerá activo.

Para deshabilitar el inicio automático, haga clic de nuevo en `Settings > Autostart TCI with AetherSDR` para quitar la marca de verificación.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| `Settings > Autostart TCI with AetherSDR` | Elemento de menú con casilla. Cuando está marcado, inicia el servidor TCI al abrir la aplicación. | Off | On / Off | `AutoStartTCI` |
| Port | Puerto en el que escucha el servidor TCI. Si se cambia mientras el servidor está en ejecución, el servidor se reinicia. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI manualmente. Vuelve a Off y muestra `(port in use)` si no se puede enlazar el puerto. | Off | On / Off | — |
| RX1–RX4 gain+meter | Control deslizante de ganancia y medidor de nivel para cada canal RX de TCI. | 0.5 | 0.0–1.0 | `TciRxGain1` – `TciRxGain4` |
| TX gain+meter | Control deslizante de ganancia y medidor de nivel para el canal TX de TCI. | 0.5 | 0.0–1.0 | `TciTxGain` |

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True` la próxima vez que active Enable directamente en el applet; el elemento del menú y el botón Enable permanecen sincronizados.
- Si el puerto ya está en uso al iniciar la aplicación, el servidor no arrancará. Cambie `TciPort` a un puerto disponible antes de reiniciar.

## Solución de problemas

- **El estado del servidor muestra `(port in use)` después del inicio** — Otra aplicación está enlazada al puerto configurado. Abra el applet del servidor TCI, cambie Port a un valor no utilizado en el rango 1024–65535 y reinicie AetherSDR.
- **Enable vuelve a Off después del inicio** — El enlace falló. Consulte la entrada `(port in use)` anterior. `AutoStartTCI` se restablece automáticamente a `False` cuando se detecta un fallo de enlace.
- **`Settings > Autostart TCI with AetherSDR` no aparece** — Esta función requiere compatibilidad con WebSocket en la compilación de AetherSDR. Contacte a su fuente de distribución si el elemento del menú no está presente.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
