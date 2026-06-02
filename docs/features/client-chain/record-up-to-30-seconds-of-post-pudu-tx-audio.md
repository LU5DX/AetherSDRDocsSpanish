# Cadena de Audio Aetherial

El applet de la Cadena de Audio Aetherial muestra el flujo de señal DSP del lado del cliente como una tira horizontal de etapas, con cadenas TX y RX independientes. La cadena TX incluye EQ Paramétrico, Compresor (con Drive previo al compresor y reducción de PAPR con rotador de fase), Puerta, De-Ess (de bandas divididas, pendiente seleccionable de 12–48 dB/oct), Tube (con conmutación de reducción de ruido RN2 en TX), excitador PUDU, Reverb. La cadena RX incluye EQ, AGC-G (puerta), AGC-C (compresor), DESS (de-esser), TUBE, EVO (pudu); las seis etapas RX están completamente implementadas, enmarcadas por los mosaicos de estado RADIO / ADSP / SPEAK. El mosaico ADSP es un conmutador con clic que desvía todo el clúster NR del lado del cliente (NR2 / NR4 / MNR / DFNR / RN2 / BNR); una instantánea en memoria restaura el estado NR anterior al reactivarlo.

## Grabe hasta 30 segundos de audio TX posterior a PUDU

Utilice el grabador de monitor incorporado para capturar y reproducir inmediatamente cómo suena su audio transmitido después de pasar por toda la cadena DSP TX, incluido PUDU. Esto le ayuda a ajustar la configuración de su cadena sin necesidad de una segunda estación que le informe.

### Antes de comenzar

- El applet de la Cadena de Audio Aetherial debe estar abierto. Si no es visible, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha.
- Su entrada de micrófono debe estar configurada en **PC** (no en una fuente de micrófono del panel frontal del radio).
- DAX debe estar desactivado. La información sobre herramientas del botón de grabar dice: "MIC must be set to PC and DAX off."
- La pestaña **TX** debe estar activa en el applet. Los controles de grabación están ocultos cuando se selecciona **RX**.

### Pasos

