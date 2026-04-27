# Establecer la frecuencia de corte inferior del audio TX

Use el control Low Cut en el applet Phone para elevar el límite inferior de la banda de paso del audio TX, eliminando ruidos de baja frecuencia, ruido de respiración o interferencias de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone requiere una conexión activa con el radio.
- Asegúrese de que el panel de applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área de filtro TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte inferior en 50 Hz, o en **>** para aumentarla en 50 Hz. También puede desplazar la rueda del ratón sobre el indicador de valor para avanzar en cualquier dirección.
4. Lea el valor actual en el indicador numérico entre los dos botones. El valor predeterminado es **50 Hz**.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **Low Cut** **<** | — | — | Disminuye la frecuencia de corte inferior del filtro TX en 50 Hz por clic. |
| **Low Cut** **>** | — | — | Aumenta la frecuencia de corte inferior del filtro TX en 50 Hz por clic. |
| Indicador de valor Low Cut | 50 Hz | 0 Hz a (corte superior − 50 Hz), paso de 50 Hz | Muestra la frecuencia de corte inferior actual. También acepta entrada mediante la rueda del ratón. |

## Consejos

- El valor de corte inferior no puede establecerse por encima de la frecuencia de corte superior actual menos 50 Hz. Si está cerca de ese límite, primero reduzca el corte superior o auméntelo para crear margen.
- Para voz en SSB, un corte inferior típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.

## Solución de problemas

- **Los botones Low Cut no responden** — Confirme que el radio está conectado. Los controles del filtro TX requieren una conexión activa con el radio para enviar los cambios de filtro al FLEX-8600.

## Temas relacionados

- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)
