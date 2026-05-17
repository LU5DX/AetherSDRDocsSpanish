# Personalizar los colores de entidad DXCC, banda y modo

Después de cargar un registro ADIF para colorear por DXCC, puede asignar colores de spot separados para entidades DXCC necesitadas, nuevas bandas en entidades trabajadas, nuevos modos en entidades trabajadas y entidades ya trabajadas. Esto le ayuda a identificar de un vistazo las aperturas más raras.

## Antes de comenzar

- Tiene listo un archivo de registro ADIF (desde su logger o desde una exportación anterior).
- El coloreado DXCC está habilitado. Consulte [Habilitar coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Si el coloreado DXCC aún no está activado, haga clic en el botón de alternancia **DXCC Colors:** para habilitarlo.
4. Haga clic en **Log File (ADIF):** y seleccione su archivo ADIF. La aplicación carga el registro y muestra un recuento como `<N> QSOs / <M> entities`.
5. Localice los cuatro botones de muestra de color **DXCC Color** debajo de la sección **DXCC Coloring**.
6. Haga clic en una muestra para abrir un selector de color:
   - **New DXCC** – spots de entidades no confirmadas en su registro.
   - **New Band** – spots de una entidad que ya ha trabajado, pero en una banda que no.
   - **New Mode** – spots de una combinación entidad/banda trabajada, pero no en este modo.
   - **Worked** – spots de entidades, bandas y modos ya confirmados.
7. Elija un color y cierre el selector. Los spots en el panadapter se actualizan inmediatamente.

## Qué hace cada control

| Control | Clave de ajuste | Comportamiento |
|---------|-----------------|----------------|
| Alternancia **DXCC Colors:** | `IsDxccColoringEnabled` | Activa o desactiva todo el coloreado DXCC. |
| **Log File (ADIF):** | `DxccAdifFilePath` | Abre un diálogo de archivo para seleccionar un registro ADIF. El archivo se monitorea en busca de cambios y se recarga automáticamente. |
| Indicador **Imported:** | ninguno | Muestra `N QSOs / M entities` cuando hay un registro cargado; muestra `(no log loaded)` en caso contrario. |
| Muestra de color **New DXCC** | `DxccColorNewEntity` | Color para spots cuya entidad DXCC aún no está confirmada en el registro. |
| Muestra de color **New Band** | `DxccColorNewBand` | Color para spots de una entidad trabajada en una banda aún no confirmada. |
| Muestra de color **New Mode** | `DxccColorNewMode` | Color para spots de una entidad y banda trabajadas en un modo aún no confirmado. |
| Muestra de color **Worked** | `DxccColorWorked` | Color para spots ya confirmados en el registro. |

## Consejos

- El archivo ADIF se monitorea automáticamente en busca de cambios — no hay un botón separado de "recargar". Si su logger actualiza el archivo, AetherSDR detecta los cambios en el siguiente evento de modificación del archivo.
- El coloreado DXCC anula los colores de spot por fuente que pueda haber configurado en las pestañas Cluster, RBN, WSJT-X u otras. Para usar colores por fuente en su lugar, desactive **DXCC Colors:**.

## Solución de problemas

- **Los colores no cambian en el panadapter** — Asegúrese de que haya un archivo de registro cargado (verifique que el indicador **Imported:** muestre un recuento, no `(no log loaded)`). También verifique que la alternancia **DXCC Colors:** esté habilitada (muestre un relleno verde).
- **Todos los spots muestran el mismo color** — Confirme que su archivo ADIF contenga registros QSO válidos con información de entidad DXCC. Solo los contactos que incluyan una entidad, banda y modo válidos se utilizan para la comparación.

## Relacionados

- [Habilitar coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
