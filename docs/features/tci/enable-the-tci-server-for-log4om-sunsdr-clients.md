# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI ejecuta un servidor WebSocket que expone el control del radio y el audio a software de terceros como Log4OM y herramientas SunSDR. Habilítelo para permitir que esos clientes se conecten a AetherSDR a través del protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El servidor TCI requiere una conexión activa con el radio.
- Decida en qué puerto escuchará el servidor. El valor predeterminado es `50001`. Si otra aplicación ya ocupa ese puerto, elija uno diferente en el rango 1024–65535.

## Pasos

1. Haga clic en el botón **TCI** en la barra lateral derecha. Se abre el panel del applet del Servidor TCI.
2. Confirme que el campo **Port** muestra el puerto deseado. El valor predeterminado es `50001`. Para cambiarlo, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango se restablecen automáticamente a `50001`.
3. Haga clic en **Enable** (o **Disabled**). La etiqueta del botón cambia a **Enabled** cuando el servidor está en ejecución y el botón se vuelve verde. Si la etiqueta del botón muestra **Disabled**, el servidor está detenido.
4. Revise el indicador de estado a la izquierda del botón Enable. Muestra `:<port> (0 clients)` cuando el servidor está activo y esperando, y actualiza el número de clientes a medida que el software se conecta.

## Qué hace cada control

| Control                           | Predeterminado                                                                                                                         | Rango / Estados                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo de texto **Port**           | `50001`                                                                                                                                | 1024–65535; los valores inválidos se restablecen a `50001`                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Alternar **Enable**               | Desactivado (la etiqueta muestra **Disabled**), o Activado si Autostart TCI está habilitado (la etiqueta muestra **Enabled**)           | Desactivado / Activado — la etiqueta se actualiza a **Enabled** o **Disabled**                                                                                                                                                                                                                                                                                                                                                                                            |
| Medidor/deslizador de ganancia **RX1**–**RX4** | `0.5`                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Medidor/deslizador de ganancia **TX**          | `0.5`                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Etiquetas de asignación de slice RX/TX         | `—`                                                                                                                    | `—` o `Slice <letter>` (puede mostrar formato HTML)                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Indicador de estado del servidor   | `(stopped)`                                                                                                                            | `(stopped)`, `:<port> (N clients)`, `(port in use)`                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Tres opciones: **Clip (0)** — Limita forzosamente los excesos a ±1.0; valor predeterminado defensivo que introduce armónicos pero protege la conversión posterior a int16. **NaN guard (1)** — Pasa las muestras sin cambios; solo pone a cero valores NaN/Inf patológicos; preserva la fidelidad tonal de los modos digitales. **Measure only (2)** — Nunca modifica las muestras; cuenta los excesos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa del radio. Se conserva como `TciTxOverflowMode`. |

Las filas RX1–RX4 muestran qué slice impulsa cada canal TCI. La etiqueta muestra `Slice A`, `Slice B`, etc., según la asignación del canal DAX de cada slice. La fila TX muestra el slice TX activo actualmente. Las etiquetas de los slices ahora utilizan formato de texto enriquecido (`#2606`).

El indicador de estado ahora utiliza colores adaptables al tema para una mejor visibilidad en temas de interfaz claros y oscuros (`v26.6.1`).

Los controles de medidor/deslizador de ganancia tienen nombres de accesibilidad configurados para compatibilidad con lectores de pantalla. Los controles RX se denominan "TCI RX 1 gain" hasta "TCI RX 4 gain", y el control TX se denomina "TCI TX gain".

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se inicie AetherSDR, vaya a `Settings > Autostart TCI with AetherSDR` y habilite esa opción. Cuando está habilitada, el botón Enable comienza con la etiqueta **Enabled** y el servidor se ejecuta de inmediato. Consulte [Autostart TCI on launch](autostart-tci-on-launch.md).
- El número de clientes en el indicador de estado se actualiza en tiempo real a medida que el software se conecta o desconecta.
- Use el menú contextual (clic derecho) en el medidor/deslizador de ganancia TX para seleccionar cómo se manejan las muestras fuera de rango de los clientes de modos digitales. **Clip** es el valor predeterminado y protege contra la excitación excesiva; **NaN guard** y **Measure only** preservan la fidelidad tonal bit-exacta de los modos digitales.

## Solución de problemas

- **Enable se desactiva y el estado muestra `(port in use)`** — Otra aplicación ya está usando ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — Verifique que AetherSDR esté conectado al radio. El servidor TCI requiere una conexión activa con el radio.

## Relacionados

- [TCI Server overview](overview.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Autostart TCI on launch](autostart-tci-on-launch.md)
- [See how many TCI clients are connected](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
