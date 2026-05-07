# Referencia Completa de Claves de AppSettings

Esta página enumera todas las claves de AppSettings persistentes en AetherSDR, el control de interfaz o elemento de menú que las escribe, y dónde encontrar ese control. Úsela al solucionar problemas de archivos de configuración, crear scripts para despliegues, o comprender qué hace una configuración detrás de la etiqueta del menú.

## Antes de comenzar

- No se requiere conexión a una radio para leer o comprender estas configuraciones.
- Las configuraciones se guardan localmente en su máquina. Cambiar un perfil de radio en la propia radio no altera estas claves.

## Qué hace cada control

La tabla siguiente cubre cada clave presente en el catálogo proporcionado. Las claves están ordenadas por el menú o diálogo donde aparecen.

### Menú Settings

| Clave AppSettings | Elemento de menú / control | Qué hace | Notas |
|---|---|---|---|
| `AutoStartRigctld` | `Settings > Autostart rigctld with AetherSDR` | Al marcarlo, inicia el servidor CAT rigctld automáticamente cada vez que se lanza AetherSDR. | — |
| `AutoStartCAT` | `Settings > Autostart CAT with AetherSDR` | Al marcarlo, crea puertos serie virtuales para control CAT al iniciar. | Solo Linux y macOS. |
| `AutoStartTCI` | `Settings > Autostart TCI with AetherSDR` | Al marcarlo, inicia el servidor TCI automáticamente al iniciar. | Requiere compilación con WebSockets. |
| `AutoStartDAX` | `Settings > Autostart DAX with AetherSDR` | Al marcarlo, habilita el puente de audio DAX al iniciar. | Solo macOS y PipeWire. |

### Menú View

Los elementos del menú View listados a continuación guardan su estado como preferencias persistentes. Los nombres de clave AppSettings específicos para los elementos de View no están confirmados en el catálogo proporcionado; no asuma nombres de clave para estos controles. Consulte el menú directamente en `View` para su estado actual.

| Control | Elemento de menú | Qué hace |
|---|---|---|
| Visibilidad del panel de applets | `View > Applet Panel` | Activa o desactiva el panel de applets del lado derecho. |
| Panel de applets flotante | `View > Pop Out Applet Panel` | Flota el panel de applets en una ventana separada o lo acopla de nuevo. Atajo: Ctrl+Shift+S. |
| Sintonización con un clic | `View > Single-Click to Tune` | Al activarlo, un solo clic en el panadapter reajusta el VFO. El valor predeterminado es doble clic. |
| Seguimiento del panadapter | `View > Pan Follows VFO` | Al activarlo, el panadapter se desplaza para mantener el VFO visible. Activado por defecto. |
| Modo mínimo | `View > Minimal Mode` | Oculta la barra de título y los controles para maximizar el área del panadapter. Atajo: Ctrl+M. |
| Ventana sin marco | `View > Frameless Window` | Oculta la decoración de ventana del sistema operativo. Atajo: Ctrl+Shift+F. |
| Superposición de propagación | `View > Propagation Conditions` | Muestra una superposición de pronóstico de propagación ionosférica en tiempo real sobre los panadapters. |
| Atajos de teclado activos | `View > Keyboard Shortcuts` | Activa o desactiva el procesamiento global de atajos de teclado. |
| Parpadeo del indicador de estado | `View > Blink Status Indicator` | El indicador de la barra de título parpadea para señalar el latido de la radio. Activado por defecto. |
| Escala de la interfaz | `View > UI Scale` | Establece la escala de la interfaz de usuario de la aplicación. Opciones: 75%, 85%, 100%, 110%, 125%, 150%, 175%, 200%. |
| Visualización del plan de bandas | `View > Band Plan` | Controla el tamaño de la superposición del plan de bandas. Opciones: Off, Small (6 pt), Medium (10 pt), Large (12 pt), Huge (16 pt), más selector de región. |

## Consejos

- Las cuatro claves `AutoStart*` son las configuraciones más comúnmente usadas en scripts. Le permiten controlar qué servidores acompañantes se inician con AetherSDR sin abrir ningún diálogo.
- `AutoStartCAT` aplica solo en Linux y macOS. En Windows, use `AutoStartRigctld` para la integración CAT a través de rigctld.
- `AutoStartTCI` solo está presente si AetherSDR fue compilado con soporte WebSocket. Si el elemento de menú `Settings > Autostart TCI with AetherSDR` está ausente, la clave no tiene efecto incluso si se establece manualmente.

## Solución de problemas

- **Un servidor acompañante (rigctld, TCI, DAX) no se inicia al lanzar** — Verifique que la clave `AutoStart*` correspondiente esté establecida confirmando que la marca de verificación esté presente en el menú `Settings`. Si el elemento de menú falta por completo, su compilación de AetherSDR no incluye soporte para esa función.
- **`AutoStartCAT` no tiene efecto en Windows** — El CAT por puerto serie virtual no es compatible con Windows. Use `Settings > Autostart rigctld with AetherSDR` (`AutoStartRigctld`) en su lugar.
- **La escala de la interfaz o el diseño del panel se reinician después de una actualización** — Estas preferencias se almacenan localmente. Si el archivo de configuración se elimina o corrompe, todas las preferencias de View vuelven a los valores predeterminados. Reconflgúrelas desde el menú `View`.
