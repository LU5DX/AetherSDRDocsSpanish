# Inicio automático de TCI al abrir la aplicación

Configure AetherSDR para iniciar el servidor TCI automáticamente cada vez que la aplicación se abre, de modo que programas de terceros como Log4OM o las herramientas de SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte para WebSocket (`HAVE_WEBSOCKETS`). Si el elemento de menú `Settings > Autostart TCI with AetherSDR` no está visible, su versión no incluye TCI.
- Compruebe que el servidor TCI funciona manualmente antes de habilitar el inicio automático. Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- Decida qué puerto desea que utilice el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart TCI with AetherSDR`.

Aparece una marca de verificación junto al elemento. AetherSDR guarda esta elección como `AutoStartTCI`.

En el siguiente inicio, AetherSDR arranca el servidor TCI en el puerto almacenado en `TciPort` antes de que se muestre el panel de applets. El botón TCI en la bandeja del sistema y el indicador de estado del servidor en el applet TCI Server reflejan automáticamente el estado de ejecución.

Para deshabilitar el inicio automático, repita los pasos 1–2. La marca de verificación desaparece y el servidor dejará de iniciarse al abrir la aplicación.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| `Autostart TCI with AetherSDR` | Elemento de menú con casilla de verificación. Cuando está marcado, el servidor TCI se inicia en cada apertura. | Desactivado | Activado / Desactivado | `AutoStartTCI` |
| Puerto | Puerto TCP al que se enlaza el servidor. Configúrelo en el applet TCI Server antes de habilitar el inicio automático. | `50001` | 1024–65535 | `TciPort` |
| Ganancia RX1–RX4 | Ganancia de recepción TCI por canal, aplicada al iniciar el servidor. | `0.5` | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia TX | Ganancia de transmisión TCI, aplicada al iniciar el servidor. | `0.5` | 0.0–1.0 | `TciTxGain` |

## Consejos

- Configure `TciPort` y los niveles de ganancia antes de habilitar el inicio automático. El inicio automático utiliza los valores que ya están guardados.
- El applet TCI Server está oculto de forma predeterminada. Actívelo con el botón `TCI` en la bandeja del sistema de la barra lateral derecha para verificar el estado del servidor tras el inicio.

## Solución de problemas

- **El elemento de menú `Autostart TCI with AetherSDR` no está visible** — La versión compilada no incluye soporte para WebSocket. TCI no está disponible en esta instalación.
- **El estado del servidor muestra `(port in use)` tras el inicio automático** — Otra aplicación ya está enlazada al puerto `TciPort`. Abra el applet TCI Server, cambie el valor del puerto a uno libre, guárdelo y reinicie la aplicación. Los valores fuera de rango vuelven automáticamente a `50001`.
- **El botón Enable aparece desactivado tras el inicio automático** — El servidor no pudo enlazarse al puerto. El interruptor vuelve automáticamente a desactivado y el estado muestra `(port in use)`. Cambie el puerto como se indica arriba.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia de recepción TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia de transmisión TCI](adjust-tci-tx-gain.md)
