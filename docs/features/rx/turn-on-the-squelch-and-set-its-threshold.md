# Activar el silenciador y ajustar su umbral

Utilice los controles de silenciador en el applet RX Controls para silenciar la salida de audio cuando no haya señal presente. Esto es más útil en FM y frecuencias de HF ruidosas donde desea audio solo cuando una señal abre el silenciador.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Identifique el slice al que desea aplicar el silenciador.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón **RX** de la bandeja en la barra lateral derecha si aún no está visible.
2. Si tiene múltiples slices, haga clic en la pestaña del slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Ajuste el umbral del silenciador arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el silenciador.
4. Haga clic en **SQL** para activar el silenciador. El botón se activa y el silenciador entra en efecto al nivel configurado en el paso 3.

Para desactivar el silenciador, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control          | Valor predeterminado | Rango válido |
|------------------|----------------------|--------------|
| **SQL**          | Off                  | On / Off     |
| **Squelch level** | 20                   | 0–100        |

## Acerca de la memoria del nivel manual del silenciador

El último umbral manual del silenciador que haya ajustado se guarda entre sesiones. Cuando cambie de modo o reinicie AetherSDR, el control deslizante **Squelch level** volverá a su ajuste manual anterior (valor almacenado en `LastManualSquelchLevel`). Esto persiste de forma independiente del nivel automático del silenciador de la radio, el cual la radio puede anular cuando un valor sugerido por el algoritmo difiere de su preferencia.

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el silenciador nunca se abre en una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el silenciador nunca se cierra entre señales, aumente el valor de **Squelch level**.
- El control deslizante tiene un valor predeterminado de 20 en el primer inicio de una instalación nueva.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está silenciado. La alternancia de silencio (🔊 / 🔇) es independiente del silenciador. Haga clic en el botón de silencio para reactivar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel del silenciador está ajustado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito del silenciador está inactivo hasta que se activa **SQL**. Confirme que **SQL** esté marcado.
- **El botón SQL aparece atenuado** — El silenciador no está disponible en modos CW, CWL, DIGU, DIGL, NT o RTTY. En modo CW/CWL la radio gestiona el silenciador internamente. En modos digitales (DIGU, DIGL, NT) y RTTY, el audio se enruta a través de DAX y el silenciador no tiene sentido — cerraría señales FSK débiles e interrumpiría la decodificación. Cambie a un modo que admita silenciador, o use el control deslizante **AF gain** para controlar el nivel de audio.
- **El nivel del silenciador se restablece a un valor diferente al que ajusté** — Si ve el control deslizante en un nivel que no eligió, es posible que la radio haya informado un nivel automático de silenciador. El umbral manual de su último ajuste se conserva en la configuración de AetherSDR y se restaurará la próxima vez que active el silenciador con **SQL**.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En la versión v0.9.5.1, los botones de pestaña de slice se reconstruyen completamente cuando la radio se reconecta o cambia la cantidad de slices disponibles. Si la fila de pestañas se ve incorrecta, desconéctese y reconéctese a la radio; las pestañas se restablecerán para coincidir con la cantidad actual de slices del hardware.

## Relacionado

- [RX Controls overview](overview.md)
- [Change mode (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Work an FM repeater with CTCSS tone and +/- offset](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Adjust filter width](adjust-filter-width.md)
- [Adjust AF gain and pan balance](adjust-af-gain-and-pan-balance.md)
