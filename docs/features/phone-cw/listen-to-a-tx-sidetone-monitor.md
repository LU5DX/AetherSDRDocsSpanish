# Escuchar el monitor de sidetone de TX

El applet Phone/CW permite escuchar el audio transmitido a través de los altavoces o auriculares de su computadora mientras transmite. Esto es útil para verificar la calidad y los niveles de audio sin necesidad de un segundo receptor.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW no está disponible sin una conexión activa al radio.
- El slice activo debe estar en un modo de fono (SSB, AM, FM). En modo CW, el applet cambia al panel CW, que tiene un control de sidetone independiente — consulte [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md).
- Confirme que el applet P/CW sea visible en el Panel de Applets de la barra lateral derecha. Si no está visible, haga clic en el botón de bandeja **P/CW** para mostrarlo.

## Pasos

1. En el applet Phone/CW, localice el botón de alternancia **MON**.
2. Haga clic en **MON** para activar el monitor de sidetone de TX. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante **Monitor volume** para establecer el nivel de escucha. El rango es 0–100.
4. Transmita normalmente. Escuchará el audio transmitido al volumen establecido por el control deslizante **Monitor volume**.
5. Para desactivar el monitoreo, haga clic en **MON** nuevamente. El botón regresa a su estado inactivo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|---|
| **MON** | Botón de alternancia | Activa o desactiva el monitor de sidetone de TX. | — | On / Off | — |
| **Monitor volume** | Control deslizante | Establece el volumen de reproducción del monitor de banda lateral. | — | 0–100 | — |

## Consejos

- El control deslizante **Monitor volume** es independiente del nivel de salida de audio principal del radio. Puede ajustarlo sin afectar el audio de recepción.
- Si está usando la fuente de micrófono **PC**, el valor de ganancia del micrófono se almacena en el lado del cliente como `PcMicGain` (predeterminado 50, rango 0–100). El radio no devuelve este valor, por lo que la posición del control deslizante en el applet es el valor de referencia.

## Solución de problemas

- **MON está activo pero no se escucha audio durante la transmisión** — Confirme que el control deslizante **Monitor volume** no esté en 0. Verifique también que el dispositivo de salida de audio del sistema esté correctamente configurado.
- **El botón MON no es visible** — Es posible que el applet esté mostrando el panel CW en lugar del panel Phone. MON es un control exclusivo del modo fono. Cambie el slice activo a un modo de fono (SSB, AM o FM) para restaurar el panel Phone.

## Relacionados

- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
