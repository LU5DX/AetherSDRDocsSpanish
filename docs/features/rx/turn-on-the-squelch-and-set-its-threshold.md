# Activar el silenciador y configurar su umbral

Use los controles del silenciador en el applet RX Controls para silenciar la salida de audio cuando no hay señal presente. Esto es muy útil en FM y en frecuencias HF ruidosas donde desea audio solo cuando una señal abre el silenciador.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet RX Controls requiere una conexión activa a la radio.
- Identifique qué slice desea aplicar el silenciador.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón de bandeja **RX** en la barra lateral derecha si aún no es visible.
2. Si tiene múltiples slices, haga clic en la pestaña de slice apropiada (**A** a **H**) en la parte superior del applet para seleccionar el slice de destino.
3. Configure el umbral del silenciador arrastrando el regulador **Squelch level** al nivel deseado. Un valor más alto requiere una señal más fuerte para abrir el silenciador.
4. Haga clic en **SQL** para activar el silenciador. El botón se activa y el silenciador entra en vigor al nivel establecido en el paso 3.

Para desactivar el silenciador, haga clic en **SQL** nuevamente para desactivarlo.

## Qué hace cada control

| Control           | Predeterminado | Rango válido |
|-------------------|----------------|-------------|
| **SQL**           | Desactivado    | Activado / Desactivado    |
| **Squelch level** | 20             | 0–100       |

## Consejos

- Ajuste el regulador **Squelch level** antes de hacer clic en **SQL** para que pueda escuchar dónde se sitúa el umbral en relación con el ruido de fondo.
- Si el silenciador nunca se abre en una señal que puede escuchar, reduzca el valor de **Squelch level**.
- Si el silenciador nunca se cierra entre señales, aumente el valor de **Squelch level**.

## Solución de problemas

- **El audio está silenciado incluso con SQL desactivado** — Compruebe si el slice está silenciado. El botón de silencio (🔊 / 🔇) es independiente del silenciador. Haga clic en el botón de silencio para reactivar el audio si es necesario. Verifique también que el regulador **AF gain** no esté en 0.
- **El nivel del silenciador está configurado pero no tiene efecto** — El regulador **Squelch level** solo controla el umbral; el circuito del silenciador está inactivo hasta que **SQL** se activa. Confirme que **SQL** está marcado.
- **El botón SQL está desactivado** — El silenciador no está disponible en los modos CW, DIGU, DIGL o NT. En modo CW, la radio gestiona el silenciador internamente. En modos digitales (DIGU, DIGL, NT) el audio se enruta a través de DAX y el silenciador no es relevante. Cambie a un modo que admita silenciador, o use el regulador **AF gain** para controlar el nivel de audio en su lugar.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Operar un repetidor FM con tono CTCSS y compensación +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
