# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI ejecuta un servidor WebSocket que expone el control de la radio y el audio a software de terceros como Log4OM y las herramientas SunSDR. Habilítelo para permitir que esos clientes se conecten a AetherSDR mediante el protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El servidor TCI requiere una conexión de radio activa.
- Decida en qué puerto escuchará el servidor. El valor predeterminado es `50001`. Si otra aplicación ya ocupa ese puerto, elija uno diferente en el rango 1024–65535.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha. Se abre el panel del applet TCI Server.
2. Confirme que el campo **Port** muestra el puerto deseado. El valor predeterminado es `50001`. Para cambiarlo, haga clic en el campo, escriba un nuevo valor (1024–65535) y presione Enter. Los valores fuera de ese rango vuelven automáticamente a `50001`.
3. Haga clic en **Enable** (o **Disabled**). La etiqueta del botón cambia a **Enabled** cuando el servidor está en ejecución y el botón se vuelve verde. Si la etiqueta del botón muestra **Disabled**, el servidor está detenido.
4. Revise el indicador de estado a la izquierda del botón Enable. Muestra `:<puerto> (0 clients)` cuando el servidor está activo y en espera, y actualiza el número de clientes a medida que el software se conecta.

## Qué hace cada control

| Control                           | Predeterminado                                                                                                                                | Rango / Estados                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo de texto **Port**           | `50001`                                                                                                                                | 1024–65535; los valores no válidos vuelven a `50001`                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Conmutador **Enable**             | Desactivado (la etiqueta muestra **Disabled**), o Activado si Autostart TCI está habilitado (la etiqueta muestra **Enabled**)          | Desactivado / Activado — la etiqueta se actualiza a **Enabled** o **Disabled**                                                                                                                                                                                                                                                                                                                                                                                              |
| Medidor/deslizador de ganancia **RX1**–**RX8** | `0.5`                                                                                                                                | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Medidor/deslizador de ganancia **TX**          | `0.5`                                                                                                                                | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Etiquetas de asignación de slice RX/TX         | `—`                                                                                                                                    | `—` o `Slice <letra>` (puede mostrar formato HTML)                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Indicador de estado del servidor               | `(stopped)`                                                                                                                            | `(stopped)`, `:<puerto> (N clients)`, `(port in use)`                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Modo de desbordamiento TX (clic derecho)       | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Tres opciones: **Clip (0)** — Recorta los excesos a ±1.0; valor predeterminado defensivo que introduce armónicos pero protege la conversión posterior a int16. **NaN guard (1)** — Pasa las muestras bit a bit sin cambios; solo pone a cero los valores patológicos NaN/Inf; preserva la fidelidad tonal de los modos digitales. **Measure only (2)** — Nunca modifica las muestras; cuenta los excesos para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio. Se guarda como `TciTxOverflowMode`. |

Las filas RX1–RX8 muestran qué slice impulsa cada canal TCI. La etiqueta muestra `Slice A`, `Slice B`, y así sucesivamente, según la asignación del canal DAX de cada slice. La fila TX muestra el slice TX activo actualmente. Las etiquetas de slice ahora usan formato de texto enriquecido (`#2606`).

En radios con menos de ocho slices, las filas RX adicionales se ocultan para coincidir con la capacidad de slices de la radio. Por ejemplo, una FLEX-6400 muestra solo las filas RX1–RX2, mientras que una FLEX-8600 muestra las ocho.

El indicador de estado ahora usa colores compatibles con el tema para una mejor visibilidad en temas de interfaz claros y oscuros (`v26.6.1`).

Los controles de medidor/deslizador de ganancia tienen nombres de accesibilidad configurados para compatibilidad con lectores de pantalla. Los controles RX se denominan "TCI RX 1 gain" hasta "TCI RX 8 gain", y el control TX se denomina "TCI TX gain".

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se lance AetherSDR, vaya a `Settings > Autostart TCI with AetherSDR` y habilite ese elemento. Cuando esté habilitado, el botón Enable comienza con la etiqueta **Enabled** y el servidor se ejecuta de inmediato. Consulte [Autostart TCI on launch](autostart-tci-on-launch.md).
- El número de clientes en el indicador de estado se actualiza en tiempo real a medida que el software se conecta o desconecta.
- Use el menú de clic derecho en el medidor/deslizador de ganancia TX para seleccionar cómo se manejan las muestras fuera de rango de los clientes de modos digitales. **Clip** es el valor predeterminado y protege contra un nivel de excitación excesivo; **NaN guard** y **Measure only** preservan la fidelidad tonal bit a bit de los modos digitales.

## Solución de problemas

- **Enable vuelve a desactivarse y el estado muestra `(port in use)`** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — Verifique que AetherSDR esté conectado a la radio. El servidor TCI requiere una conexión de radio activa.
- **Faltan algunas filas RX** — El applet TCI muestra solo tantas filas RX como slices tenga la radio. Esto es normal; las filas se ocultan en radios con menos ranuras de slice.

## Relacionado

- [TCI Server overview](overview.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Autostart TCI on launch](autostart-tci-on-launch.md)
- [See how many TCI clients are connected](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
