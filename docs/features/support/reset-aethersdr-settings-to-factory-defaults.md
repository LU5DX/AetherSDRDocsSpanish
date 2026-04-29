# Restablecer la configuración de AetherSDR a los valores predeterminados de fábrica

Use este procedimiento para borrar la configuración almacenada localmente por AetherSDR y la caché de sabiduría NR2, y devolverlas a sus valores predeterminados de fábrica. La configuración almacenada en el propio radio no se ve afectada.

## Antes de comenzar

- Cierre cualquier transmisión activa o flujo de audio antes de restablecer.
- Anote cualquier configuración personalizada que desee restaurar después, ya que el restablecimiento no se puede deshacer.

## Pasos

1. Abra `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `Reset Settings`.
3. Cuando aparezca el mensaje de confirmación, confirme la acción.
4. Reinicie AetherSDR para que el restablecimiento surta efecto completo.

## Qué hace cada control

| Control | Descripción |
|---|---|
| `Reset Settings` | Elimina la configuración local de AetherSDR y la caché de sabiduría NR2. La configuración almacenada en el radio FLEX-8600 no se modifica. Se muestra un mensaje de confirmación antes de eliminar cualquier dato. |

## Consejos

- La configuración del lado del radio (perfiles, disposición del panadapter almacenada en el radio, configuración de banda TX) permanece intacta después de un restablecimiento. Solo se eliminan los AppSettings persistidos por AetherSDR y los datos DSP en caché.
- Si está restableciendo para resolver un problema reproducible, considere capturar primero un registro. Consulte [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).

## Relacionado

- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Presentar un informe de error asistido por IA](file-an-ai-assisted-bug-report.md)
- [Descripción general de Support & Diagnostics](overview.md)
