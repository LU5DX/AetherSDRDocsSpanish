# Ciclar por imágenes de longitudes de onda solares para desarrollar intuición

El panel Solar y Lunar en el Panel de Propagación de HF muestra una imagen solar en vivo. Al hacer clic en la imagen, se cicla por cinco vistas de longitud de onda, cada una revelando diferentes características solares. Use esto para desarrollar una sensación de lo que está haciendo el sol y cómo se relaciona con las condiciones de propagación actuales.

## Antes de comenzar

- Abra el Panel de Propagación de HF mediante `View > Propagation Conditions`.

## Pasos

1. Localice el panel **Solar And Lunar** en la sección inferior del diálogo. La etiqueta de imagen debajo de la imagen solar muestra la longitud de onda actual; el valor predeterminado es **Corona (193Å)**.
2. Haga clic en la imagen solar una vez. La vista avanza a la siguiente longitud de onda en la secuencia.
3. Continúe haciendo clic para ciclar por las cinco longitudes de onda en orden:

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
| **What To Look For** | Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar mostrada actualmente. Se actualiza automáticamente al ciclar longitudes de onda. |

## Consejos

- Lea el panel **What To Look For** junto con cada imagen. Proporciona orientación en lenguaje sencillo adaptada a la vista solar actual, lo que ayuda a conectar las características visuales con los efectos de propagación.
- La vista **Flaring (94Å)** resalta el plasma de alta temperatura asociado con la actividad de llamaradas. Compárela con la tarjeta métrica **X-RAY** para ver si alguna región de llamarada visible está produciendo un flujo de rayos X elevado.
- No se requiere conexión de radio para usar esta función.

## Comportamiento de la ventana del panel

El Panel de Propagación de HF utiliza una geometría de ventana persistente que guarda y restaura automáticamente su posición y tamaño. El diálogo almacena su geometría bajo la clave de configuración `PropDashboardDialogGeometry`. No admite el modo de ventana sin marco; el marco de ventana estándar siempre está activo. El diálogo y sus paneles integrados utilizan el tema activo en todo momento; las líneas separadoras, los fondos de las justificaciones y los paneles de notas de aprendizaje respetan el esquema de color actual.

## Relacionados

- [HF Propagation Dashboard overview](overview.md)
- [Read rotating learning notes about solar conditions](read-rotating-learning-notes-about-solar-conditions.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
