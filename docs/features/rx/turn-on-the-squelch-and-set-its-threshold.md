# Activar el squelch y ajustar su umbral

Use los controles de squelch del applet RX Controls para silenciar la salida de audio cuando no hay señal presente. Esto resulta más útil en FM y en frecuencias HF ruidosas donde se desea audio únicamente cuando una señal abre el squelch.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión de radio activa.
- Identifique a qué slice desea aplicar el squelch.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de bandeja **RX** de la barra lateral derecha, si no está visible aún.
2. Si tiene múltiples slices, haga clic en la pestaña del slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Ajuste el umbral de squelch arrastrando el control deslizante **Squelch level** hasta el nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para activar el squelch. El botón se activa y el squelch entra en efecto al nivel establecido en el paso 3.

Para desactivar el squelch, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **SQL** | Apagado | Encendido / Apagado | Activa el squelch al nivel actual del control deslizante. No tiene efecto cuando no está marcado. |
| **Squelch level** | 20 | 0–100 | Establece el umbral de squelch. Valores más altos requieren una señal más fuerte para abrir el squelch. Solo tiene efecto cuando **SQL** está activado. |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde queda el umbral en relación con el ruido de fondo.
- Si el squelch nunca se abre ante una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el squelch nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Solución de problemas

- **El audio está en silencio aunque SQL esté desactivado** — Verifique si el slice está silenciado. El botón de silencio (🔊 / 🔇) es independiente del squelch. Haga clic en el botón de silencio para reactivar el audio si es necesario. Además, compruebe que el control deslizante **AF gain** no esté en 0.
- **El nivel de squelch está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de squelch permanece inactivo hasta que **SQL** esté habilitado. Confirme que **SQL** esté marcado.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
