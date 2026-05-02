# Confirmar visualmente cuando TX (MOX) está activo

El applet Aetherial Audio Chain muestra un indicador rojo pulsante en el extremo TX cada vez que su slice está transmitiendo (MOX activo). Esto le permite confirmar de un vistazo que su radio está en el aire sin apartar la vista de su cadena de audio.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para abrir el contenedor Aetherial Audio.
- Haga clic en `TX` en el encabezado del applet para que la cadena TX sea la vista activa.

## Pasos

1. Haga clic en el botón de bandeja `TX` en el encabezado del applet para mostrar la cadena DSP de TX.
2. Active el radio (PTT, VOX o MOX).
3. Observe el indicador del extremo TX al final de la tira de cadena TX.

El indicador del extremo TX pulsa en rojo mientras su slice está transmitiendo. Al desactivar la transmisión, el indicador regresa a su estado inactivo (sin pulso).

## Qué hace cada control

| Etiqueta                                           | Tipo                                                                                                                                    | Comportamiento                                                                                                                                                                                                                                                                      |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `TX`                                               | Botón de alternancia                                                                                                                    | Muestra la cadena DSP de TX. Predeterminado: activado. Forma un par exclusivo con `RX`; aparece en color ámbar cuando está seleccionado.                                                                                                                                            |
| Indicador del extremo TX                           | Indicador                                                                                                                               | Pulsa en rojo mientras el radio está transmitiendo en el slice activo (controlado por el estado de MOX). Inactivo cuando no se transmite.                                                                                                                                           |
| Etapa de cadena RX (EQ / AGC-T / AGC-C / TUBE / PUDU) | Un clic simple alterna el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las cinco etapas RX (EQ, AGC-T/Gate, AGC-C/Comp, Tube, PUDU) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME exclusivo `application/x-aethersdr-rx-chain-stage` evita soltar elementos entre las dos tiras. |

## Consejos

- El indicador del extremo TX solo está presente en el modo TX. Cambie a `TX` usando el botón `TX` en el encabezado del applet si ve la cadena RX en su lugar.
- El pulso rojo está controlado por el estado MOX del radio, por lo que refleja el estado real de transmisión en el aire independientemente de cómo se haya activado la transmisión (PTT por hardware, MOX por software, VOX).

## Relacionado

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
