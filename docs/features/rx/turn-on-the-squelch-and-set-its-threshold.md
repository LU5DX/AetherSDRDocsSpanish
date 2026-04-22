# Activar el silenciador (squelch) y ajustar su umbral

Use el squelch para silenciar el audio de un slice cuando no hay señal presente. Esto es más útil en FM, NFM o bandas de HF ruidosas donde se desea silencio entre transmisiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El squelch es un control por slice y requiere un slice activo.
- Abra el applet RX Controls. Si no está visible, haga clic en el botón de bandeja **RX** de la barra lateral derecha.

## Pasos

1. En el applet RX Controls, localice el botón **SQL** y el control deslizante del nivel de squelch que se encuentra inmediatamente a su derecha.
2. Establezca primero el umbral de squelch: arrastre el control deslizante hacia la izquierda (menor) o hacia la derecha (mayor) hasta alcanzar el nivel deseado. El valor predeterminado es 20 (rango 0–100). Un valor más alto requiere una señal más fuerte para abrir el squelch.
3. Haga clic en **SQL** para activar el squelch. El botón se ilumina cuando está activo.
4. Para desactivar el squelch, haga clic en **SQL** nuevamente.

## Qué hace cada control

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **SQL** | Off | On / Off | Activa el squelch en el nivel actual del control deslizante. El audio se silencia hasta que la señal supere el umbral. |
| Control deslizante de nivel de squelch | 20 | 0–100 | Establece el umbral de squelch. No tiene efecto a menos que **SQL** esté activado. |

## Consejos

- Ajuste el umbral mientras la banda está en silencio. Suba el control deslizante hasta que el audio se corte, luego retroceda ligeramente para que las señales débiles todavía abran el squelch.
- El control deslizante de nivel de squelch puede ajustarse mientras **SQL** ya está activado; los cambios surten efecto de inmediato.

## Solución de problemas

- **El audio está en silencio aunque SQL esté desactivado** — Verifique el botón de silencio 🔊 / 🔇. Si el slice está silenciado, el audio permanecerá en silencio independientemente del estado del squelch. Haga clic en el botón de silencio para reactivar el audio.
- **SQL está activado pero el audio nunca se abre** — El control deslizante de nivel de squelch puede estar ajustado demasiado alto. Arrástrelo hacia 0 hasta que el audio pase, luego súbalo gradualmente para encontrar el umbral correcto.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
