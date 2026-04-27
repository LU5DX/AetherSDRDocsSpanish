# Pausar y limpiar la pantalla de forma de onda

La pantalla de forma de onda puede congelarse para inspeccionar un transitorio en detalle, o borrarse para comenzar desde cero. Use estos gestos para controlar lo que muestra la pantalla sin afectar la cadena de audio.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE del panel lateral derecho para mostrarlo.

## Pasos

### Pausar y reanudar

1. Haga un solo clic en cualquier parte de la pantalla de forma de onda.
   La pantalla se congela en la instantánea del búfer actual. Aparece un indicador **PAUSED** en el pie.
2. Haga un solo clic nuevamente en la pantalla para reanudar la actualización en vivo. El indicador **PAUSED** desaparece.

### Limpiar el búfer

1. Haga doble clic en cualquier parte de la pantalla de forma de onda.
   El búfer circular de la dirección activa (RX o TX) se borra y la pantalla regresa a vacío.

## Qué hace cada control

| Interacción | Comportamiento | Estado predeterminado |
|---|---|---|
| Un clic en la pantalla | Alterna entre vista en vivo y pausada. Mientras está pausada, se muestra una instantánea del búfer y aparece un indicador **PAUSED** en el pie. | En vivo |
| Doble clic en la pantalla | Borra el búfer circular de la dirección activa (RX o TX). Restablece la pantalla a vacío. | — |

## Consejos

- La pausa distingue la dirección: la instantánea conserva el lado (RX o TX) que estaba activo en el momento del clic. El color de dirección y la etiqueta RX/TX del encabezado permanecen visibles para identificar qué ruta se está inspeccionando.
- El doble clic borra únicamente el búfer de la dirección activa. Si está en modo RX, el búfer TX no se ve afectado.
- La pantalla muestra una ventana de tiempo de 100 ms. La pausa es más útil cuando necesita medir un evento breve que de otro modo desaparecería antes de poder examinarlo.

## Solución de problemas

- **El doble clic borra en lugar de pausar** — Esto es normal. Qt distingue entre clic simple y doble clic usando el intervalo de doble clic del sistema. Haga un clic y espere; si la pantalla no se pausa, intente hacer clic más lentamente.
- **El indicador PAUSED no es visible** — El indicador aparece en el pie, a la derecha del contador de escala de tiempo. Si el applet es muy estrecho, el texto del pie puede truncarse. Amplíe el panel del applet o ábralo en ventana flotante con `View > Pop Out Applet Panel`.

## Relacionado

- [Descripción general del applet Waveform](overview.md)
- [Usar la pantalla de forma de onda para monitorear audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
