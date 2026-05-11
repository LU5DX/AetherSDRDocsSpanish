# Lea el medidor ALC de software (pico SSB posterior al ALC de software) en el panel de Phone o CW

Esta página le explica cómo monitorear el medidor de Control Automático de Nivel (ALC) de software, que muestra el pico SSB posterior al ALC de software en dBFS. Este medidor le ayuda a ajustar la ganancia de su micrófono o la envolvente de manipulación CW para transmitir a un nivel adecuado sin sobreexcitar la cadena de audio.

## Antes de comenzar

- Asegúrese de que su FLEX-8600 esté conectado y que el slice activo esté en un modo de voz (Phone) o modo CW.
- El applet de Phone/CW debe estar visible en la barra lateral derecha — actívelo usando el botón **P/CW** de la bandeja si es necesario.

## Pasos

1. Localice el indicador **ALC** en el subpanel de Phone o CW. Muestra un rango de **-20 a 0 dBFS**, llenándose de derecha a izquierda.
2. Active el transmisor (o, para CW, comience a enviar).
3. Observe la aguja del indicador ALC mientras ajusta la ganancia de su micrófono con el control deslizante **Mic gain**:
   - El medidor está vacío (en **-20 dBFS**) cuando no se aplica ALC.
   - El indicador se llena hacia **0 dBFS** a medida que aumenta el ALC.
   - La zona roja comienza en **-3 dBFS** (marcada en el indicador).
4. Para CW, el mismo indicador ALC aparece en el subpanel de CW — es idéntico y está controlado por la misma fuente del medidor.

## Qué hace cada control

| Control | Etiqueta | Comportamiento | Rango válido | Valor predeterminado | Clave de configuración |
|---------|----------|----------------|--------------|----------------------|------------------------|
| Indicador ALC (panel Phone) | **ALC** | Muestra la lectura de control automático de nivel del medidor ALC de software (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Zona roja por encima de -3 dBFS. | -20 a 0 dBFS | — | None |
| Indicador ALC (panel CW) | **ALC** | Refleja el indicador ALC del panel Phone; ambos leen del mismo medidor ALC de software para obtener lecturas coherentes en voz y CW. | -20 a 0 dBFS | — | None |

## Relacionado

- [Ajuste la ganancia del micrófono y habilite la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Configure la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
