# Omitir PUDU de la cadena

Elimine temporalmente el excitador PUDU de la cadena DSP de TX sin modificar ninguna de sus configuraciones. Use esto cuando desee comparar su audio con y sin el procesamiento PUDU, o cuando necesite transmitir sin el efecto activo.

## Antes de comenzar

- La etapa PUDU debe estar ya presente en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
- No se requiere conexión de radio para omitir o reactivar la etapa.

## Pasos

1. Localice el widget CHAIN en el contenedor PooDoo Audio (TXDSP).
2. Haga clic una vez en la etapa **PUDU (Enh)** en el widget CHAIN.

Un solo clic alterna la etapa PUDU entre activa y omitida. La etapa permanece en la cadena, pero el audio la atraviesa sin procesamiento mientras está omitida. La configuración `ClientPuduTxEnabled` se actualiza de inmediato y se conserva.

Para reactivar PUDU, haga clic una vez más en la etapa **PUDU (Enh)**.

## Sugerencias

- Omitir la etapa mediante el widget CHAIN no restablece ningún valor de los controles. Todos los ajustes de Poo Drive, Poo Tune, Poo Mix, Doo Tune, Doo Air y Doo Mix se conservan.
- Hacer doble clic en la etapa **PUDU (Enh)** en el widget CHAIN abre el editor flotante de PUDU en lugar de alternar la omisión. Use un solo clic para omitirla.
- El logotipo de PooDoo dentro del applet de PUDU pulsa con el RMS de la señal procesada cuando PUDU está activo y deja de pulsar cuando está omitido.

## Relacionado

- [Descripción general del excitador PUDU](overview.md)
- [Elegir el carácter Aphex (par) o Behringer (impar)](pick-aphex-even-vs-behringer-odd-character.md)
