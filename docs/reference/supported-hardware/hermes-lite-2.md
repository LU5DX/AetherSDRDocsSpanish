---
title: Hermes-Lite 2
---

# Hermes-Lite 2

!!! warning "Experimental"
    El soporte de Hermes-Lite 2 es **experimental** — todavía no es una familia
    de radio soportada. La recepción y transmisión básicas funcionan, pero
    algunos controles, medidores y funciones específicas siguen incompletos.
    FlexRadio sigue siendo el objetivo soportado.

El Hermes-Lite 2 (HL2) es un transceptor SDR de bajo costo y código abierto.
Habla **Protocolo 1** de HPSDR (Metis) por Ethernet y, a diferencia de un
FlexRadio, entrega IQ crudo y **no ejecuta DSP en el firmware** — todo el
filtrado, la reducción de ruido y la demodulación ocurren en tu computadora.

## Conexión

1. Abre **Conectar a Radio**.
2. Elige el tipo de radio manual **Hermes-Lite 2**.
3. El HL2 responde a un datagrama de descubrimiento del Protocolo 1 de HPSDR en
   UDP/1024, por lo que se detecta automáticamente en la red local.

## Qué funciona

- **Cuatro receptores independientes**, cada uno con su propio slice.
- **Voz SSB**, **decodificación de CW/RTTY** y **paquetes AX.25**.
- **Conmutación de banda con filtros de hardware**.
- **Filtros notch manuales**.
- **Supresión de ruido** — el HL2 no tiene DSP en el lado de la radio, así que
  el supresor de impulsos corre en el host, antes del demodulador, sobre el IQ
  crudo.
- **Un BFO de CW real** — la falda del paso de banda se centra en el tono de CW,
  de modo que el receptor escucha donde la radio realmente transmite.
- **Calibración de frecuencia en el host** y **restauración de estado por radio**
  (incluido el modo y el umbral de AGC, que sobreviven a un reinicio).
- **Transmisión de CW con temporización del cliente** con persistencia tras
  reiniciar.
- **Control de nivel de TX** — el nivel de audio del cliente (por ejemplo, el
  deslizador `Pwr` de WSJT-X) se respeta; el ALC de voz del host ya no lo anula.

## En qué se diferencia de FlexRadio

- **Modulación en el host:** el HL2 transmite el audio que le envíes, así que el
  host hace la modulación. Es lo opuesto al backend de Icom en red, que deja
  que la radio module.
- **Sin DSP en la radio:** NR/ANF no se ofrecen; el supresor de ruido y demás
  procesamiento corren en el host.
- **IQ crudo:** no hay espectro generado por la radio; el panadapter se dibuja
  a partir del flujo de IQ en tu máquina.

## Limitaciones

- Experimental: no todos los medidores, controles y funciones específicas están
  cableados.
- El host hace más trabajo por slice que en un FlexRadio (el IQ se procesa
  localmente).

Consulta [Hardware compatible](index.md) para el panorama completo.