1. Haga clic en el botón de la pestaña **TX** en la parte superior del applet de la Cadena de Audio Aetherial para asegurarse de que se muestre la cadena TX. El botón se vuelve ámbar cuando está seleccionado.
2. Confirme que el botón de grabar (⏺) esté habilitado. Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está en curso. Si aparece atenuado y no se puede hacer clic, verifique que la fuente del micrófono esté configurada en PC y que DAX esté desactivado.
3. Haga clic en **⏺** para iniciar la grabación. El botón parpadea en rojo para indicar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos, o puede detenerla antes.
4. Para detener la grabación antes de que hayan transcurrido 30 segundos, haga clic en **⏺** nuevamente. La reproducción comienza automáticamente una vez que se detiene la grabación.
5. Para cancelar la reproducción antes de que termine, haga clic en **▶** mientras parpadea en verde.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| Botones de alternancia **TX** / **RX** | TX está marcado | Par exclusivo; muestra y edita la cadena DSP correspondiente. La última pestaña activa persiste mediante `PooDooAudioActiveTab='TX'` / `'RX'`. |
| **BYPASS** | Sin marcar | Toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas (incluido RN2). Desmarque para reactivar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. El estado visual marcado sigue el lado que se muestra actualmente. El alcance es global (por motor de audio), no por perfil; el botón permanece presionado al cambiar de perfil de Channel Strip. |
| **⏺** (grabar) | Sin marcar | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic nuevamente para detener; la reproducción comienza automáticamente. Oculto en modo RX. Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está en curso. Parpadea en rojo mientras graba. |
| **▶** (reproducir) | Sin marcar | Reproduce el audio PUDU capturado. Haga clic nuevamente para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce. |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | N/A | Un solo clic alterna el bypass de la etapa; un doble clic abre su editor flotante sin marco (o el Channel Strip en TX); arrastrar reordena la cadena TX. Texto de sugerencia: "Click to bypass · Double click to edit · Drag to reorder". |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | N/A | Un solo clic alterna el bypass de la etapa RX; un doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas RX están completamente implementadas. El orden es independiente de la cadena TX. Un tipo mime distintivo `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |
| Mosaico de estado **RADIO** | Siempre visible en modo RX | Se vuelve verde cuando PC Audio (flujo SSB estándar) está habilitado. No interactivo. |
| Mosaico de estado/bypass **ADSP** | Sin marcar | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic desvía todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Un doble clic abre el diálogo de Configuración de AetherDSP. |
| Mosaico de estado **SPEAK** | Siempre visible en modo RX | Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. No interactivo. |

## Ajustes de interacción

El intervalo de discriminación de clic utilizado para distinguir un solo clic de un doble clic es configurable a través del diálogo **Ajustes de Interacción**. De forma predeterminada, AetherSDR utiliza el intervalo de doble clic del sistema, pero puede ajustarlo según su preferencia. Esta configuración afecta tanto a los widgets de la cadena TX como a los de la cadena RX.

Para ajustar el intervalo:

1. Abra **File > Settings**.
2. Seleccione **Interaction** en la barra lateral.
3. Ajuste el control deslizante **Click discrimination interval**.
4. Haga clic en **Apply**.

## Abrir el editor DSP TX desde la cadena

Hacer doble clic en cualquier mosaico de etapa de la cadena TX abre el Channel Strip de Audio Aetherial, la ventana unificada de DSP TX. El Channel Strip proporciona acceso a todos los editores de etapas individuales a través de sus propios controles. Este gesto de doble clic es la forma estándar de abrir la configuración de audio TX desde el applet de la cadena.

## Sincronización de BYPASS TX y RX

El botón **BYPASS** en el applet de la Cadena de Audio Aetherial y el botón **BYPASS** en el Channel Strip de Audio Aetherial comparten un único estado de bypass propiedad del motor para cada lado. Presionar cualquiera de los botones actualiza ambos. Cuando cambia entre las pestañas **TX** y **RX**, el botón **BYPASS** refleja inmediatamente el estado actual del motor para el lado activo.

## Consejos

- El grabador captura audio en el punto posterior a la etapa PUDU en la cadena TX. Para escuchar el efecto de una etapa específica, desvíe o active esa etapa, haga una grabación y compare la reproducción.
- No necesita transmitir a un receptor; el monitor graba el audio directamente desde la salida DSP del lado del cliente.
- Si desea comparar configuraciones, detenga la grabación actual, ajuste una etapa, grabe nuevamente y reproduzca para comparar.
- Para ajustar la configuración de una etapa TX individual, haga doble clic en cualquier mosaico de etapa en la cadena TX. Se abre el Channel Strip de Audio Aetherial; use sus controles para editar cada etapa.

## Solución de problemas

- **El botón ⏺ está atenuado y no se puede hacer clic** — La entrada del micrófono no está configurada en PC, DAX está activado o la reproducción está en curso. Desactive DAX, configure la fuente del micrófono en PC y espere a que termine cualquier reproducción activa.
- **Los botones ⏺ y ▶ no son visibles** — La pestaña **RX** está activa. Haga clic en **TX** para cambiar a la cadena TX; ambos botones están ocultos en modo RX.
- **La reproducción no comienza después de que se detiene la grabación** — No se capturó audio. Confirme que su entrada de micrófono esté entregando audio a la PC durante la ventana de grabación.
- **Hacer doble clic en un mosaico de etapa TX no abre un editor flotante** — Este es un comportamiento esperado. Hacer doble clic abre el Channel Strip de Audio Aetherial. Acceda a los editores de etapas individuales desde dentro del Channel Strip.
- **El estado del botón BYPASS no coincide con lo que configuré en el Channel Strip** — Si acaba de conectar el motor de audio, recargue el applet o cambie a otra pestaña y vuelva a la pestaña activa para que el botón pueda releer el estado actual del motor.
- **Las acciones de doble clic se sienten demasiado rápidas o demasiado lentas** — Ajuste el intervalo de discriminación de clic en **File > Settings > Interaction**.

## Relacionados

- [Aetherial Audio Chain overview](overview.md)
- [Play back the captured PUDU audio](play-back-the-captured-pudu-audio.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
