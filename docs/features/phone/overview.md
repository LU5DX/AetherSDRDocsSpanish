# Descripción general del applet Phone

El applet Phone agrupa todos los controles de transmisión de voz en un solo lugar: nivel de portadora AM, VOX, puerta de ruido por expansión descendente (DEXP) y frecuencias de corte del filtro de audio TX. Ábralo cuando necesite ajustar la forma en que se procesa su audio transmitido o cuando desee configurar la transmisión activada por voz.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone requiere una conexión de radio activa.
- El applet es visible en el Panel de applets (barra lateral derecha). Si el panel está oculto, haga clic en el botón de bandeja PHNE en la barra lateral derecha, o actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet Phone siempre está presente en el Panel de applets. Alterne su visibilidad con el botón de bandeja PHNE. Los controles se envían directamente al radio en tiempo real; el applet refleja el estado actual del radio cuando hay una conexión activa.

**Limitación de DEXP:** El botón de alternancia de DEXP y el control deslizante de umbral DEXP están presentes en la interfaz, pero en el firmware v1.4.0.0 (protocolo SmartSDR v1.4.0.0), el radio devuelve un error cuando se envían estos comandos. Los ajustes de DEXP (`DexpEnabled`, `DexpLevel`) son guardados localmente por AetherSDR, pero no tienen efecto en el radio hasta que se resuelva esta limitación del firmware.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|---|
| AM Carrier | Control deslizante | — | 0–100 | — | Establece el nivel de potencia de la portadora AM. El valor actual aparece como número a la derecha del control deslizante (p. ej., `48`). |
| VOX | Botón de alternancia | — | On / Off | — | Activa o desactiva la transmisión activada por voz. Cuando está activado, el audio por encima del umbral de nivel VOX dispara la transmisión (TX). |
| VOX level | Control deslizante | — | 0–100 | — | Establece el umbral de activación del VOX. Valores más altos requieren audio más fuerte para disparar la transmisión. |
| Delay | Control deslizante | — | 0–100 | — | Establece el tiempo de retención del VOX: cuánto tiempo permanece el radio en TX después de que el audio cae por debajo del umbral antes de volver a recepción. |
| DEXP | Botón de alternancia | — | On / Off | `DexpEnabled` | Activa o desactiva la puerta de ruido por expansión descendente. No funcional en el firmware v1.4.0.0. |
| DEXP threshold | Control deslizante | 0 | 0–100 | `DexpLevel` | Establece el umbral de la puerta DEXP. No funcional en el firmware v1.4.0.0. |
| Low Cut `<` / `>` | Spinbox | 50 Hz | 0 a (corte alto − 50 Hz), paso 50 Hz | — | Ajusta la frecuencia de corte inferior del filtro de audio TX. Haga clic en `<` o `>`, o use la rueda del ratón. |
| High Cut `<` / `>` | Spinbox | 3300 Hz | (corte bajo + 50 Hz) a 10000 Hz, paso 50 Hz | — | Ajusta la frecuencia de corte superior del filtro de audio TX. Haga clic en `<` o `>`, o use la rueda del ratón. |

## Consejos

- Los spinboxes Low Cut y High Cut imponen una separación mínima de 50 Hz entre ambos valores. Al acercar un límite al otro, el ajuste se detendrá en esa frontera.
- `DexpEnabled` y `DexpLevel` se guardan en la configuración local de AetherSDR cada vez que los modifica, de modo que sus valores deseados quedan preservados para cuando el firmware los soporte.

## Solución de problemas

- **El botón de alternancia DEXP o el umbral no tienen efecto en el radio** — Esta es una limitación conocida del firmware en v1.4.0.0. El radio devuelve el error 0x5000002D para estos comandos. Sus ajustes se almacenan localmente, pero no se aplican al radio.
- **El applet Phone no es visible** — Haga clic en el botón de bandeja PHNE en la barra lateral derecha, o verifique que `View > Applet Panel` esté habilitado.

## Temas relacionados

- [Ajustar la potencia de la portadora AM para transmisión en AM](adjust-am-carrier-power-for-am-transmit.md)
- [Activar el VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)
- [Ajustar el tiempo de retención del VOX](tune-vox-hang-time.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
