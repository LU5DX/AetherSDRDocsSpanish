# Activar el squelch y ajustar su umbral

Use el squelch para silenciar el audio del slice (receptor parcial) cuando no hay señal presente. Es especialmente útil en FM y en bandas con mucho ruido, donde se desea silencio entre transmisiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa al radio.
- Seleccione el slice al que desea aplicar el squelch usando las pestañas de slice (A–H) en la parte superior del applet RX Controls.

## Pasos

1. Haga clic en el botón de bandeja **RX** en la barra lateral derecha para abrir el applet RX Controls, si no está visible todavía.
2. Si tiene más de un slice, haga clic en la pestaña de slice correspondiente (A–H) para vincular el applet al slice correcto.
3. Mueva el control deslizante **Squelch level** hasta el umbral deseado. El valor predeterminado es 20; el rango válido es 0–100. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para activar el squelch. El botón se activa y el squelch entra en efecto con el nivel establecido en el paso 3.

Para desactivar el squelch, haga clic en **SQL** nuevamente.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| **SQL** | Botón de alternancia | Desactivado | Activado / Desactivado | Activa el squelch en el nivel actual del control deslizante. El audio se silencia hasta que una señal supera el umbral. |
| **Squelch level** | Control deslizante | 20 | 0–100 | Establece el umbral del squelch. Solo tiene efecto cuando **SQL** está activado. Valores más altos requieren una señal más fuerte para abrir el squelch. |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL**, de modo que el squelch se abra en el umbral correcto en el momento de la activación.
- Si el squelch nunca se abre, disminuya el control deslizante **Squelch level**. Si nunca se cierra, auméntelo.
- El nivel de squelch no tiene efecto cuando **SQL** está desactivado.

## Solución de problemas

- **El audio siempre está silenciado después de activar SQL** — El control deslizante **Squelch level** está configurado demasiado alto. Disminuya el control deslizante hasta que el squelch se abra con la señal objetivo y, a continuación, haga clic en **SQL** nuevamente.
- **El squelch nunca se cierra entre transmisiones** — El control deslizante **Squelch level** está configurado demasiado bajo. Auméntelo hasta que el ruido débil deje de abrirlo.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
