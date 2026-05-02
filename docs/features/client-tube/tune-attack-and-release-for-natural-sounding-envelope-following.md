# Ajustar Attack y Release para un seguimiento de envolvente de sonido natural

Attack y Release determinan la rapidez con que el seguidor de envolvente rastrea los niveles de señal ascendentes y descendentes. Solo tienen efecto cuando Envelope tiene un valor distinto de cero. Girar estos dos mandos evita que el carácter de tubo se active y desactive de forma abrupta durante el habla o los transitorios de audio.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).
- Envelope debe tener un valor distinto de cero. Attack y Release no producen ningún efecto audible al 0 %. Consulte [Usar Envelope para agregar drive dinámico en transitorios](use-envelope-to-add-dynamic-drive-on-transients.md).
- Abra el editor flotante del lado que desea ajustar: haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX.
2. Localice el mando Attack en la columna derecha del editor.
3. Ajuste Attack para establecer la rapidez con que el seguidor de envolvente responde cuando los niveles de señal suben. Los valores más bajos hacen que el seguidor reaccione más rápido ante los transitorios; los valores más altos suavizan los picos cortos.
4. Localice el mando Release directamente debajo de Attack en la columna derecha.
5. Ajuste Release para establecer la rapidez con que el seguidor se recupera después de que los niveles bajen. Los valores más bajos regresan al drive de reposo más rápido; los valores más altos permiten que el efecto se prolongue después de un pico.
6. Observe la curva de transferencia y la bola de entrada en tiempo real mientras transmite o recibe para confirmar que la modulación del drive se ve natural.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente (TX / RX) |
|---|---|---|---|
| Attack | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` |
| Release | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` |

**Attack** — Utiliza mapeo exponencial en todo su rango. Establece la rapidez con que el seguidor de envolvente responde a los niveles de señal ascendentes cuando Envelope ≠ 0. La etiqueta se muestra como "X.XX ms" por debajo de 10 ms y "X.X ms" por encima de 10 ms.

**Release** — Utiliza mapeo exponencial en todo su rango. Establece la rapidez con que el seguidor de envolvente se recupera después de que los niveles de señal caen cuando Envelope ≠ 0. La etiqueta se muestra como "X.XX ms" por debajo de 100 ms y "X.X ms" por encima de 100 ms.

## Consejos

- Attack y Release son independientes por lado. Los cambios realizados en el editor TX no afectan al editor RX y viceversa.
- Para un sonido de voz natural en TX, comience con los valores predeterminados (Attack 5.00 ms, Release 35.00 ms) y alargue primero Release. Los valores de Release muy cortos pueden producir un carácter de bombeo o traqueteo.
- Para el modelado de tono en RX, un Attack más largo (10 ms o más) permite que los picos transitorios pasen antes de que el seguidor de envolvente se active, lo que preserva las consonantes iniciales del audio recibido.
- La bola de entrada en tiempo real sobre la curva de transferencia se mueve en tiempo real. Con Envelope activo, puede ver cómo el punto de operación se desplaza a medida que cambian los niveles, lo que ayuda a confirmar que Attack y Release se sienten correctos antes de salir al aire.

## Solución de problemas

- **Ajustar Attack o Release no produce ningún efecto audible** — Es probable que Envelope esté en 0 %. Primero establezca Envelope en un valor positivo o negativo; Attack y Release solo se aplican cuando el seguidor de envolvente está activo.
- **El efecto suena demasiado abrupto o entrecortado** — Release está configurado demasiado bajo. Aumente Release hacia 100 ms o más para suavizar la recuperación.
- **Los picos fuertes hacen que el drive se active bruscamente** — Attack está configurado demasiado bajo. Aumente Attack a 10–20 ms para ralentizar la respuesta del seguidor ante los transitorios.

## Relacionados

- [Usar Envelope para agregar drive dinámico en transitorios](use-envelope-to-add-dynamic-drive-on-transients.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Omitir el tubo desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
- [Supervisar el recorte de salida con el medidor de nivel en el editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
