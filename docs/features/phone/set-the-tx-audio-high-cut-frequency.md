# Establecer la frecuencia de corte alto de audio TX

Use el applet Phone para subir o bajar el límite superior de la banda de paso de audio TX. Reducir el corte alto elimina el silbido de alta frecuencia; ampliarlo mejora la fidelidad de audio en los modos que lo permiten.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el panel del applet esté visible. Si no lo está, haga clic en el botón PHNE de la bandeja en la barra lateral derecha, o vaya a `View > Applet Panel`.

## Pasos

1. Haga clic en el botón **PHNE** de la bandeja en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **High Cut** en el área de filtro TX en la parte inferior del applet.
3. Haga clic en **>** para aumentar la frecuencia de corte alto en 50 Hz, o haga clic en **<** para disminuirla en 50 Hz.
   - Alternativamente, coloque el cursor sobre el valor de frecuencia y gire la rueda del ratón para ajustar en los mismos incrementos de 50 Hz.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|
| **High Cut `<`** | — | Disminuye en pasos de 50 Hz | No puede bajar de (corte bajo + 50) Hz |
| **High Cut `>`** | — | Aumenta en pasos de 50 Hz | El límite superior es 10000 Hz |
| Pantalla de valor High Cut | 3300 Hz | (corte bajo + 50) a 10000, paso de 50 Hz | Pantalla numérica de solo lectura; también acepta la rueda del ratón |

## Consejos

- El límite inferior del corte alto es siempre 50 Hz por encima del valor actual del corte bajo. Si el corte alto no puede bajar más, disminuya primero el corte bajo.
- Para voz SSB estándar, un corte alto de 2800–3000 Hz reduce las interferencias en los canales adyacentes y mantiene la voz inteligible.

## Relacionado

- [Establecer la frecuencia de corte bajo de audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
