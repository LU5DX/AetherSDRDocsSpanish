# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI ejecuta un servidor WebSocket que expone el control de la radio y el audio a software de terceros como Log4OM y herramientas SunSDR. Habilítelo para permitir que esos clientes se conecten a AetherSDR mediante el protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El servidor TCI requiere una conexión activa con la radio.
- Decida en qué puerto escuchará el servidor. El valor predeterminado es `50001`. Si otra aplicación ya ocupa ese puerto, elija uno diferente en el rango 1024–65535.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha. Se abre el panel del applet del servidor TCI.
2. Confirme que el campo **Port** muestre el puerto deseado. El valor predeterminado es `50001`. Para cambiarlo, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango se restablecen a `50001`.
3. Haga clic en **Enable**. El botón se vuelve verde cuando el servidor está en ejecución.
4. Verifique el indicador de estado a la izquierda de **Enable**. Muestra `:<puerto> (0 clientes)` cuando el servidor está activo y en espera, y actualiza el conteo de clientes a medida que el software se conecta.

## Qué hace cada control

| Control                                    | Valor predeterminado | Rango / Estados                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo de texto **Port**                    | `50001`              | 1024–65535; los valores no válidos se restablecen a `50001`                                                                                                                                                                                                                                                                                                                                                                                                           |
| Interruptor **Enable**                     | Apagado              | Apagado / Encendido (verde)                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Medidor/deslizador de ganancia **RX1**–**RX4** | `0.5`                | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Medidor/deslizador de ganancia **TX**      | `0.5`                | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Etiquetas de asignación de slice RX/TX     | `—`                  | `—` o `Slice <letra>` (puede mostrar formato HTML)                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Indicador de estado del servidor           | `(detenido)`         | `(detenido)`, `:<puerto> (N clientes)`, `(puerto en uso)`                                                                                                                                                                                                                                                                                                                                                                                                             |
| Modo de desbordamiento TX (clic derecho)   | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Tres opciones: **Clip (0)** — Sujeta (clampa) los picos a ±1.0; valor predeterminado defensivo que introduce armónicos pero protege la conversión a int16 posterior. **NaN guard (1)** — Pasa las muestras sin modificar bit a bit; solo pone a cero los valores NaN/Inf patológicos; preserva la fidelidad tonal de los modos digitales. **Measure only (2)** — Nunca modifica las muestras; cuenta los picos para telemetría; la conversión a int16 posterior aún sujeta en la ruta DAX nativa de la radio. Se conserva como `TciTxOverflowMode`. |

Las filas RX1–RX4 muestran qué slice impulsa cada canal TCI. La etiqueta indica `Slice A`, `Slice B`, etc., según la asignación del canal DAX de cada slice. La fila TX muestra el slice TX activo actualmente. Las etiquetas de slice ahora usan formato de texto enriquecido (`#2606`).

El indicador de estado ahora usa colores adaptables al tema para una mejor visibilidad en temas de interfaz claros y oscuros (`v26.6.1`).

Los controles del medidor/deslizador de ganancia tienen nombres de accesibilidad configurados para compatibilidad con lectores de pantalla. Los controles RX se denominan "TCI RX 1 gain" hasta "TCI RX 4 gain", y el control TX se denomina "TCI TX gain".

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se inicie AetherSDR, vaya a `Settings > Autostart TCI with AetherSDR` y habilite ese elemento. Consulte [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md).
- El conteo de clientes en el indicador de estado se actualiza en tiempo real a medida que el software se conecta o desconecta.
- Use el menú de clic derecho en el medidor/deslizador de ganancia TX para seleccionar cómo se manejan las muestras fuera de rango de los clientes de modo digital. **Clip** es el valor predeterminado y protege contra una excitación excesiva; **NaN guard** y **Measure only** preservan la fidelidad tonal bit a bit de los modos digitales.

## Solución de problemas

- **Enable vuelve a apagarse y el estado muestra `(puerto en uso)`** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece `(detenido)` después de hacer clic en Enable** — Verifique que AetherSDR esté conectado a la radio. El servidor TCI requiere una conexión activa con la radio.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
