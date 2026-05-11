# Activar el squelch y ajustar su umbral

Use los controles de squelch en el applet RX Controls para silenciar la salida de audio cuando no haya señal presente. Esto es más útil en FM y en frecuencias de HF ruidosas donde desea audio solo cuando una señal abre el squelch.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Identifique qué slice desea aplicar al squelch.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de la bandeja **RX** en la barra lateral derecha si aún no está visible.
2. Si tiene varios slices, haga clic en la pestaña del slice correspondiente (**A** a la **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Ajuste el umbral del squelch arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para habilitar el squelch. El botón se activa y el squelch entra en efecto al nivel configurado en el paso 3.

Para desactivar el squelch, haga clic nuevamente en **SQL**.

## Qué hace cada control

| Control          | Predeterminado | Rango válido   |
|------------------|----------------|----------------|
| **SQL**          | Apagado        | Encendido / Apagado |
| **Squelch level** | 20            | 0–100          |

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder oír dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el squelch nunca se abre en una señal que puede oír, reduzca el valor de **Squelch level**.
- Si el squelch nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Solución de problemas

- **El audio está silencioso incluso con SQL apagado** — Verifique si el slice está silenciado. La alternancia de silencio (🔊 / 🔇) es independiente del squelch. Haga clic en el botón de silencio para reactivar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel de squelch está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de squelch permanece inactivo hasta que **SQL** esté habilitado. Confirme que **SQL** esté marcado.
- **El botón SQL aparece atenuado** — El squelch no está disponible en modos CW, CWL, DIGU, DIGL, NT o RTTY. En modo CW/CWL la radio gestiona el squelch internamente. En modos digitales (DIGU, DIGL, NT) y RTTY, el audio se enruta a través de DAX y el squelch no tiene sentido práctico: silenciaría señales FSK débiles e interrumpiría la decodificación. Cambie a un modo que admita squelch, o use el control deslizante **AF gain** para ajustar el nivel de audio.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En v0.9.5.1, los botones de las pestañas de slice se reconstruyen completamente cada vez que la radio se reconecta o cambia la cantidad de slices disponibles. Si la fila de pestañas se ve incorrecta, desconecte y reconecte la radio; las pestañas se restablecerán para coincidir con la cantidad actual de slices del hardware.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con un repetidor FM usando tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Ajustar el ancho del filtro](adjust-filter-width.md)
