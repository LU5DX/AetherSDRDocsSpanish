# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet Waveform ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar entre modos le permite elegir la representación que mejor se adapte a su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la pantalla de forma de onda sin controles debajo, haga doble clic en la pantalla de forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la pantalla de forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**. El cuadro combinado tiene un nombre accesible de "WAVE view mode".
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La pantalla se actualiza inmediatamente. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el siguiente inicio.

## Qué hace cada control

| Control                   | Valor predeterminado | Valores válidos                                        |
|---------------------------|----------------------|--------------------------------------------------------|
| Cuadro combinado **View:**| Scope                | Scope, Envelope, History, Bands                        |
| Deslizador **Window:**    | 200 ms               | 10–500 ms                                              |
| Deslizador **Zoom:**      | 1.7x                 | 1.0x – 6.0x (100–600)                                 |
| Deslizador **FPS:**       | 25 fps               | 5–60 Hz                                                |

## Controles del cajón de configuración

Todos los controles se encuentran en el cajón de configuración plegable debajo de la pantalla de forma de onda. Cada control tiene un nombre accesible para compatibilidad con lectores de pantalla:

| Control                   | Nombre accesible   | Clave de configuración                | Comportamiento                                                       |
|---------------------------|---------------------|---------------------------------------|----------------------------------------------------------------------|
| Cuadro combinado **View:**| WAVE view mode      | `WaveApplet_ViewMode`                 | Se conserva como 'Graph', 'Envelope', 'History' o 'Bands'            |
| Deslizador **Zoom:**      | WAVE zoom           | `WaveApplet_ZoomPercent`              | Escala el eje de amplitud; predeterminado 170 (1.7x)                 |
| Deslizador **FPS:**       | WAVE FPS            | `WaveApplet_RefreshRateHz`            | Controla la velocidad de redibujado; predeterminado 25 fps, rango 5–60 Hz |
| Deslizador **Window:**    | WAVE window         | `WaveApplet_TimeWindowMs`             | Ventana de tiempo mostrada; predeterminado 200 ms, rango 10–500 ms   |

**Nota:** La clave heredada `WaveApplet_TimeWindowSec` se migra a `WaveApplet_TimeWindowMs` en el primer inicio. El estado plegado del cajón se conserva entre reinicios de la aplicación usando `WaveApplet_DrawerExpanded`.

## Consejos

- El modo **Bands** usa un filtro Goertzel para derivar barras de bandas de frecuencia. Es útil para verificar si la energía de audio de TX se distribuye en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la pantalla muestra un mensaje de **"no RX audio"** o **"no TX audio"**, no han llegado muestras de alcance en el último segundo. Para la ruta de RX, habilite PC Audio en la configuración de la radio. Para la ruta de TX, verifique que el micrófono o la entrada de línea estén activos. La configuración del modo de visualización aún se aplica y tendrá efecto tan pronto como se reanude el audio.
- Un solo clic en la pantalla de forma de onda alterna la pausa. Si la pantalla parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.
- El estado del cajón de configuración (abierto o cerrado) se conserva. Si cierra el cajón y reinicia AetherSDR, permanece cerrado. Haga doble clic en la forma de onda para volver a abrirlo.
- La ruta de audio de TX se tiñe con un color cálido y la ruta de RX con un color frío, para que pueda identificar la dirección activa de un vistazo sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.
- Cuando ocurre recorte (muestras en o por encima de ±0.98 de escala completa), las columnas afectadas se resaltan en rojo y aparece un contador **CLIP N** en el encabezado.
- Los FPS predeterminados se cambiaron de 24 a 25 fps en v26.7.4 para coincidir con la tasa típica del panadapter de la radio. Los usuarios que guardaron previamente un valor de FPS explícito conservan su configuración — el nuevo valor predeterminado solo se aplica cuando no se ha guardado ninguna configuración de FPS.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la pantalla de forma de onda para abrirlo.
- **El modo seleccionado no se conserva después de reiniciar** — Confirme que AetherSDR tiene acceso de escritura a su almacenamiento de configuración. Si el problema persiste, verifique que ninguna otra instancia de AetherSDR se esté ejecutando simultáneamente y sobrescribiendo `WaveApplet_ViewMode` al salir.
- **La pantalla muestra un mensaje de marcador de posición en lugar de una forma de onda** — No han llegado muestras de alcance en el último segundo. Verifique que la fuente de audio esté activa. Para la ruta de RX, asegúrese de que PC Audio esté habilitado en la configuración de la radio. Para la ruta de TX, confirme que el micrófono o la entrada de línea estén activos.
- **La pantalla de forma de onda parece congelada** — La pantalla puede estar en pausa. Haga un solo clic en la forma de onda para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Establecer la velocidad de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Establecer la ventana de tiempo de la forma de onda
