# Referencia completa de claves AppSettings

Esta página lista todas las claves AppSettings persistidas en AetherSDR, el control de interfaz o elemento de menú que las escribe, y dónde encontrar dicho control. Úsela para solucionar problemas con archivos de configuración, automatizar despliegues o entender qué hace un ajuste detrás de la etiqueta de menú.

## Antes de comenzar

- No se requiere conexión a una radio para leer o comprender estos ajustes.
- Los ajustes se almacenan localmente en su equipo. Cambiar un perfil de radio en la propia radio no modifica estas claves.

## Qué hace cada control

La tabla a continuación cubre todas las claves disponibles en el catálogo suministrado. Las claves están ordenadas por el menú o diálogo donde aparecen.

### Menú Settings

| Clave AppSettings | Elemento de menú / control | Qué hace | Notas |
|---|---|---|---|
| `AutoStartRigctld` | `Settings > Autostart rigctld with AetherSDR` | Cuando está activado, inicia automáticamente el servidor CAT rigctld cada vez que se lanza AetherSDR. | — |
| `AutoStartCAT` | `Settings > Autostart CAT with AetherSDR` | Cuando está activado, crea puertos serie virtuales para control CAT al iniciar. | Solo en Linux y macOS. |
| `AutoStartTCI` | `Settings > Autostart TCI with AetherSDR` | Cuando está activado, inicia el servidor TCI automáticamente al lanzar la aplicación. | Requiere compilación con WebSockets. |
| `AutoStartDAX` | `Settings > Autostart DAX with AetherSDR` | Cuando está activado, habilita el puente de audio DAX al iniciar. | Solo en macOS y PipeWire. |

### Menú View

Los elementos del menú View que se listan a continuación guardan su estado como preferencias persistidas. Los nombres específicos de clave AppSettings para los elementos de View no están confirmados en el catálogo suministrado; no asuma nombres de clave para estos controles. Consulte directamente el menú `View` para conocer su estado actual.

| Control | Elemento de menú | Qué hace |
|---|---|---|
| Visibilidad del panel de applets | `View > Applet Panel` | Activa o desactiva el panel de applets del lado derecho. |
| Panel de applets flotante | `View > Pop Out Applet Panel` | Hace flotar el panel de applets en una ventana separada o lo vuelve a anclar. Atajo: Ctrl+Shift+S. |
| Sintonía con un clic | `View > Single-Click to Tune` | Cuando está habilitado, un solo clic en el panadapter (visor panorámico) resintoniza el VFO. Por defecto se usa doble clic. |
| Seguimiento del panadapter | `View > Pan Follows VFO` | Cuando está habilitado, el panadapter se desplaza para mantener el VFO visible. Activado por defecto. |
| Modo mínimo | `View > Minimal Mode` | Oculta la barra de título y los controles para maximizar el área del panadapter. Atajo: Ctrl+M. |
| Ventana sin marco | `View > Frameless Window` | Oculta la decoración de ventana del sistema operativo. Atajo: Ctrl+Shift+F. |
| Superposición de propagación | `View > Propagation Conditions` | Muestra una superposición en tiempo real del pronóstico de propagación ionosférica sobre los panadapters. |
| Atajos de teclado activos | `View > Keyboard Shortcuts` | Habilita o deshabilita el procesamiento de atajos de teclado de forma global. |
| Parpadeo del indicador de estado | `View > Blink Status Indicator` | El indicador de la barra de título parpadea para señalar el latido de la radio. Activado por defecto. |
| Escala de interfaz | `View > UI Scale` | Establece la escala de la interfaz de la aplicación. Opciones: 75%, 85%, 100%, 110%, 125%, 150%, 175%, 200%. |
| Visualización del plan de banda | `View > Band Plan` | Controla el tamaño de la superposición del plan de banda. Opciones: Off, Small (6 pt), Medium (10 pt), Large (12 pt), Huge (16 pt), más selector de región. |

## Consejos

- Las cuatro claves `AutoStart*` son los ajustes más utilizados en automatizaciones. Permiten controlar qué servidores complementarios se inician junto con AetherSDR sin abrir ningún diálogo.
- `AutoStartCAT` aplica únicamente en Linux y macOS. En Windows, use `AutoStartRigctld` para la integración CAT mediante rigctld.
- `AutoStartTCI` solo está presente si AetherSDR fue compilado con soporte para WebSocket. Si el elemento de menú `Settings > Autostart TCI with AetherSDR` no aparece, la clave no tiene efecto aunque se establezca manualmente.

## Solución de problemas

- **Un servidor complementario (rigctld, TCI, DAX) no inicia al lanzar la aplicación** — Verifique que la clave `AutoStart*` correspondiente esté activada comprobando que la marca de verificación esté presente en el menú `Settings`. Si el elemento de menú no aparece, su compilación de AetherSDR no incluye soporte para esa función.
- **`AutoStartCAT` no tiene efecto en Windows** — El control CAT mediante puertos serie virtuales no es compatible con Windows. Use `Settings > Autostart rigctld with AetherSDR` (`AutoStartRigctld`) en su lugar.
- **La escala de interfaz o la distribución del panel se restablece tras una actualización** — Estas preferencias se almacenan localmente. Si el archivo de ajustes se elimina o se corrompe, todas las preferencias de View vuelven a sus valores predeterminados. Reconfigúrelas desde el menú `View`.
