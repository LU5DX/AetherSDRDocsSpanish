# Omitir la etapa de tubo en cualquiera de las cadenas

El widget CHAIN permite desactivar la etapa de tubo en la ruta TX o RX sin modificar ninguno de los ajustes de los controles. Úselo para comparar el efecto (A/B) o para eliminar el tubo de la cadena de señal por completo.

## Antes de comenzar

- AetherSDR debe estar en ejecución con un motor de audio cargado (no se requiere una conexión de radio para la etapa de tubo en sí).
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si no lo está, verifique `View > Applet Panel`.
- Localice el widget CHAIN dentro del contenedor Aetherial Audio (TXDSP). Contiene selectores de etapas de cadena de señal independientes para TX y RX.

## Pasos

1. En el panel de applets, busque el widget CHAIN dentro del contenedor **Aetherial Audio (TXDSP)**.
2. Identifique la etapa **TUBE** en el lado que desea omitir: TX (etiquetado **Aetherial Mic-PreAmp**) o RX (etiquetado **Aetherial Dynamic Tube**).
3. Haga clic una vez en la etapa **TUBE** del widget CHAIN para activar o desactivar el bypass en ese lado.
   - Cuando la etapa está activa, el applet de tubo es visible y procesa la señal.
   - Cuando está en bypass, el applet de tubo está oculto y la etapa deja pasar la señal sin procesarla.
4. Para volver a habilitarla, haga clic una vez más en la etapa **TUBE**.

De forma alternativa, abra el editor flotante de cualquiera de los lados haciendo doble clic en la etapa **TUBE** del widget CHAIN (título: **Aetherial Tube — TX** o **Aetherial Tube — RX**). El bypass se controla desde el widget CHAIN, no desde el interior del editor.

## Qué hace cada control

| Clave de ajuste | Qué controla | Valor predeterminado | Rango válido |
|---|---|---|---|
| `ClientTubeTxEnabled` | Si la etapa de tubo TX está activa | — | Habilitado / bypass |
| `ClientTubeRxEnabled` | Si la etapa de tubo RX está activa | — | Habilitado / bypass |
| `ClientTubeTxDriveDb` | Drive TX — nivel de señal a la entrada del tubo | 0.0 dB | 0.0 – 24.0 dB |
| `ClientTubeRxDriveDb` | Drive RX — nivel de señal a la entrada del tubo | 0.0 dB | 0.0 – 24.0 dB |
| `ClientTubeTxTone` | Tone TX — oscurece (negativo) o aclara (positivo) el timbre | 0.00 | −1.0 a 1.0 |
| `ClientTubeRxTone` | Tone RX | 0.00 | −1.0 a 1.0 |
| `ClientTubeTxBiasAmount` | Bias TX — punto de operación en la curva de transferencia | 0 % | 0 – 100 % |
| `ClientTubeRxBiasAmount` | Bias RX | 0 % | 0 – 100 % |
| `ClientTubeTxOutputGainDb` | Output TX — ganancia de compensación posterior al tubo | 0.0 dB | −24.0 a 12.0 dB |
| `ClientTubeRxOutputGainDb` | Output RX | 0.0 dB | −24.0 a 12.0 dB |
| `ClientTubeTxDryWet` | Mix TX — mezcla seca/húmeda (100 % = saturación total) | 100 % | 0 – 100 % |
| `ClientTubeRxDryWet` | Mix RX | 100 % | 0 – 100 % |

## Consejos

- Al poner en bypass la etapa de tubo se conservan todos los valores de los controles (`Drive`, `Tone`, `Bias`, `Output`, `Mix`). Al volver a habilitarla se restauran los mismos ajustes.
- La curva de transferencia y la bola de entrada en tiempo real del applet solo son visibles cuando la etapa de tubo está activa. Desaparecen cuando está en bypass porque el propio applet queda oculto.
- Los lados TX y RX son completamente independientes. Puede poner uno en bypass sin afectar al otro.
- Un temporizador de sincronización de 30 Hz mantiene los controles del applet coherentes con cualquier cambio realizado en el editor flotante. Si modifica ajustes en el editor mientras la etapa está activa, el applet los reflejará en un ciclo de sondeo.

## Solución de problemas

- **Hacer clic una vez en la etapa TUBE no tiene efecto** — Confirme que está haciendo clic en la etapa TUBE del lado correcto (TX vs. RX). Las dos cadenas son independientes y hacer clic en una no afecta a la otra.
- **El applet de tubo no es visible después de habilitarlo** — El applet permanece oculto hasta que la etapa de tubo se habilita mediante el widget CHAIN. Si aun así no aparece después de habilitarla, verifique que el contenedor principal **Aetherial Audio (TXDSP)** esté expandido en el panel de applets.

## Temas relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Ajuste el Drive hasta que la curva comience a curvarse (calidez en TX o modelado de timbre en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Saturación en mezcla paralela con Mix](parallel-blend-saturation-with-mix.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
