# Importación/Exportación de Perfiles — Resumen

La función de Importación/Exportación de Perfiles le permite guardar perfiles de radio (Globales, de Transmisión y de Micrófono) en archivos en su máquina local y restaurarlos más tarde. Esto es útil para realizar copias de seguridad de la configuración de su radio, transferir ajustes entre radios o compartir perfiles con otros operadores.

## Antes de comenzar

- Se requiere una conexión de radio para exportar perfiles desde la radio o importarlos a ella.
- La función requiere AetherSDR v26.5.2.1 o posterior.

## Cómo funciona

El cuadro de diálogo de Importación/Exportación de Perfiles tiene dos pestañas: **Export** (Exportar) e **Import** (Importar).

### Pestaña Export (Exportar)

1. Abra el cuadro de diálogo: **Profiles > Import/Export Profiles...**
2. Haga clic en la pestaña **Export** si no está seleccionada.
3. Marque las casillas junto a los perfiles que desea exportar.
4. Elija una ruta de archivo usando el selector de rutas.
5. Haga clic en **Export** para guardar los perfiles seleccionados en el archivo elegido.

### Pestaña Import (Importar)

1. Abra el cuadro de diálogo: **Profiles > Import/Export Profiles...**
2. Haga clic en la pestaña **Import**.
3. Busque el archivo de perfiles en su máquina local; se muestran los archivos disponibles.
4. Seleccione qué perfiles restaurar usando las casillas de verificación.
5. Haga clic en **Import** para enviar los perfiles seleccionados a la radio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Notas |
|---------|------|---------------|-------|
| **Export** (pestaña) | pestaña | Muestra una lista de perfiles de radio con casillas de verificación para seleccionar y un selector de ruta de archivo. Al hacer clic en **Export** se guardan los perfiles seleccionados en el archivo elegido. | Nuevo en v26.5.2.1. |
| **Import** (pestaña) | pestaña | Muestra los archivos de perfiles disponibles en la máquina local. Seleccione qué perfiles restaurar y haga clic en **Import** para enviarlos a la radio. | — |

## Relacionado

- Profile Manager (Administrador de Perfiles) — ver, crear, editar y eliminar perfiles de transmisión
