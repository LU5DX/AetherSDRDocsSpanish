# Activar el squelch y ajustar su umbral

Use los controles de squelch del applet RX Controls para silenciar la salida de audio cuando no haya señal presente. Esto es más útil en FM y en frecuencias de HF ruidosas donde desea audio solo cuando una señal abre el squelch.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Identifique qué slice desea aplicar el squelch.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de la bandeja **RX** en la barra lateral derecha si aún no está visible.
2. Si tiene varios slices, haga clic en la pestaña del slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice objetivo.
3. Ajuste el umbral de squelch arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para activar el squelch. El botón se activa y el squelch entra en vigor al nivel configurado en el paso 3.

Para desactivar el squelch, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control           | Valor predeterminado | Rango válido |
|-------------------|----------------------|--------------|
| **SQL**           | Off                  | On / Off     |
| **Squelch level** | 20                   | 0–100        |

## Acerca de la memoria del nivel de squelch manual

El último umbral de squelch manual que configuró se guarda entre sesiones. Cuando cambie de modo o reinicie AetherSDR, el control deslizante **Squelch level** volverá a su ajuste manual anterior (valor almacenado en `LastManualSquelchLevel`). Esto persiste de forma independiente del nivel de squelch automático de la radio, que la radio puede anular cuando un valor sugerido por un algoritmo difiere de su preferencia.

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder escuchar dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el squelch nunca se abre con una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el squelch nunca se cierra entre señales, aumente el valor de **Squelch level**.
- El control deslizante tiene un valor predeterminado de 20 en la primera ejecución de una instalación nueva.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está silenciado. La alternativa de silencio (🔊 / 🔇) es independiente del squelch. Haga clic en el botón de silencio para reactivar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel de squelch está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de squelch está inactivo hasta que se activa **SQL**. Confirme que **SQL** esté marcado.
- **El botón SQL aparece atenuado o se desactiva automáticamente** — El squelch no está disponible en modos CW, CWL, DIGU, DIGL, NT o RTTY. En modo CW/CWL, la radio gestiona el squelch internamente. En modos digitales (DIGU, DIGL, NT) y RTTY, el audio se enruta a través de DAX y el squelch no tiene sentido práctico: bloquearía señales FSK débiles e interrumpiría la decodificación. AetherSDR desactiva automáticamente el squelch al cambiar a RTTY o modos digitales. Cambie a un modo que admita squelch, o use el control deslizante **AF gain** para controlar el nivel de audio.
- **El nivel de squelch se reinicia a un valor diferente del que configuré** — Si ve el control deslizante en un nivel que no eligió, es posible que la radio haya informado un nivel de squelch automático. El umbral manual de su último ajuste se conserva en la configuración de AetherSDR y se restaurará la próxima vez que active el squelch con **SQL**.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En la versión v0.9.5.1, los botones de las pestañas de slice se reconstruyen completamente cada vez que la radio se reconecta o cambia la cantidad de slices disponibles. Si la fila de pestañas parece incorrecta, desconéctese y vuelva a conectarse a la radio; las pestañas se restablecerán para coincidir con la cantidad actual de slices del hardware.

## Relacionado

- [Resumen de RX Controls](overview.md)
- [Cambiar de modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con un repetidor FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- Ajustar el ancho del filtro
- Ajustar la ganancia de AF y el balance del paneo
