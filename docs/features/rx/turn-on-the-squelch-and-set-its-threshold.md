# Activar el squelch y ajustar su umbral

Utilice los controles de squelch en el applet RX Controls para silenciar la salida de audio cuando no hay señal presente. Esto es más útil en FM y en frecuencias de HF con ruido, donde se desea audio solo cuando una señal abre el squelch.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa con la radio.
- Identifique el slice al que desea aplicar el squelch.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de bandeja **RX** en la barra lateral derecha si aún no está visible.
2. Si tiene varios slices, haga clic en la pestaña del slice correspondiente (**A** a **H**) en la parte superior del applet para seleccionar el slice objetivo.
3. Ajuste el umbral de squelch arrastrando el control deslizante **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el squelch.
4. Haga clic en **SQL** para habilitar el squelch. El botón se activa y el squelch entra en efecto en el nivel configurado en el paso 3.

Para deshabilitar el squelch, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control           | Valor predeterminado | Rango válido | Comportamiento |
|-------------------|---------|-------------|----------|
| **SQL / AUTO**    | Off     | Off, SQL (Manual), AUTO | Botón de ciclo de tres posiciones: cada clic avanza Off → SQL (umbral manual) → AUTO (el algoritmo rastrea el piso de ruido) → Off. En modo AUTO el botón muestra 'AUTO' en ámbar; en modo manual muestra 'SQL' en verde. Deshabilitado (y desactivado automáticamente) en modos RTTY y digitales (DIGU, DIGL) donde el squelch recortaría los caracteres FSK (#2504). |
| **Squelch level** | 20      | Manual: 0-100 (o 0-99 en recepción de reemplazo Kiwi); Auto: 5-20 dB de margen | En modo Manual ajusta el umbral de squelch (solo tiene efecto cuando el squelch está activado). En modo AUTO establece el margen en dB por encima del piso de ruido medido donde se abre la compuerta, y se guarda en `AutoSqlMarginDb`. |
| REV / XFC         | —       | REV (alternar) o XFC (momentáneo) | Para operación de repetidoras en FM, REV invierte el signo del offset de TX para trabajar un par de repetidora invertido. En backends que admiten una verificación de frecuencia de transmisión, el botón se reetiqueta como XFC: al mantenerlo presionado se mantiene la verificación de frecuencia de TX durante la pulsación, y mientras está presionado fuerza brevemente la radio hacia la frecuencia de transmisión para confirmar la cobertura. |

## Acerca de la memoria del nivel de squelch manual

El squelch tiene autoridad sobre la radio: el umbral manual no se guarda ni se restaura entre sesiones o reconexiones. Cuando cambia de modo o reinicia AetherSDR, el control deslizante **Squelch level** refleja el nivel de squelch actual de la radio, que puede incluir valores sugeridos por el algoritmo del modo AUTO. La radio es la fuente de verdad para el nivel de squelch.

En modo AUTO, el margen en dB que configure se guarda en `AutoSqlMarginDb`.

## Consejos

- Ajuste el control deslizante **Squelch level** antes de hacer clic en **SQL** para poder oír dónde se encuentra el umbral en relación con el ruido de fondo.
- Si el squelch nunca se abre en una señal que puede oír, reduzca el valor de **Squelch level**.
- Si el squelch nunca se cierra entre señales, aumente el valor de **Squelch level**.
- El control deslizante tiene un valor predeterminado de 20 en el primer arranque de una instalación nueva.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Verifique si el slice está silenciado. La alternancia de silencio (🔊 / 🔇) es independiente del squelch. Haga clic en el botón de silencio para reactivar el audio si es necesario. También verifique que el control deslizante **AF gain** no esté en 0.
- **El nivel de squelch está configurado pero no tiene efecto** — El control deslizante **Squelch level** solo controla el umbral; el circuito de squelch está inactivo hasta que se habilite **SQL**. Confirme que **SQL** esté marcado.
- **El botón SQL está atenuado o se desactiva automáticamente** — El squelch no está disponible en los modos CW, CWL, DIGU, DIGL, NT o RTTY. En el modo CW/CWL la radio gestiona el squelch internamente. En los modos digitales (DIGU, DIGL, NT) y RTTY, el audio se enruta a través de DAX y el squelch no es significativo: recortaría señales FSK débiles y rompería la decodificación. AetherSDR desactiva automáticamente el squelch al cambiar a modos RTTY o digitales. Cambie a un modo compatible con squelch, o use el control deslizante **AF gain** para controlar el nivel de audio en su lugar.
- **El nivel de squelch se restablece a un valor diferente del que configuré** — El nivel de squelch tiene autoridad sobre la radio. Si ve el control deslizante en un nivel que no eligió, la radio informó ese valor. En modo AUTO, el valor sugerido por el algoritmo anula su nivel manual; cambie al modo SQL Manual para configurar el nivel usted mismo.
- **Las pestañas de slice se ven incorrectas después de reconectar** — En v0.9.5.1, los botones de pestaña de slice se reconstruyen por completo cada vez que la radio se reconecta o cuando cambia la cantidad de slices disponibles. Si la fila de pestañas se ve incorrecta, desconecte y vuelva a conectar la radio; las pestañas se restablecerán para coincidir con la cantidad de slices de hardware actual.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con una repetidora de FM con tono CTCSS y offset +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- Ajustar el ancho del filtro
- Ajustar la ganancia AF y el balance panorámico
