# Active el silencio y ajuste su umbral

Use los controles de silencio en el applet RX Controls para silenciar la salida de audio cuando no haya señal presente. Esto es más útil en FM y en frecuencias HF ruidosas donde desea audio solo cuando una señal abre el silencio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión de radio activa.
- Identifique el slice al que desea aplicar el silencio.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón **RX** de la bandeja en la barra lateral derecha si aún no está visible.
2. Si tiene múltiples slices, haga clic en la pestaña del slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice objetivo.
3. Ajuste el umbral de silencio arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el silencio.
4. Haga clic en **SQL** para activar el silencio. El botón se activa y el silencio entra en efecto al nivel configurado en el paso 3.

Para desactivar el silencio, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control           | Valor predeterminado | Rango válido |
|-------------------|----------------------|--------------|
| **SQL**           | Apagado              | Encendido / Apagado |
| **Squelch level** | 20                   | 0–100        |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el silencio nunca se abre en una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el silencio nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Solución de problemas

- **El audio está silenciado incluso con SQL apagado** — Verifique si el slice está silenciado. La alternancia de silencio (🔊 / 🔇) es independiente del SQL. Haga clic en el botón de silencio para activar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel de silencio está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de silencio está inactivo hasta que se activa **SQL**. Confirme que **SQL** esté marcado.
- **El botón SQL está atenuado** — El silencio no está disponible en los modos CW, DIGU, DIGL o NT. En modo CW, la radio gestiona el silencio internamente. En modos digitales (DIGU, DIGL, NT), el audio se enruta a través de DAX y el silencio no tiene sentido. Cambie a un modo que admita silencio, o use el control deslizante **AF gain** para controlar el nivel de audio.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En v0.9.5.1, los botones de las pestañas de slice se reconstruyen completamente cada vez que la radio se reconecta o cambia el número de slices disponibles. Si la fila de pestañas se ve incorrecta, desconecte y vuelva a conectar la radio; las pestañas se restablecerán para coincidir con el número actual de slices del hardware.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Ajustar el ancho del filtro](adjust-filter-width.md)
