# Resumen de formas de onda

El diálogo Formas de onda refleja el panel SmartSDR Archivo > Formas de onda, permitiéndole ver el estado del WFP (Procesador de formas de onda) y gestionar las formas de onda instaladas en su radio FLEX-8600. Úselo para verificar si el procesador de formas de onda está encendido y listo, conocer su dirección IP y reiniciar o eliminar formas de onda individuales.

## Cómo funciona

El diálogo se conecta directamente al FlexWaveformModel del radio para obtener actualizaciones de estado en vivo. Muestra el estado de alimentación del WFP, su disponibilidad y dirección IP en la parte superior, seguido de una lista de formas de onda instaladas con controles por fila.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Estado del WFP** | Muestra el estado de alimentación del procesador de formas de onda, su disponibilidad y dirección IP. | Nuevo en v26.5.2.1. |
| **Formas de onda instaladas** | Lista las formas de onda instaladas con botones **Reiniciar** y **Eliminar/Desinstalar** por fila. | Se conecta a FlexWaveformModel para obtener estado en vivo. |

## Cómo abrirlo

**Archivo > Formas de onda...**

## Requisitos

- Debe haber una conexión activa al radio (el diálogo requiere conectividad con el radio).

## Consejos

- El diálogo no es modal, por lo que puede mantenerlo abierto mientras opera el radio.
- Use el botón **Reiniciar** para recargar una forma de onda sin necesidad de eliminarla y volverla a instalar.
- Use **Eliminar/Desinstalar** para borrar una forma de onda no deseada del radio.

## Relacionado

- [Configuración del radio...](radio-setup.md) — Configure la conexión del radio, audio, antena y ajustes de banda.
