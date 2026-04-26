# Activar el silenciador (squelch) y ajustar su umbral

El squelch silencia el audio del slice cuando la señal recibida cae por debajo de un nivel establecido. Esto es útil en FM, AM o cualquier modo en el que desee que el altavoz permanezca en silencio entre transmisiones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- El applet RX Controls debe estar visible. Si no lo está, haga clic en el botón RX tray en la barra lateral derecha para mostrarlo.

## Pasos

1. En el applet RX Controls, seleccione el slice que desea ajustar haciendo clic en su pestaña (de A a H) si hay más de un slice activo.
2. Mueva el control deslizante de nivel de squelch para establecer el umbral. El valor predeterminado es 20 y el rango válido es 0–100. Un valor más alto significa que la señal debe ser más fuerte para abrir el squelch.
3. Haga clic en SQL para activar el squelch. El botón se resalta cuando el squelch está activo.
4. Ajuste el control deslizante de nivel de squelch hasta que el audio se abra de forma confiable en las señales que desea escuchar y se cierre entre ellas.
5. Para desactivar el squelch, haga clic en SQL nuevamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| SQL | Desactivado | Activado / Desactivado | Activa el squelch en el nivel actual del control deslizante. El audio se silencia cuando la señal está por debajo del umbral. |
| Nivel de squelch | 20 | 0–100 | Establece el umbral del squelch. Solo tiene efecto cuando SQL está activado. Los valores más altos requieren una señal más fuerte para abrir el squelch. |

## Consejos

- Ajuste el control deslizante de nivel de squelch antes de hacer clic en SQL para que el audio no se corte mientras realiza el ajuste.
- Si no puede encontrar un nivel que se abra de forma confiable en señales débiles pero permanezca cerrado con el ruido, intente reducir el valor hacia 0 en pequeños incrementos.
- El control deslizante de nivel de squelch no tiene efecto cuando SQL está desactivado.

## Solución de problemas

- **El audio permanece silenciado después de hacer clic en SQL** — El nivel de squelch está configurado demasiado alto para la señal entrante. Reduzca el control deslizante de nivel de squelch hasta que el audio se abra.
- **El squelch nunca se cierra con el ruido** — El nivel de squelch es demasiado bajo. Aumente el valor del control deslizante hasta que el audio se silencie entre transmisiones.

## Temas relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Trabajar con un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
