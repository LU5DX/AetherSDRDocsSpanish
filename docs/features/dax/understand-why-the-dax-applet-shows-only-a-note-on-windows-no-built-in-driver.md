# Entienda por qué el applet de DAX muestra solo una nota en Windows (sin controlador integrado)

Esta página explica por qué el applet de DAX Audio muestra solo una nota en Windows en lugar del conjunto completo de medidores y controles deslizantes de ganancia, y qué usar en su lugar.

## Antes de comenzar

- Está ejecutando AetherSDR en Windows.
- Tiene una conexión de radio establecida (el applet solo está disponible cuando está conectado).

## Qué sucede en Windows

Cuando abre el applet de DAX Audio en Windows, muestra solo esta nota:

> No built-in DAX driver on Windows.
> Use TCI, or SmartSDR DAX.

No hay botón **DAX Enable**, ni medidores/controles deslizantes RX por canal, ni control de ganancia TX. Todos los demás controles de DAX se omiten de la interfaz.

## Por qué sucede esto

AetherSDR no incluye un puente de audio DAX integrado para Windows. El puente DAX requiere un controlador de audio en modo kernel que AetherSDR solo proporciona en macOS y Linux. Debido a que los controles no tendrían efecto sin ese controlador, la compilación de Windows muestra solo esta nota explicativa y nada más.

El audio DAX sigue funcionando en Windows: lo proporcionan los controladores SmartSDR DAX de FlexRadio, que puede instalar por separado. El applet de DAX en pantalla de AetherSDR simplemente no gestiona esa ruta.

## Qué usar en su lugar

En Windows, enrute el audio del slice al software digital usando una de estas alternativas:

- **SmartSDR DAX** — Instale los controladores DAX de FlexRadio y use los canales DAX estándar de SmartSDR.
- **TCI** — Habilite el servidor TCI y conecte su software digital (por ejemplo, WSJT-X, fldigi) mediante el protocolo TCI.

## Consejos

- El ajuste **Autostart DAX with AetherSDR** (menú `Settings > Autostart DAX with AetherSDR`, clave de AppSettings `AutoStartDAX`) tampoco es aplicable en Windows por la misma razón.
- La nota de Windows está coloreada para resaltar (texto ámbar) y está fijada en la parte superior del panel del applet.

## Relacionado

- [Resumen de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
