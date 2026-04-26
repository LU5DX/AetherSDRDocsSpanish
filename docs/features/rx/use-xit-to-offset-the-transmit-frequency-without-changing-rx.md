# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión una cantidad fija mientras deja la frecuencia de recepción sin cambios. Esto es útil cuando necesita transmitir ligeramente fuera de su VFO de recepción — por ejemplo, para trabajar un pile-up en split o compensar un desplazamiento del transceptor en la otra estación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión de radio activa.
- El applet RX debe estar visible. Si no lo está, haga clic en el botón de bandeja RX en la barra lateral derecha para mostrarlo.
- Seleccione el slice correcto usando las pestañas de slice (A..H) si tiene más de un slice activo.

## Pasos

1. Abra el applet RX haciendo clic en el botón de bandeja RX en la barra lateral derecha si aún no está visible.
2. Desplácese hacia abajo hasta la fila XIT cerca de la parte inferior del applet.
3. Haga clic en XIT para habilitar Transmit Incremental Tuning. El botón se ilumina cuando está activo.
4. Ajuste el desplazamiento XIT usando el spinbox de desplazamiento XIT:
   - Haga clic en `<` para disminuir el desplazamiento en pasos de 10 Hz.
   - Haga clic en `>` para aumentar el desplazamiento en pasos de 10 Hz.
   - Desplace la rueda del ratón sobre el spinbox para cambiar el desplazamiento en pasos de 10 Hz.
5. Para devolver la frecuencia de TX a la frecuencia de RX, haga clic en XIT 0. Esto pone el desplazamiento a cero sin desactivar XIT.
6. Para deshabilitar XIT por completo, haga clic en XIT nuevamente para desactivarlo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido / paso | Comportamiento |
|---|---|---|---|
| XIT | Desactivado (sin marcar) | Activado / Desactivado | Activa o desactiva Transmit Incremental Tuning. |
| Desplazamiento XIT | +0 Hz | Paso: 10 Hz | Establece el desplazamiento de frecuencia de TX relativo al VFO de RX. Ajuste con `<` / `>` o la rueda del ratón. |
| XIT 0 | — | — | Pone inmediatamente el desplazamiento XIT a cero. No desactiva XIT. |

## Consejos

- RIT y XIT son independientes. Puede usar ambos simultáneamente: RIT desplaza lo que escucha, XIT desplaza donde transmite.
- El spinbox de desplazamiento XIT responde a la rueda del ratón cuando el cursor está posicionado sobre él, lo cual es conveniente al operar sin desplazar el foco fuera del panadapter.
- Si el slice está bloqueado para sintonización (🔒), los controles relacionados con la frecuencia quedan deshabilitados. Desbloquee el slice primero si los controles XIT no responden.

## Solución de problemas

- **El spinbox de desplazamiento XIT no tiene efecto** — Confirme que XIT está habilitado (el botón debe estar iluminado). Si el slice está bloqueado, haga clic en el botón 🔓 / 🔒 para desbloquearlo primero.
- **La frecuencia de TX no se desplaza como se esperaba** — Verifique que este slice sea el slice de TX activo. Compruebe que el botón TX (insignia) esté activo para este slice; solo el slice de TX utiliza el desplazamiento XIT al transmitir.

## Relacionados

- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Descripción general de RX Controls](overview.md)
- [Bloquear el slice para evitar una resintonización accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
