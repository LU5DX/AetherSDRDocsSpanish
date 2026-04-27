# Activar el silenciador y ajustar su umbral

Use los controles de silenciador en el applet RX Controls para silenciar la salida de audio cuando no hay señal presente. Esto es más útil en frecuencias FM y HF ruidosas donde se desea audio únicamente cuando una señal abre el silenciador.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión de radio activa.
- Identifique a qué slice desea aplicar el silenciador.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de bandeja **RX** de la barra lateral derecha si no está visible aún.
2. Si tiene múltiples slices, haga clic en la pestaña del slice correspondiente (**A** hasta **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Ajuste el umbral del silenciador arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el silenciador.
4. Haga clic en **SQL** para activar el silenciador. El botón se activa y el silenciador entra en efecto al nivel establecido en el paso 3.

Para desactivar el silenciador, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **SQL** | Desactivado | Activado / Desactivado | Activa el silenciador al nivel actual del control deslizante. No tiene efecto cuando no está marcado. |
| **Squelch level** | 20 | 0–100 | Establece el umbral del silenciador. Valores más altos requieren una señal más fuerte para abrir el silenciador. Solo tiene efecto cuando **SQL** está activado. |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde se encuentra el umbral en relación con el ruido de fondo.
- Si el silenciador nunca se abre con una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el silenciador nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Resolución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está en mute. El botón de silencio (🔊 / 🔇) es independiente del silenciador. Haga clic en el botón de silencio para reactivar el audio si es necesario. Verifique también que el control deslizante **AF gain** no esté en 0.
- **El Squelch level está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de silenciador permanece inactivo hasta que **SQL** esté activado. Confirme que **SQL** esté marcado.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
