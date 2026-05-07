# Restaurar la configuración predeterminada de fábrica de AetherSDR

Utilice este procedimiento para eliminar la configuración almacenada localmente de AetherSDR y el caché de conocimiento NR2, restaurándolos a sus valores predeterminados de fábrica. La configuración almacenada en la radio no se ve afectada.

## Antes de comenzar

- Cierre cualquier transmisión activa o flujo de audio antes de restablecer.
- Tome nota de cualquier configuración personalizada que desee restaurar después, ya que el restablecimiento no se puede deshacer.

## Pasos

1. Abra `Help > Support...` para abrir el diálogo de Soporte y Diagnóstico.
2. Haga clic en `Reset Settings`.
3. Cuando aparezca la ventana de confirmación, confirme la acción.
4. Reinicie AetherSDR para que el restablecimiento surta efecto por completo.

## Qué hace cada control

| Control | Descripción |
|---|---|
| `Reset Settings` | Elimina la configuración local de AetherSDR y el caché de conocimiento NR2. La configuración almacenada en la radio FLEX-8600 no se modifica. Se muestra una ventana de confirmación antes de eliminar cualquier dato. |

## Consejos

- La configuración del lado de la radio (perfiles, diseño del panadapter almacenado en la radio, ajustes de banda de TX) permanece intacta después de un restablecimiento. Solo se eliminan los AppSettings persistentes propios de AetherSDR y los datos DSP almacenados en caché.
- Si está restableciendo para resolver un problema reproducible, considere capturar un registro primero. Consulte [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).

## Relacionados

- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Enviar un informe de error asistido por IA](file-an-ai-assisted-bug-report.md)
- [Descripción general de Soporte y Diagnóstico](overview.md)
