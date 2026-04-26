# Ajustar la ganancia de recepción DAX por canal

Use el applet DAX Audio para ajustar la ganancia de recepción en cada uno de los cuatro canales DAX. Los cambios de ganancia surten efecto de inmediato y se conservan entre sesiones.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- Habilite DAX haciendo clic en Enable en el applet DAX Audio. Los controles deslizantes de ganancia están presentes en todo momento, pero el audio no fluirá hasta que DAX esté en ejecución.

## Pasos

1. Haga clic en el botón DAX del panel lateral derecho para abrir el applet DAX Audio.
2. Localice la fila del canal que desea ajustar: **DAX 1**, **DAX 2**, **DAX 3** o **DAX 4**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda o la derecha para establecer la ganancia de RX. Arrastrar hacia la izquierda disminuye la ganancia; arrastrar hacia la derecha la aumenta.
4. Suelte para confirmar. El valor se guarda automáticamente.

Repita el procedimiento para cualquier otro canal que desee ajustar.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistente |
|---|---|---|---|
| Ganancia+medidor DAX 1 | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Estado de asignación de slice | — | — o Slice A–H | (ninguno) |

Cada medidor/deslizador es un control combinado: la barra de fondo muestra el nivel de recepción RMS suavizado (post-fader, es decir, refleja la salida efectiva después de su ajuste de ganancia), y el cursor arrastrable establece la ganancia. Los valores de ganancia se almacenan con dos decimales, por ejemplo `0.75`.

El indicador de asignación de slice a la izquierda de cada medidor muestra qué slice está enrutado actualmente a ese canal DAX. Muestra — cuando no hay ningún slice asignado.

## Sugerencias

- El medidor de nivel usa balística post-fader, lo que significa que la barra refleja el nivel de salida real después de su ajuste de ganancia. Si arrastra el cursor a cero, la barra del medidor desaparece aunque haya audio presente.
- Los valores de ganancia persisten entre sesiones. No es necesario reajustarlos después de reiniciar AetherSDR.

## Solución de problemas

- **Arrastrar el deslizador no produce ningún efecto audible** — Confirme que Enable está activo (el botón aparece resaltado). Si DAX no está en ejecución, la ganancia se almacena pero no fluye audio.
- **La barra del medidor no se mueve** — Compruebe que hay un slice asignado al canal. El indicador de asignación de slice muestra — si no hay ningún slice enrutado allí. Consulte [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md).

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia de transmisión DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Iniciar DAX automáticamente al arrancar](autostart-dax-on-launch.md)
