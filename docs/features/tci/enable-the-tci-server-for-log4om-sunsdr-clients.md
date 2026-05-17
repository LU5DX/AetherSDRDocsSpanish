# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI ejecuta un servidor WebSocket que expone el control del radio y el audio a software de terceros como Log4OM y herramientas SunSDR. Actívelo para permitir que esos clientes se conecten a AetherSDR mediante el protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El servidor TCI requiere una conexión activa al radio.
- Decida en qué puerto escuchará el servidor. El valor predeterminado es `50001`. Si otra aplicación ya ocupa ese puerto, elija uno diferente en el rango 1024–65535.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha. Se abre el panel del applet del Servidor TCI.
2. Confirme que el campo **Port** muestra el puerto deseado. El valor predeterminado es `50001`. Para cambiarlo, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango se restablecen a `50001`.
3. Haga clic en **Enable**. El botón se vuelve verde cuando el servidor está en ejecución.
4. Verifique el indicador de estado a la izquierda de **Enable**. Muestra `:<puerto> (0 clients)` cuando el servidor está activo y en espera, y actualiza el conteo de clientes a medida que el software se conecta.

## Qué hace cada control

| Control                              | Predeterminado | Rango / Estados                                      |
|--------------------------------------|----------------|------------------------------------------------------|
| Campo de texto **Port**              | `50001`        | 1024–65535; valores inválidos se restablecen a `50001` |
| Interruptor **Enable**               | Off            | Off / On (verde)                                     |
| Medidor/deslizador de ganancia **RX1**–**RX4** | `0.5`          | 0.0–1.0                                              |
| Medidor/deslizador de ganancia **TX** | `0.5`          | 0.0–1.0                                              |
| Etiquetas de asignación de slice RX/TX | `—`            | `—` o `Slice <letra>` (puede mostrar formato HTML)   |
| Indicador de estado del servidor     | `(stopped)`    | `(stopped)`, `:<puerto> (N clients)`, `(port in use)` |

Las filas RX1–RX4 muestran qué slice impulsa cada canal TCI. La etiqueta indica `Slice A`, `Slice B`, etc., según la asignación del canal DAX de cada slice. La fila TX muestra el slice TX activo actualmente. Las etiquetas de slice ahora usan formato de texto enriquecido (`#2606`).

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se lance AetherSDR, vaya a `Settings > Autostart TCI with AetherSDR` y active ese elemento. Consulte [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md).
- El conteo de clientes en el indicador de estado se actualiza en tiempo real a medida que el software se conecta o desconecta.

## Solución de problemas

- **Enable vuelve a Off y el estado muestra `(port in use)`** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece `(stopped)` después de hacer clic en Enable** — Verifique que AetherSDR esté conectado al radio. El servidor TCI requiere una conexión activa al radio.

## Relacionados

- [Descripción general del Servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
