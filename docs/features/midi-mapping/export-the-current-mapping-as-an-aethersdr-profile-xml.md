# Exportar la asignación actual como un XML de perfil de AetherSDR

En esta página se muestra cómo guardar sus asignaciones MIDI actuales como un archivo XML de perfil de AetherSDR que puede compartir o respaldar.

## Antes de comenzar

- Abra el diálogo MIDI Controller Mapping mediante `Settings > MIDI Mapping...`.
- Tenga al menos una asignación MIDI configurada. Si su tabla de asignaciones está vacía, la exportación producirá un perfil sin asignaciones.

## Pasos

1. Haga clic en **Export...**.
2. En el diálogo de archivo, elija dónde guardar el archivo XML del perfil.
3. Ingrese un nombre de archivo y haga clic en Save.

El diálogo informa cuántas asignaciones se exportaron. El directorio recordado se almacena bajo `MidiImportExportPath` y se usará la próxima vez que abra el diálogo de archivo de Export o Import.

## Qué hace cada control

| Control | Comportamiento | Configuración persistida |
|---|---|---|
| **Export...** | Exporta las asignaciones actuales como un archivo XML de perfil de AetherSDR. | `MidiImportExportPath` (directorio recordado) |

## Consejos

- El archivo exportado es XML plano, por lo que puede abrirlo en cualquier editor de texto para inspeccionar o transferir asignaciones manualmente.
- AetherSDR también puede importar un archivo `.map` de SmartSDR si está migrando desde una configuración de FlexRadio — use **Import...** en el mismo diálogo.

## Relacionado

- [Importar un perfil MIDI o un archivo .map de SmartSDR](import-a-midi-profile-or-smartsdr-map-file.md)
- [Guardar la asignación actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Cargar un perfil MIDI guardado previamente](load-a-previously-saved-midi-profile.md)
- [Descripción general de MIDI Controller Mapping](overview.md)
