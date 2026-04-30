# Establezca la frecuencia de corte bajo del audio de TX

Use el control Low Cut en el applet Phone para elevar el borde inferior de la banda de paso del audio de TX, eliminando ronquera, ruido de respiración o interferencia de baja frecuencia de su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el Applet Panel esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área de filtro TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte bajo en 50 Hz, o en **>** para aumentarla en 50 Hz. También puede desplazar la rueda del ratón sobre la pantalla de valor para cambiar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Qué hace cada control

| Control               | Predeterminado | Rango válido                            |
|-----------------------|----------------|-----------------------------------------|
| **Low Cut** **<**     | —              | —                                       |
| **Low Cut** **>**     | —              | —                                       |
| Pantalla de valor Low Cut | 50 Hz   | 0 Hz a (high-cut − 50 Hz), paso 50 Hz |

## Consejos

- El valor de corte bajo no puede establecerse más alto que la frecuencia de corte alto actual menos 50 Hz. Si se encuentra cerca de ese límite, primero baje el corte alto o auméntelo para crear espacio.
- Para voz SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.

## Solución de problemas

- **Los botones Low Cut no funcionan** — Confirme que la radio esté conectada. Los controles de filtro TX requieren una conexión de radio activa para enviar cambios de filtro al FLEX-8600.

## Relacionado

- [Establezca la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Habilite VOX y establezca el umbral de activación](enable-vox-and-set-trigger-threshold.md)
