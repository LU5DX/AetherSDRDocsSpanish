# Ajustar la potencia de salida de RF

Use el control deslizante **RF Power** del applet TX Controls para establecer el nivel de potencia de transmisión enviado a la antena. Ajuste este valor antes de transmitir para evitar sobrecargar su amplificador o exceder los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no lo está, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón de bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls. Aparece debajo del indicador **SWR**.
2. Arrastre el control deslizante hacia la izquierda o la derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control se actualiza de inmediato.
3. Confirme que el valor mostrado en la lectura es el que desea. El indicador **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control                    | Descripción                                                             | Predeterminado |
|----------------------------|-------------------------------------------------------------------------|----------------|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. | 100            |
| Medidor **RF Pwr**         | Muestra la potencia directa real en la salida del excitador.            | —              |
| Medidor **SWR**            | Muestra la relación de onda estacionaria en el excitador.               | —              |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de radio. En un FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda de forma independiente a este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de ajuste y los ajustes de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador externo independiente. Si está usando un amplificador externo, ajuste este control al nivel de excitación que espera su amplificador.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en la versión v0.9.5.1 para reflejar el funcionamiento por frecuencia encontrado en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de ajuste del ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya reporta una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado de frecuencia desde el último ajuste, hacer clic en **ATU** nuevamente pone el sintonizador en bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de ajuste, aunque el estado anterior haya sido exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando una coincidencia está activa. El indicador **Mem** se ilumina en verde cuando el sintonizador está usando una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin ajuste previo, o la frecuencia ha cambiado | Inicia el ciclo de ajuste |
| Coincidencia exitosa, misma frecuencia que el último ajuste | Cambia a bypass |
| Bypass activo | Inicia un nuevo ciclo de ajuste en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transverter TGXL está en modo OPERATE.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio está efectivamente activada. Verifique que MOX esté activo (el botón **MOX** está en rojo) o que su línea PTT esté afirmada. También verifique que el control deslizante **RF Power** no esté en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — Es posible que la conexión con la radio se haya perdido. Verifique el estado de la conexión y reconéctese mediante `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia un nuevo ciclo de ajuste aunque Success estaba encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde el último ajuste. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de ajuste.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Ajustar la potencia del portador de ajuste](set-tune-carrier-power.md)
- [Iniciar un portador de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (por ejemplo, SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
