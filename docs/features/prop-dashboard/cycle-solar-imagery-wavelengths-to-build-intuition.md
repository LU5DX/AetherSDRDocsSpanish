# Cicle a través de las longitudes de onda de imágenes solares para desarrollar la intuición

El panel Solar And Lunar del HF Propagation Dashboard muestra una imagen solar en vivo. Al hacer clic en la imagen, se recorren cinco vistas de longitud de onda, cada una revelando diferentes características solares. Utilice esto para desarrollar una percepción de lo que está haciendo el sol y cómo se relaciona con las condiciones de propagación actuales.

## Antes de comenzar

- Abra el HF Propagation Dashboard mediante `View > Propagation Conditions`.

## Pasos

1. Localice el panel **Solar And Lunar** en la sección inferior del diálogo. La etiqueta de imagen debajo de la imagen solar muestra la longitud de onda actual; la predeterminada es **Corona (193Å)**.
2. Haga clic una vez en la imagen solar. La vista avanza a la siguiente longitud de onda en la secuencia.
3. Continúe haciendo clic para recorrer las cinco longitudes de onda en orden:

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
| **Solar And Lunar panel** (imagen solar) | Muestra una imagen solar en vivo. Cada clic avanza a la siguiente longitud de onda. Vuelve a Corona (193Å) después de la última entrada. La vista predeterminada es Corona (193Å). |
| **What To Look For** | Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar mostrada actualmente. Se actualiza automáticamente al recorrer las longitudes de onda. |

## Consejos

- Lea el panel **What To Look For** junto con cada imagen. Proporciona una guía en lenguaje sencillo que coincide con la vista solar actual, lo que le ayuda a conectar las características visuales con los efectos de propagación.
- La vista **Flaring (94Å)** resalta el plasma de alta temperatura asociado con la actividad de fulguraciones. Crúcelo con la tarjeta de métrica **X-RAY** para ver si alguna región de fulguración visible está produciendo un flujo de rayos X elevado.
- No se requiere conexión de radio para usar esta función.

## Comportamiento de la ventana del panel

El HF Propagation Dashboard utiliza una geometría de ventana persistente que guarda y restaura su posición y tamaño automáticamente. El diálogo almacena su geometría bajo la clave de configuración `PropDashboardDialogGeometry`. No admite el modo de ventana sin marco; el marco de ventana estándar siempre está activo.

## Relacionados

- [Información general del HF Propagation Dashboard](overview.md)
- [Lea notas de aprendizaje rotativas sobre las condiciones solares](read-rotating-learning-notes-about-solar-conditions.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
