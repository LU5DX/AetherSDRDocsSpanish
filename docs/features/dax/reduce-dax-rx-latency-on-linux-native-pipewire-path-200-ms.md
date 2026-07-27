# Applet de Audio DAX

El applet de Audio DAX proporciona el puente de audio digital entre su radio FLEX-8600 y el sistema de audio de su computadora. Muestra medidores de recepción por canal y deslizadores de ganancia para los canales DAX 1–4, además de un medidor de transmisión único, con un interruptor maestro de Habilitación.

## Antes de comenzar

- AetherSDR v26.7.4 o posterior instalado.
- Una radio FLEX-8600 conectada (DAX requiere una conexión activa con la radio).
- Al menos un slice asignado a un canal DAX en la radio.

## Soporte de plataforma

| Plataforma | Controlador DAX | Notas |
|---|---|---|
| Linux | Incorporado (fuente PipeWire `pw_stream`) | Ruta nativa de PipeWire desde v0.9.7, latencia de ~200 ms. Sin respaldo de PulseAudio. |
| macOS | Incorporado | Incluido como parte de AetherSDR. |
| Windows | **No incluido con AetherSDR** | El botón de Habilitar DAX y todos los medidores están inactivos en Windows. Use los controladores SmartSDR DAX de FlexRadio o TCI. |

En Windows, el applet de Audio DAX solo muestra un aviso: *"No hay controlador DAX incorporado en Windows. Use TCI o SmartSDR DAX."* No se construyen controles ni se actualizan los medidores. Para instrucciones de configuración en Windows, consulte **Help > Configuring Data Modes**.

## Cómo usar (Linux / macOS)

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet de Audio DAX.
2. Haga clic en **Enable** para iniciar el puente de audio DAX. El botón se vuelve verde y muestra "Enabled" cuando está activo.
3. Confirme que la configuración `AutoStartDAX` esté guardada: el botón Enable permanece marcado y muestra "Enabled" después de volver a abrir el applet.
4. En su software de modos digitales (WSJT-X, fldigi o similar), seleccione la fuente de audio correspondiente al canal DAX que asignó.

En Linux, el audio llega con una latencia de aproximadamente 200 ms en lugar de ~400 ms. No se requiere configuración adicional; la ruta de PipeWire se usa automáticamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|
| DAX Enable | Apagado | Encendido / Apagado | `AutoStartDAX` | Interruptor maestro. Inicia todos los flujos de RX y TX de DAX. Debe estar encendido para que fluya el audio. El texto del botón cambia a "Enabled" cuando está encendido, a "Disabled" cuando está apagado. |
| Ganancia+medidor DAX 1 | 0.5 | 0.0 – 1.0 | `DaxRxGain1` | Medidor de nivel y deslizador de ganancia combinados para el canal DAX 1. Arrastre para ajustar la ganancia de RX. |
| Ganancia+medidor DAX 2 | 0.5 | 0.0 – 1.0 | `DaxRxGain2` | Medidor de nivel y deslizador de ganancia combinados para el canal DAX 2. |
| Ganancia+medidor DAX 3 | 0.5 | 0.0 – 1.0 | `DaxRxGain3` | Medidor de nivel y deslizador de ganancia combinados para el canal DAX 3. |
| Ganancia+medidor DAX 4 | 0.5 | 0.0 – 1.0 | `DaxRxGain4` | Medidor de nivel y deslizador de ganancia combinados para el canal DAX 4. |
| Ganancia+medidor TX | 0.5 | 0.0 – 1.0 | `DaxTxGain` | Medidor de nivel y deslizador de ganancia combinados para el flujo TX de DAX. |
| Estado de asignación de slice (por canal) | — | — o Slice A–H | *(ninguna)* | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX. |

## Consejos

- Si las barras del medidor en DAX 1–4 no se mueven después de hacer clic en **Enable**, verifique que el indicador de estado de asignación de slice muestre una letra de slice en lugar de —. Un — significa que ningún slice está enrutado actualmente a ese canal; asigne el slice al canal DAX desde los controles de slice de la radio.
- Para que DAX se inicie automáticamente en cada arranque, marque **Settings > Autostart DAX with AetherSDR**. Esto establece `AutoStartDAX` en True sin necesidad de hacer clic en Enable manualmente cada sesión.
- El medidor de nivel usa un ataque rápido (α = 0.4) y una caída lenta (α = 0.08). Una breve ausencia de señal no borrará el medidor de inmediato.

## Solución de problemas

- **El botón Enable aparece atenuado o no responde** — En Windows, este comportamiento es esperado (consulte Soporte de plataforma arriba). En Linux y macOS, DAX requiere una conexión activa a la radio. Conéctese a la FLEX-8600 primero mediante **Settings > Connect to Radio...**, luego haga clic en Enable.
- **La latencia sigue siendo de ~400 ms después de la actualización** — Verifique que PipeWire sea el servidor de audio activo en su sistema Linux. Si su sistema aún usa PulseAudio sin PipeWire, la ruta nativa de PipeWire no está disponible y la latencia se mantendrá en el valor más alto.
- **Sin audio desde la fuente DAX en WSJT-X o fldigi** — Confirme que Enable esté marcado (muestra "Enabled") en el applet DAX y que el indicador de asignación de slice para el canal relevante muestre una letra de slice, no —.
- **En Windows, ¿qué controlador DAX debo usar?** — Use los controladores oficiales SmartSDR DAX de FlexRadio, o configure su software digital para usar TCI en lugar de audio DAX.

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Establecer ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ver qué slice está usando cada canal DAX actualmente](see-which-slice-is-currently-using-each-dax-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
