# Cambiar a una referencia externa de 10 MHz

Use esta página para seleccionar una señal de referencia externa de 10 MHz como estándar de frecuencia del FLEX-8600. Esto es útil cuando tiene un oscilador disciplinado por GPS, un patrón de rubidio u otra referencia de precisión conectada al puerto REF IN del panel trasero del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Radio Setup requiere una conexión activa con el radio.
- La fuente de referencia externa de 10 MHz debe estar conectada al conector REF IN del panel trasero del radio y debe estar activa antes de cambiar la configuración.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **RX**.
3. Localice el cuadro combinado **10 MHz Reference Source:**.
4. Seleccione **External** en la lista desplegable.
5. Haga clic en **Close** para cerrar el diálogo.

Para volver al oscilador interno, repita los pasos y seleccione **Internal**.

## Qué hace cada control

| Control | Tipo | Valores válidos | Comportamiento |
|---|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | `Internal`, `External` | Selecciona si el radio sincroniza su reloj de muestreo con el oscilador interno o con una señal de 10 MHz presente en el conector REF IN. |

## Consejos

- La pestaña **RX** también contiene los controles de calibración del GPSDO (**Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):**). Si utiliza un oscilador disciplinado por GPS como referencia externa, no es necesario aplicar también un desplazamiento de frecuencia manual — el GPSDO mantiene la frecuencia.

## Solución de problemas

- **La indicación de frecuencia se vuelve inestable o el radio deja de recibir tras cambiar a External** — La referencia externa está ausente, su nivel es demasiado bajo o no es exactamente 10 MHz. Verifique que la fuente esté en funcionamiento y correctamente cableada; luego vuelva a **Internal** para restablecer la operación normal.

## Temas relacionados

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Descripción general de Radio Setup](overview.md)
