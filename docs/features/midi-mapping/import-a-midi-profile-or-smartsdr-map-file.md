# Importar un perfil MIDI o un archivo .map de SmartSDR

Esta página explica cómo importar un perfil de asignación MIDI guardado en AetherSDR — ya sea un archivo XML de perfil de AetherSDR o un archivo ".map" de SmartSDR — y aplicarlo a su configuración actual de controlador MIDI.

## Antes de comenzar

- Tenga un controlador MIDI conectado a su radio (consulte [Connect a MIDI controller](../../getting-started/setup/connect-a-midi-controller.md)).
- Sepa qué archivo de perfil desea importar: un XML de perfil de AetherSDR o un archivo .map de SmartSDR.

## Pasos

1. Abra el diálogo de asignación MIDI: **Settings > MIDI Mapping...**.
2. En la sección "Parameter Bindings", haga clic en **Import...**.
3. En el diálogo de archivos, localice y seleccione su archivo de perfil (XML de perfil de AetherSDR o archivo .map de SmartSDR). El diálogo se abre en el último directorio de importación/exportación utilizado, o en su carpeta Documents la primera vez.
4. Haga clic en **Open**. AetherSDR lee el archivo e informa cuántas asignaciones importó.
5. En el cuadro combinado **Profile:**, seleccione el perfil importado.
6. Haga clic en **Load** para aplicar las asignaciones importadas a su mapeo actual.

## Qué hace cada control

- **Import...** — Importa un archivo de perfil (XML de perfil de AetherSDR o un archivo .map de SmartSDR) al almacén de perfiles. Nuevo en v26.8.4.
- **Profile:** — Selecciona un perfil de asignación MIDI guardado, incluido uno que acaba de importar.
- **Load** — Carga el perfil actualmente seleccionado en el conjunto de asignaciones activo.

El directorio desde el que importó o al que exportó por última vez se recuerda y se almacena en la configuración `MidiImportExportPath`.

## Consejos

- Después de importar, haga clic en **Load** para activar las asignaciones importadas. El paso de importación por sí solo solo agrega el perfil al almacén.
- Puede importar archivos .map de SmartSDR directamente; no se necesita conversión.

## Relacionados

- [Overview](overview.md)
- [Export the current mapping as an AetherSDR profile XML](export-the-current-mapping-as-an-aethersdr-profile-xml.md)
- [Save the current mapping as a named profile](save-the-current-mapping-as-a-named-profile.md)
- [Load a previously saved MIDI profile](load-a-previously-saved-midi-profile.md)
