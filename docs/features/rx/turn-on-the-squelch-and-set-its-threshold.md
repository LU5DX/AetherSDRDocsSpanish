# Activar el silenciador y ajustar su umbral

Use los controles del silenciador en el applet RX Controls para silenciar la salida de audio cuando no haya señal presente. Esto es más útil en FM y en frecuencias de HF ruidosas donde desea audio solo cuando una señal abre el silenciador.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Identifique a qué slice desea aplicar el silenciador.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de la bandeja **RX** en la barra lateral derecha si aún no está visible.
2. Si tiene varios slices, haga clic en la pestaña del slice correspondiente (**A** a la **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Ajuste el umbral del silenciador arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el silenciador.
4. Haga clic en **SQL** para activar el silenciador. El botón se activa y el silenciador entra en efecto al nivel configurado en el paso 3.

Para desactivar el silenciador, haga clic nuevamente en **SQL** para desactivarlo.

## Qué hace cada control

| Control           | Valor predeterminado | Rango válido |
|-------------------|----------------------|--------------|
| **SQL**           | Off                  | On / Off     |
| **Squelch level** | 20                   | 0–100        |

## Acerca de la memoria del nivel manual del silenciador

El último umbral manual del silenciador que configuró se guarda entre sesiones. Cuando cambie de modo o reinicie AetherSDR, el control deslizante **Squelch level** vuelve a su configuración manual anterior (valor almacenado en `LastManualSquelchLevel`). Esto persiste independientemente del nivel automático del silenciador de la radio, que la radio puede anular cuando un valor sugerido por un algoritmo difiere de su preferencia.

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el silenciador nunca se abre con una señal que pueda oír, reduzca el valor de **Squelch level**.
- Si el silenciador nunca se cierra entre señales, aumente el valor de **Squelch level**.
- El control deslizante tiene un valor predeterminado de 20 en el primer inicio de una instalación nueva.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está silenciado. La activación/desactivación del silencio (🔊 / 🔇) es independiente del silenciador. Haga clic en el botón de silencio para reactivar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel del silenciador está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito del silenciador permanece inactivo hasta que **SQL** esté activado. Confirme que **SQL** esté marcado.
- **El botón SQL aparece atenuado** — El silenciador no está disponible en los modos CW, CWL, DIGU, DIGL, NT o RTTY. En modo CW/CWL, la radio gestiona el silenciador internamente. En modos digitales (DIGU, DIGL, NT) y RTTY, el audio se enruta a través de DAX y el silenciador no es relevante: bloquearía señales FSK débiles e interrumpiría la decodificación. Cambie a un modo que admita el silenciador o use el control deslizante **AF gain** para controlar el nivel de audio.
- **El nivel del silenciador se restablece a un valor diferente al que configuré** — Si ve el control deslizante en un nivel que no eligió, es posible que la radio haya informado un nivel automático del silenciador. El umbral manual de su último ajuste se conserva en la configuración de AetherSDR y se restaurará la próxima vez que active el silenciador con **SQL**.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En la v0.9.5.1, los botones de las pestañas de slice se reconstruyen completamente cada vez que la radio se reconecta o cambia la cantidad de slices disponibles. Si la fila de pestañas aparece incorrecta, desconéctese y reconéctese a la radio; las pestañas se restablecerán para coincidir con la cantidad actual de slices del hardware.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Ajustar el ancho del filtro](adjust-filter-width.md)
