# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI ejecuta un servidor WebSocket que expone el control de radio y el audio a software de terceros, como Log4OM y las herramientas de SunSDR. Habilítelo para permitir que esos clientes se conecten a AetherSDR mediante el protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El servidor TCI requiere una conexión de radio activa.
- Decida en qué puerto escuchará el servidor. El valor predeterminado es `50001`. Si otra aplicación ya ocupa ese puerto, elija uno diferente en el rango 1024–65535.

## Pasos

1. Haga clic en el botón de bandeja **TCI** de la barra lateral derecha. Se abre el panel del applet TCI Server.
2. Confirme que el campo **Port** muestra el puerto que desea utilizar. El valor predeterminado es `50001`. Para cambiarlo, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango vuelven automáticamente a `50001`.
3. Haga clic en **Enable**. El botón se vuelve verde cuando el servidor está en ejecución.
4. Revise el indicador de estado a la izquierda de **Enable**. Muestra `:<port> (0 clients)` cuando el servidor está activo y en espera, y actualiza el recuento de clientes a medida que el software se conecta.

## Qué hace cada control

| Control | Valor predeterminado | Rango / Estados | Clave persistida |
|---|---|---|---|
| Campo de texto **Port** | `50001` | 1024–65535; los valores no válidos vuelven a `50001` | `TciPort` |
| Interruptor **Enable** | Desactivado | Desactivado / Activado (verde) | — |
| Medidor/deslizador de ganancia **RX1**–**RX4** | `0.5` | 0.0–1.0 | `TciRxGain1`–`TciRxGain4` |
| Medidor/deslizador de ganancia **TX** | `0.5` | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | `—` | `—` o `Slice <letra>` | — |
| Indicador de estado del servidor | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — |

Las filas RX1–RX4 muestran qué slice controla cada canal TCI. La etiqueta indica `Slice A`, `Slice B`, etc., según la asignación de canal DAX de cada slice. La fila TX muestra el slice TX actualmente activo.

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que AetherSDR se inicia, vaya a `Settings > Autostart TCI with AetherSDR` y habilite ese elemento. Consulte [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md).
- El recuento de clientes en el indicador de estado se actualiza en tiempo real a medida que el software se conecta o desconecta.

## Solución de problemas

- **Enable vuelve a desactivarse y el estado muestra `(port in use)`** — Otra aplicación ya está enlazada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — Verifique que AetherSDR esté conectado a la radio. El servidor TCI requiere una conexión de radio activa.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
