# Alinear el reloj local con la base de tiempo GPS de la radio

Utilice este procedimiento para sincronizar el reloj de su PC con la base de tiempo de precisión disciplinada por GPS de la FLEX-8600 para obtener marcas de tiempo precisas a nivel de muestra en toda su estación.

## Antes de comenzar

- Asegúrese de que la radio esté conectada a AetherSDR.
- Verifique que la radio tenga bloqueo GPS/GNSS (consulte [Verificar el estado de bloqueo GPS/GNSS de la radio](check-the-radio-s-gps-gnss-lock-status.md)).

## Pasos

1. Abra el panel de Applet y haga clic en el mosaico **AetherClock**.
2. Confirme que el **indicador de bloqueo GNSS** muestre "Locked".
3. Anote el valor de **Clock drift** en nanosegundos: este es el desfase actual entre el reloj GPS de la radio y el reloj de su PC.
4. Haga clic en **Align Clock**.

AetherSDR ajusta el reloj del sistema local para que coincida con la base de tiempo GPS de la radio. El indicador de **Clock drift** debería restablecerse a un valor cercano a cero.

## Qué hace cada control

| Control | Propósito |
|---------|-----------|
| **Indicador de bloqueo GNSS** | Muestra el estado de bloqueo GPS/GNSS de la radio: Locked, Unlocked o Acquiring. |
| **Clock drift** | Muestra el desfase medido entre el reloj GPS de la radio y el reloj de su PC en nanosegundos. |
| **Align Clock** | Alinea el reloj local del PC con la referencia disciplinada por GPS de la radio. |

## Selección de canal DAX

El selector DAX en el applet AetherClock selecciona qué canal DAX enruta el audio para el slice seleccionado actualmente.

La cantidad de canales DAX disponibles coincide con la capacidad de slices de la radio:

- En radios con 2 receptores, el selector ofrece DAX 1 y DAX 2.
- En radios con 8 receptores, el selector ofrece DAX 1 a DAX 8.
- **DAX Off** siempre está disponible como primera opción.

Si un slice seleccionado tiene asignado un canal DAX que está fuera de rango para la radio actual, el selector muestra **DAX Off** en lugar de un valor no válido dentro del rango.

En radios que no tienen ningún plano DAX, el selector DAX está oculto y el banner de advertencia ámbar "sin canal DAX" se suprime porque el audio fluye normalmente a través de la alimentación integrada de la radio.

## Consejos

- La radio debe tener bloqueo GNSS antes de que la alineación sea precisa. Si el indicador muestra "Unlocked" o "Acquiring", espere hasta que muestre "Locked".
- Después de la alineación, el valor de **Clock drift** debería permanecer cerca de cero si la radio mantiene el bloqueo.

## Solución de problemas

- **El indicador de bloqueo GNSS muestra "Unlocked"** — El receptor GPS de la radio no tiene una corrección de tiempo válida. Asegúrese de que la radio tenga una vista despejada del cielo o una recepción satelital suficiente.
- **Clock drift permanece alto después de hacer clic en Align Clock** — Su sistema puede requerir privilegios de root/administrador para cambiar el reloj del sistema. En Linux, asegúrese de que su usuario tenga permiso o ejecute AetherSDR con la capacidad `CAP_SYS_TIME`.
- **El selector DAX falta o muestra menos canales de los esperados** — El selector está dimensionado según la capacidad de slices de la radio. En radios sin plano DAX, el control está oculto por completo.

## Relacionados

- [Verificar el estado de bloqueo GPS/GNSS de la radio](check-the-radio-s-gps-gnss-lock-status.md)
- [Monitorear el desfase de reloj entre PC y radio](monitor-clock-drift-between-pc-and-radio.md)
- [Descripción general de AetherClock](overview.md)
