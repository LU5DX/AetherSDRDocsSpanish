# Resumen de formas de onda

El diálogo Formas de onda replica el panel SmartSDR Archivo > Formas de onda, permitiéndole ver el estado del WFP (Procesador de formas de onda) y gestionar las formas de onda instaladas en su radio FLEX-8600. Úselo para verificar si el procesador de formas de onda está encendido y listo, consultar su dirección IP, y reiniciar o eliminar formas de onda individuales.

## Cómo funciona

El diálogo se conecta directamente al FlexWaveformModel de la radio para obtener actualizaciones de estado en vivo. Muestra el estado de alimentación del WFP, su disponibilidad y dirección IP en la parte superior, seguido de una lista de formas de onda instaladas con controles por fila.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Estado del WFP** | Muestra el estado de alimentación del procesador de formas de onda, el estado de disponibilidad y la dirección IP. | Nuevo en v26.5.2.1. |
| **Formas de onda instaladas** | Lista las formas de onda instaladas con botones **Reiniciar** y **Eliminar/Desinstalar** por fila. | Se conecta al FlexWaveformModel para obtener estado en vivo. |

## Cómo abrirlo

**Archivo > Formas de onda...**

## Requisitos

- Debe haber una conexión activa con la radio (el diálogo requiere conectividad con la radio).

## Consejos

- El diálogo es no modal, por lo que puede mantenerlo abierto mientras opera la radio.
- Use el botón **Reiniciar** para recargar una forma de onda sin eliminarla y reinstalarla.
- Use **Eliminar/Desinstalar** para borrar una forma de onda no deseada de la radio.
- El diálogo aplica el estilo del tema actual para las ventanas de formas de onda, garantizando coherencia visual con otros diálogos.

## Relacionado

- Configuración de la radio... — Configure la conexión de la radio, el audio, la antena y los parámetros de banda.
