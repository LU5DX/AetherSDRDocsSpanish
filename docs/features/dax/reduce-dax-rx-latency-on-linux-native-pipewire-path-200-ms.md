# Applet de Audio DAX

El applet de Audio DAX proporciona el puente de audio digital entre su radio FLEX-8600 y el sistema de audio de su computadora. Muestra medidores RX por canal y deslizadores de ganancia para los canales DAX 1–8, además de un medidor TX único, con un interruptor maestro de Habilitar.

## Antes de comenzar

- Tener instalado AetherSDR v26.8.4 o posterior.
- Una radio FLEX-8600 conectada (DAX requiere una conexión de radio activa).
- Al menos un slice asignado a un canal DAX en la radio.

Las filas que superan la capacidad de slices de la radio conectada están ocultas, por lo que una radio con menos slices (por ejemplo, un modelo de 2 o 4 slices) no muestra deslizadores de ganancia inactivos.

## Soporte de plataformas

| Plataforma | Controlador DAX | Notas |
|---|---|---|
| Linux | Integrado (fuente PipeWire `pw_stream`) | Ruta nativa de PipeWire desde v0.9.7, ~200 ms de latencia. Sin respaldo de PulseAudio. |
| macOS | Integrado | Incluido como parte de AetherSDR. |
| Windows | **No incluido con AetherSDR** | El botón Habilitar DAX y todos los medidores están inactivos en Windows. Use los controladores DAX SmartSDR de FlexRadio o TCI. |

En Windows, el applet de Audio DAX muestra solo un aviso: *"No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX."* No se construyen controles ni se actualizan medidores. Para instrucciones de configuración en Windows, consulte **Help > Configuring Data Modes**.

## Cómo usar (Linux / macOS)

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en **Enable** para iniciar el puente de audio DAX. El botón se vuelve verde y muestra "Enabled" cuando está activo.
3. Confirme que la configuración `AutoStartDAX` esté guardada: el botón Habilitar permanece marcado y muestra "Enabled" después de volver a abrir el applet.
4. En su software de modos digitales (WSJT-X, fldigi o similar), seleccione la fuente de audio correspondiente al canal DAX que asignó.

En Linux, el audio llega con aproximadamente 200 ms de latencia en lugar de ~400 ms. No se requiere configuración adicional; la ruta de PipeWire se usa automáticamente.

## Qué hace cada control

| Control                               | Predeterminado                                                                                                          | Rango válido                                                                                                                          |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| DAX Enable                            | Inicia el puente de audio DAX; emite daxToggled.                                                                           | La etiqueta del botón es 'Enable'/'Disabled'; interruptor maestro para todas las transmisiones RX y TX de DAX. No se construye en Windows (#4112).                      |
| DAX 1 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                            |
| DAX 2 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                            |
| DAX 3 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                            |
| DAX 4 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                            |
| DAX 5 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0. Visible solo cuando la radio conectada admite al menos 5 slices.                                                         |
| DAX 6 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0. Visible solo cuando la radio conectada admite al menos 6 slices.                                                         |
| DAX 7 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0. Visible solo cuando la radio conectada admite al menos 7 slices.                                                         |
| DAX 8 ganancia+medidor                | 0.5                                                                                                                      | 0.0 – 1.0. Visible solo en una radio con capacidad de 8 slices.                                                                                 |
| TX ganancia+medidor                   | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                            |
| Estado de asignación de slice (por canal) | Muestra qué slice está enrutado actualmente a cada canal DAX.                                                               | Las letras de slice se muestran como identificadores de texto enriquecido.                                                                                       |
| Nota de Windows                       | En las versiones de Windows, el applet muestra solo la nota 'No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.' (#4112). | Windows no tiene puente DAX integrado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus asignadores están protegidos contra nulos. |

## Consejos

- Si las barras de medidor en DAX 1–8 no se mueven después de hacer clic en **Enable**, verifique que el indicador de estado de asignación de slice muestre una letra de slice en lugar de —. Un — significa que ningún slice está enrutado actualmente a ese canal; asigne el slice al canal DAX desde los controles de slice de la radio.
- Para que DAX se inicie automáticamente en cada ejecución, marque **Settings > Autostart DAX with AetherSDR**. Esto establece `AutoStartDAX` en True sin necesidad de hacer clic en Enable manualmente cada sesión.
- El medidor de nivel utiliza ataque rápido (α = 0.4) y caída lenta (α = 0.08). Una breve ausencia de señal no dejará el medidor en blanco de inmediato.

## Solución de problemas

- **El botón Enable está atenuado o no responde** — En Windows, este es un comportamiento esperado (consulte Soporte de plataformas arriba). En Linux y macOS, DAX requiere una conexión de radio activa. Conéctese primero a la FLEX-8600 mediante **Settings > Connect to Radio...**, luego haga clic en Enable.
- **La latencia sigue siendo ~400 ms después de actualizar** — Verifique que PipeWire sea el servidor de audio activo en su sistema Linux. Si su sistema aún usa PulseAudio sin PipeWire, la ruta nativa de PipeWire no está disponible y la latencia permanecerá en el valor más alto.
- **Sin audio desde la fuente DAX en WSJT-X o fldigi** — Confirme que Enable esté marcado (muestra "Enabled") en el applet DAX y que el indicador de asignación de slice para el canal correspondiente muestre una letra de slice, no —.
- **En Windows, ¿qué controlador DAX debo usar?** — Use los controladores DAX SmartSDR oficiales de FlexRadio, o configure su software digital para usar TCI en lugar de audio DAX.

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Inicio automático de DAX al iniciar](autostart-dax-on-launch.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configurar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
