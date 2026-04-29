# Omitir el PUDU de la cadena

Elimine temporalmente el excitador PUDU de la cadena DSP de TX sin modificar ninguno de sus ajustes. Use esta opción cuando desee comparar su audio con y sin el procesamiento PUDU, o cuando necesite transmitir sin el efecto activo.

## Antes de comenzar

- La etapa PUDU debe estar ya presente en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
- No se requiere conexión de radio para omitir o reactivar la etapa.

## Pasos

1. Localice el widget CHAIN en el contenedor PooDoo Audio (TXDSP).
2. Haga clic una vez en la etapa **PUDU (Enh)** del widget CHAIN.

Un solo clic alterna la etapa PUDU entre activa y omitida. La etapa permanece en la cadena, pero el audio la atraviesa sin procesamiento mientras está omitida. El ajuste `ClientPuduTxEnabled` se actualiza de inmediato y se guarda de forma persistente.

Para reactivar el PUDU, haga clic una vez más en la etapa **PUDU (Enh)**.

## Consejos

- Omitir la etapa mediante el widget CHAIN no restablece ningún valor de los controles. Todos los ajustes de Poo Drive, Poo Tune, Poo Mix, Doo Tune, Doo Air y Doo Mix se conservan.
- Hacer doble clic en la etapa **PUDU (Enh)** del widget CHAIN abre el editor flotante del PUDU en lugar de alternar el bypass. Use un solo clic para omitirla.
- El logotipo de PooDoo dentro del applet PUDU pulsa con el nivel RMS de la señal procesada cuando el PUDU está activo y deja de pulsar cuando está omitido.

## Temas relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Elegir el carácter Aphex (par) o Behringer (impar)](pick-aphex-even-vs-behringer-odd-character.md)
