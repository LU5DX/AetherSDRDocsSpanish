# Recarga automática del registro ADIF cuando el programa de registro lo actualiza

Cuando el coloreado DXCC está habilitado, AetherSDR puede vigilar su archivo de registro ADIF y volver a leerlo automáticamente cada vez que su software de registro escribe un nuevo QSO. Esto mantiene los colores de los spots actualizados sin necesidad de recargar manualmente.

## Antes de comenzar

- El coloreado DXCC debe estar habilitado y un archivo ADIF debe estar ya cargado. Consulte [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su software de registro debe escribir las actualizaciones en la misma ruta de archivo ADIF que AetherSDR tiene cargada.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **DXCC Coloring** está habilitado (el interruptor aparece como activo).
4. Confirme que **Log File (ADIF):** muestra la ruta de archivo correcta.
5. Haga clic en **Auto-Reload Log:** para habilitarlo.

AetherSDR vigilará ahora el archivo y lo volverá a leer cada vez que cambie. Los colores de los spots en el panadapter se actualizan para reflejar el nuevo contenido del registro.

## Qué hace cada control

| Control | Comportamiento | Configuración persistente |
|---|---|---|
| **DXCC Coloring** | Interruptor principal para colorear los spots según el estado trabajado/confirmado/necesario de DXCC. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un selector de archivos para elegir el archivo de registro ADIF que controla el coloreado DXCC. La ruta seleccionada se guarda. | `DxccAdifPath` |
| **Auto-Reload Log:** | Cuando está habilitado, vuelve a leer el archivo ADIF cada vez que se modifica en el disco. | `DxccAutoReload` |

## Consejos

- Apunte la exportación ADIF de su software de registro a la misma ruta de archivo almacenada en `DxccAdifPath`. Muchos programas de registro admiten una opción de exportación continua o por QSO guardado que escribe en un archivo fijo.
- Si su programa de registro crea un archivo nuevo en cada exportación en lugar de actualizar el existente, el vigilante de archivos no detectará el cambio. Configure su programa de registro para que sobreescriba siempre el mismo archivo.

## Solución de problemas

- **Los colores de los spots no se actualizan después de registrar un QSO** — Verifique que **Auto-Reload Log:** esté habilitado en la pestaña **Display**. Confirme también que su programa de registro está escribiendo en la ruta de archivo exacta que aparece junto a **Log File (ADIF):**. Si el programa escribe en un archivo diferente o renombra el archivo en cada exportación, el vigilante no se activará.
- **El interruptor DXCC Coloring está desactivado** — **Auto-Reload Log:** no tiene efecto a menos que **DXCC Coloring** también esté habilitado. Habilite primero **DXCC Coloring**.

## Relacionado

- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
