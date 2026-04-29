# Inspeccionar la curva de EQ de RX y el espectro en vivo

El applet "Aetherial RX EQ" ofrece una vista compacta y siempre visible de la respuesta en frecuencia sumada del ecualizador de RX y una superposición del analizador FFT en tiempo real del audio que pasa por la cadena de RX. Úselo para monitorear el efecto de sus ajustes de EQ de RX de un vistazo, sin necesidad de abrir el editor completo.

## Antes de comenzar

- El subcontenedor "Aetherial RX EQ" permanece oculto hasta que la etapa de EQ de RX esté habilitada. Habilítela desde el widget CHAIN o desde el editor flotante antes de esperar que el applet aparezca.
- El applet se encuentra dentro del contenedor padre "Aetherial Audio (TXDSP)" en el panel de applets. Asegúrese de que el panel de applets esté visible (`View > Applet Panel`).

## Pasos

1. En el panel de applets, localice el contenedor padre "Aetherial Audio (TXDSP)".
2. Expándalo y busque el subcontenedor "Aetherial RX EQ".
3. Observe el área del analizador/curva: la pantalla de 110 px de altura que muestra la cuadrícula de frecuencias.
4. La curva de respuesta de EQ sumada muestra la respuesta en frecuencia acumulada de todas las bandas de RX habilitadas. Una línea plana indica que no hay modelado neto; una línea con forma refleja los ajustes de banda activos almacenados en `ClientEqRxBands`.
5. La superposición del analizador en vivo que se extiende por la misma área muestra la FFT en tiempo real del audio que pasa por la cadena de RX. Cuando hay audio presente, la superposición está activa; cuando no pasa audio, la superposición está inactiva.
6. La traza de retención de pico aparece como una línea blanco apagado dibujada sobre la superposición del analizador. Registra el nivel máximo visto por frecuencia y decae a aproximadamente 10 dB/sec entre actualizaciones. Úsela para detectar resonancias y picos agresivos durante el ajuste.
7. Para inspeccionar con mayor detalle o editar bandas, haga doble clic en la etapa de EQ de RX en el widget CHAIN para abrir el editor flotante "Aetherial Parametric EQ — RX".

## Qué hace cada control

| Control                        | Comportamiento                                                                                                                                                                                                                                                                                                                                            | Predeterminado |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Área del analizador/curva     | Muestra la curva de respuesta de EQ sumada, la superposición del analizador FFT en vivo y la traza de retención de pico para la cadena de RX. Solo lectura en este applet.                                                                                                                                                                               | —              |
| Respuesta de EQ sumada        | Muestra la respuesta en frecuencia acumulada de todas las bandas de RX habilitadas. Se atenúa en gris cuando la etapa de EQ está en bypass.                                                                                                                                                                                                              | plana          |
| Superposición del analizador en vivo | FFT en tiempo real del audio que pasa por la cadena de RX, mostrada como un relleno degradado en cian.                                                                                                                                                                                                                                             | inactiva       |
| Traza de retención de pico    | Línea blanco apagado superpuesta al analizador que muestra el nivel máximo visto por frecuencia desde el último reinicio. Decae a aproximadamente 10 dB/sec durante el funcionamiento normal. Se congela en el nivel máximo observado por bin cuando Peak Hold está habilitado en el editor flotante. Ayuda a identificar resonancias y picos agresivos durante el ajuste. | decayendo      |
| Estado habilitado del EQ de RX | Indica si la etapa de EQ de RX está activa. Se controla desde el widget CHAIN o el editor flotante, no desde este applet.                                                                                                                                                                                                                                | —              |
| Peak Hold                     | Botón de alternancia en la barra de encabezado del editor flotante. Cuando está activado (fondo ámbar), la traza de retención de pico deja de decaer: el nivel máximo observado de cada frecuencia se mantiene hasta que se desactive el botón. Desactívelo para reanudar el decaimiento normal. Se encuentra solo en el editor flotante, no en el tile del applet acoplado. | desactivado    |
| Filter family                 | Cuadro combinado en la barra de encabezado del editor flotante. Selecciona las matemáticas de la cascada HP/LP: Butterworth (banda de paso máximamente plana), Chebyshev (caída más pronunciada con rizado de 1 dB en la banda de paso), Bessel (fase lineal / caída más suave) o Elliptic (transición más pronunciada con rizado en ambas bandas). Se aplica solo a los tipos de filtro HP y LP; las bandas de pico y de estante usan su propia topología fija de segundo orden independientemente. Se almacena como `ClientEqRxFilterFamily`. | Butterworth    |
| Reset                         | Botón en la barra de encabezado del editor flotante. Restablece todas las bandas a la plantilla predeterminada de 10 bandas, restaura el número de bandas predeterminado y restablece la familia de filtros a Butterworth. Se guarda inmediatamente. Información de herramienta: "Reset all bands to default values". Se encuentra solo en el editor flotante.  | —              |
| Output Fader                  | Fader vertical combinado con medidor de nivel en el borde derecho del editor flotante. Arrástrelo para ajustar la ganancia maestra post-EQ; la rueda del ratón ajusta en pasos de 0.5 dB; el doble clic restablece a 0 dB. La barra de nivel detrás del control muestra el pico post-EQ suavizado en tiempo real con el mismo degradado verde-ámbar-rojo que el medidor de nivel Tube. Se almacena como `ClientEqRxMasterGain`. Información de herramienta: "Output gain (dB). Drag to set, wheel for fine step, double-click to reset to 0 dB." Se encuentra solo en el editor flotante, no en el tile del applet acoplado. | 0 dB           |

## Consejos

- El área del analizador/curva es de solo lectura en el applet. Para agregar, eliminar o ajustar bandas, abra el editor flotante haciendo doble clic en la etapa de EQ de RX en el widget CHAIN.
- Para congelar la traza de retención de pico mientras ajusta una resonancia, abra el editor flotante y haga clic en **Peak Hold**. El fondo del botón se torna ámbar cuando está activo. Haga clic de nuevo para reanudar el decaimiento normal.
- Use el botón **Reset** en el editor flotante para devolver todas las bandas, el número de bandas y la familia de filtros a sus valores predeterminados en un solo paso. El reinicio se guarda inmediatamente.
- El ajuste de **Filter family** afecta únicamente a los tipos de banda HP y LP. Las bandas de pico y de estante siempre usan una topología fija de segundo orden independientemente de este ajuste.
- Si desea hacer flotante, extraer u ocultar el subcontenedor "Aetherial RX EQ", haga clic derecho en su barra de título para acceder a esas opciones.

## Solución de problemas

- **El subcontenedor "Aetherial RX EQ" no es visible** — El applet permanece oculto hasta que la etapa de EQ de RX esté habilitada. Habilite la etapa desde el widget CHAIN o el editor flotante. Verifique que `ClientEqRxEnabled` esté configurado.
- **La superposición del analizador en vivo aparece inactiva incluso durante la recepción** — El audio debe pasar por la cadena de RX para que la FFT funcione. Confirme que el radio esté conectado y que el enrutamiento de audio esté activo.
- **La traza de retención de pico no se mueve ni decae** — Verifique que **Peak Hold** no esté habilitado en el editor flotante. Si el botón tiene fondo ámbar, haga clic en él para reanudar el decaimiento normal.

## Relacionado

- [Descripción general de Aetherial Parametric EQ (TX / RX)](overview.md)
- [Inspeccionar la curva de EQ de TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Poner en bypass la etapa de EQ desde la cadena](bypass-the-eq-stage-from-the-chain.md)
- [Abrir el editor sin marco para agregar, eliminar o ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
