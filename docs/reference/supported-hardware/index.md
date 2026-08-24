---
title: Hardware compatible
---

# Hardware compatible

AetherSDR funciona con cualquier transceptor **FlexRadio** (el objetivo
soportado) y, de forma experimental, con una lista creciente de otras familias
de radio que usan la capa neutral `IRadioBackend`.

## Soportado: FlexRadio

- Serie FLEX-6000 — FLEX-6300, 6400, 6400M, 6500, 6600, 6600M, 6700
- Serie FLEX-8000 — FLEX-8400, 8400M, 8600, 8600M
- Serie Aurora — AU-510, 510M, 520, 520M
- Dispositivos de las series ML, CL y RT

El objetivo de prueba activo es el FLEX-8600 con firmware 4.2.18 (protocolo
SmartSDR v1.4.0.0). El firmware 4.x anterior funciona; v3.x no está soportado.

## Dispositivos externos

Fuera de la capa de radio, AetherSDR también controla:

- Amplificador **PGXL** (Power Genius XL) y sintonizador **TGXL** (Tuner Genius XL)
- Amplificadores **ACOM serie S** (serial / ser2net)
- Amplificadores **SPE Expert** — 1.3K-FA / 1.5K-FA / 2K-FA (serial / ser2net TCP)
- Amplificadores **VK3AMP** — 600 W / 1000 W / 2000 W (control TCP + telemetría UDP)

## Familias de radio experimentales

Dos familias adicionales están en desarrollo activo. Ninguna es una familia
*soportada* todavía, y FlexRadio sigue siendo el objetivo soportado:

- [**Hermes-Lite 2**](hermes-lite-2.md) — un SDR de bajo costo y código abierto.
  Cuatro receptores, SSB/CW/RTTY/AX.25, conmutación de banda con filtros de
  hardware y un supresor de impulsos ejecutado en el host.
- [**Icom en red**](icom.md) — CI-V sobre el transporte UDP de RS-BA1, probado en
  el IC-705 y completado contra un IC-7300MK2 real.

Ambas son opt-in y están claramente marcadas en la interfaz: AetherSDR muestra
un aviso la primera vez que conectas una, y solo se alcanzan a través del flujo
manual de "Conectar a Radio".

## ¿Sin radio?

El **Modo demo** ejecuta la interfaz completa contra un backend sintético que
genera su propio audio y espectro de recepción — sin hardware.
