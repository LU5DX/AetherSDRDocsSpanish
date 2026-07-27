# Alinear el reloj local con la base de tiempo GPS del radio

Utilice este procedimiento para sincronizar el reloj de su PC con la base de tiempo de precisión disciplinada por GPS del FLEX-8600 para obtener marcas de tiempo con precisión de muestra en toda su estación.

## Antes de comenzar

- Asegúrese de que el radio esté conectado a AetherSDR.
- Verifique que el radio tenga bloqueo GPS/GNSS (consulte [Verificar el estado de bloqueo GPS/GNSS del radio](check-the-radio-s-gps-gnss-lock-status.md)).

## Pasos

1. Abra el panel Applet y haga clic en el mosaico **AetherClock**.
2. Confirme que el **indicador de bloqueo GNSS** muestre "Locked".
3. Observe el valor de **Deriva del reloj** en nanosegundos: este es el desfase actual entre el reloj GPS del radio y el reloj de su PC.
4. Haga clic en **Align Clock**.

AetherSDR ajusta el reloj del sistema local para que coincida con la base de tiempo GPS del radio. El indicador de **Deriva del reloj** debería restablecerse a un valor cercano a cero.

## Función de cada control

| Control | Propósito |
|---------|-----------|
| **Indicador de bloqueo GNSS** | Muestra el estado de bloqueo GPS/GNSS del radio: Locked (Bloqueado), Unlocked (Desbloqueado) o Acquiring (Adquiriendo). |
| **Deriva del reloj** | Muestra la deriva medida entre el reloj GPS del radio y el reloj de su PC en nanosegundos. |
| **Align Clock** | Alinea el reloj local del PC con la referencia disciplinada por GPS del radio. |

## Consejos

- El radio debe tener bloqueo GNSS para que la alineación sea precisa. Si el indicador muestra "Unlocked" o "Acquiring", espere hasta que muestre "Locked".
- Después de la alineación, el valor de **Deriva del reloj** debería permanecer cercano a cero si el radio mantiene el bloqueo.

## Solución de problemas

- **El indicador de bloqueo GNSS muestra "Unlocked"** — El receptor GPS del radio no tiene una corrección de tiempo válida. Asegúrese de que el radio tenga una vista despejada del cielo o suficiente recepción de satélites.
- **La deriva del reloj sigue siendo alta después de hacer clic en Align Clock** — Es posible que su sistema requiera privilegios de administrador/superusuario para cambiar el reloj del sistema. En Linux, asegúrese de que su usuario tenga permiso o ejecute AetherSDR con la capacidad `CAP_SYS_TIME`.

## Relacionados

- [Verificar el estado de bloqueo GPS/GNSS del radio](check-the-radio-s-gps-gnss-lock-status.md)
- [Monitorear la deriva del reloj entre el PC y el radio](monitor-clock-drift-between-pc-and-radio.md)
- [Descripción general de AetherClock](overview.md)
