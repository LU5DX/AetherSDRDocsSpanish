# Ciclo por vistas de longitud de onda solar para desarrollar intuición

El panel Solar And Lunar en el HF Propagation Dashboard muestra una imagen solar en vivo. Al hacer clic en la imagen, se cicla a través de cinco vistas de longitud de onda, cada una revelando diferentes características solares. Use esto para desarrollar una intuición sobre lo que está haciendo el sol y cómo se relaciona con las condiciones de propagación actuales.

## Antes de empezar

- Abra el HF Propagation Dashboard a través de `View > Propagation Conditions`.

## Pasos

1. Localice el panel **Solar And Lunar** en la sección inferior del diálogo. La etiqueta de imagen debajo de la imagen solar muestra la longitud de onda actual — la predeterminada es **Corona (193Å)**.
2. Haga clic una vez en la imagen solar. La vista avanza a la siguiente longitud de onda en la secuencia.
3. Continúe haciendo clic para ciclar a través de las cinco longitudes de onda en orden:

   | Posición | Etiqueta |
   |---|---|
   | 1 | Corona (193Å) |
   | 2 | Chromosphere (304Å) |
   | 3 | Quiet Corona (171Å) |
   | 4 | Flaring (94Å) |
   | 5 | Visible (HMI) |

4. Deje de hacer clic cuando la etiqueta debajo de la imagen muestre la longitud de onda que desea estudiar.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Panel **Solar And Lunar** (imagen solar) | Muestra una imagen solar en vivo. Cada clic avanza a la siguiente longitud de onda. Vuelve a Corona (193Å) después de la última entrada. La vista predeterminada es Corona (193Å). |
| **What To Look For** | Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar mostrada actualmente. Se actualiza automáticamente a medida que cicla las longitudes de onda. |

## Consejos

- Lea el panel **What To Look For** junto con cada imagen. Proporciona orientación en lenguaje sencillo adaptada a la vista solar actual, lo que le ayuda a conectar las características visuales con los efectos de propagación.
- La vista **Flaring (94Å)** resalta el plasma de alta temperatura asociado con la actividad de fulguraciones. Cruce referencia con la tarjeta de métrica **X-RAY** para ver si alguna región de fulguración visible está produciendo un flujo de rayos X elevado.
- No se requiere conexión de radio para usar esta función.

## Relacionado

- [HF Propagation Dashboard overview](overview.md)
- [Read rotating learning notes about solar conditions](read-rotating-learning-notes-about-solar-conditions.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
