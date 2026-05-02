# Activar el squelch y ajustar su umbral

Use los controles de squelch en el applet RX Controls para silenciar la salida de audio cuando no hay señal presente. Esto es más útil en frecuencias FM y HF con mucho ruido, donde se desea audio únicamente cuando una señal abre el squelch.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión de radio activa.
- Identifique qué slice desea controlar con el squelch.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón **RX** de la bandeja en la barra lateral derecha, si no está visible todavía.
2. Si tiene múltiples slices, haga clic en la pestaña de slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Establezca el umbral del squelch arrastrando el control deslizante **Squelch level** hasta el nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para activar el squelch. El botón se activa y el squelch entra en efecto con el nivel establecido en el paso 3.

Para desactivar el squelch, haga clic en **SQL** nuevamente para deshabilitarlo.

## Qué hace cada control

| Control           | Valor predeterminado | Rango válido |
|-------------------|----------------------|--------------|
| **SQL**           | Apagado              | Activado / Apagado |
| **Squelch level** | 20                   | 0–100        |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para escuchar dónde queda el umbral en relación con el ruido de fondo.
- Si el squelch nunca se abre con una señal que usted puede escuchar, disminuya el valor de **Squelch level**.
- Si el squelch nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está en silencio. El botón de silencio (🔊 / 🔇) es independiente del squelch. Haga clic en el botón de silencio para reactivar el audio si es necesario. Verifique también que el control deslizante **AF gain** no esté en 0.
- **El nivel de squelch está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de squelch permanece inactivo hasta que **SQL** esté habilitado. Confirme que **SQL** esté activado.
- **El botón SQL aparece deshabilitado** — El squelch no está disponible en los modos CW, DIGU, DIGL ni NT. En el modo CW, el radio gestiona el squelch internamente. En los modos digitales (DIGU, DIGL, NT), el audio se enruta a través de DAX y el squelch no es aplicable. Cambie a un modo que admita squelch, o use el control deslizante **AF gain** para controlar el nivel de audio en su lugar.
- **Las pestañas de slice se ven incorrectas tras reconectar** — En la versión v0.9.5.1, los botones de pestaña de slice se reconstruyen completamente cada vez que el radio se reconecta o cambia el número de slices disponibles. Si la fila de pestañas se ve incorrecta, desconecte y reconecte el radio; las pestañas se restablecerán para coincidir con el número actual de slices del hardware.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar un repetidor FM con tono CTCSS y desvío +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
