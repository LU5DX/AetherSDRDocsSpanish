# Omitir PUDU de la cadena

Elimine temporalmente el excitador PUDU de la cadena DSP de TX sin cambiar ninguno de sus ajustes. Use esto cuando desee comparar su audio con y sin procesamiento PUDU, o cuando necesite transmitir sin el efecto activo.

## Antes de comenzar

- La etapa PUDU ya debe estar presente en el widget CHAIN dentro del contenedor PooDoo Audio (TXDSP).
- No se requiere conexión de radio para omitir o reactivar la etapa.

## Pasos

1. Localice el widget CHAIN en el contenedor PooDoo Audio (TXDSP).
2. Haga un solo clic en la etapa **PUDU (Enh)** en el widget CHAIN.

Un solo clic alterna la etapa PUDU entre activa y omitida. La etapa permanece en la cadena, pero el audio pasa a través de ella sin procesar mientras está omitida. El ajuste `ClientPuduTxEnabled` se actualiza inmediatamente y se conserva.

Para reactivar PUDU, haga un solo clic en la etapa **PUDU (Enh)** nuevamente.

## Consejos

- Omitir mediante el widget CHAIN no restablece ningún valor de perilla. Todos los ajustes de Poo Drive, Poo Tune, Poo Mix, Doo Tune, Doo Air y Doo Mix se conservan.
- Hacer doble clic en la etapa **PUDU (Enh)** en el widget CHAIN abre el editor flotante de PUDU en lugar de alternar la omisión. Use un solo clic para omitir.
- El logotipo de PooDoo dentro del applet de PUDU parpadea con el RMS de la señal procesada cuando PUDU está activo y deja de parpadear cuando está omitido.

## Relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Seleccionar carácter Aphex (Par) vs Behringer (Impar)](pick-aphex-even-vs-behringer-odd-character.md)
