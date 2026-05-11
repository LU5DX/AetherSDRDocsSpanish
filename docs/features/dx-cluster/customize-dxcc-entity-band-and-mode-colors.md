# Personalizar colores de entidad DXCC, banda y modo

Después de cargar un registro ADIF para colorear por DXCC, puede asignar colores de spot separados para entidades DXCC necesitadas, nuevas bandas en entidades ya trabajadas, nuevos modos en entidades ya trabajadas y entidades ya confirmadas. Esto le ayuda a identificar de un vistazo las aperturas más raras.

## Antes de comenzar

- Disponga de un archivo de registro ADIF (desde su programa de registro o desde una exportación anterior).
- El coloreado DXCC está habilitado. Consulte [Habilitar coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Si el coloreado DXCC no está activado, haga clic en el botón de alternancia **DXCC Colors:** para activarlo.
4. Haga clic en **Log File (ADIF):** y seleccione su archivo ADIF. La aplicación carga el registro y muestra un recuento como `<N> QSOs / <M> entities`.
5. Localice los cuatro botones de muestra de color **DXCC Color** bajo la sección **DXCC Coloring**.
6. Haga clic en una muestra para abrir un selector de color:
   - **New DXCC** – spots para entidades no confirmadas en su registro.
   - **New Band** – spots para una entidad ya trabajada, pero en una banda no confirmada.
   - **New Mode** – spots para una combinación entidad/banda ya trabajada, pero no en este modo.
   - **Worked** – spots para entidades, bandas y modos ya confirmados.
7. Elija un color y cierre el selector. Los spots en el panadapter se actualizan inmediatamente.

## Qué hace cada control

| Control | Clave de ajuste | Comportamiento |
|---------|-----------------|----------------|
| Alternancia **DXCC Colors:** | `IsDxccColoringEnabled` | Activa o desactiva todo el coloreado DXCC. |
| **Log File (ADIF):** | `DxccAdifFilePath` | Abre un diálogo de archivos para seleccionar un registro ADIF. El archivo se vigila en busca de cambios y se recarga automáticamente. |
| Indicador **Imported:** | ninguno | Muestra `N QSOs / M entities` cuando hay un registro cargado; muestra `(no log loaded)` en caso contrario. |
| Muestra de color **New DXCC** | `DxccColorNewEntity` | Color para spots cuya entidad DXCC aún no está confirmada en el registro. |
| Muestra de color **New Band** | `DxccColorNewBand` | Color para spots de una entidad ya trabajada en una banda no confirmada. |
| Muestra de color **New Mode** | `DxccColorNewMode` | Color para spots de una entidad y banda ya trabajadas en un modo no confirmado. |
| Muestra de color **Worked** | `DxccColorWorked` | Color para spots ya confirmados en el registro. |

## Consejos

- El archivo ADIF se vigila automáticamente en busca de cambios — no hay un botón separado de "recargar". Si su programa de registro actualiza el archivo, AetherSDR detecta los cambios en el siguiente evento de modificación del archivo.
- El coloreado DXCC reemplaza los colores de spot por fuente que pueda haber configurado en las pestañas Cluster, RBN, WSJT-X u otras. Para usar colores por fuente en su lugar, desactive la alternancia **DXCC Colors:**.

## Solución de problemas

- **Los colores no cambian en el panadapter** — Asegúrese de que hay un archivo de registro cargado (verifique que el indicador **Imported:** muestre un recuento, no `(no log loaded)`). También verifique que la alternancia **DXCC Colors:** esté activada (muestra un relleno verde).
- **Todos los spots muestran el mismo color** — Confirme que su archivo ADIF contiene registros QSO válidos con información de entidad DXCC. Solo se usan para la comparación los contactos que incluyen una entidad, banda y modo válidos.

## Relacionados

- [Habilitar coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
