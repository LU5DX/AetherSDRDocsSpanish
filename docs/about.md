---
title: Acerca de esta documentación
description: Cómo se construye la documentación de AetherSDR, el pipeline de IA detrás de ella y cómo puede apoyar el proyecto.
---

# Acerca de esta documentación

## Creada para una aplicación seria

AetherSDR no es un proyecto de fin de semana. Está desarrollado con **C++20 y Qt6** desde el primer día — la mejor tecnología disponible para una aplicación que exige rendimiento DSP en tiempo real, baja latencia y comportamiento nativo multiplataforma en Linux, macOS y Windows. Ese nivel de ingeniería merece una documentación a la altura.

La documentación es un componente de primera clase en cualquier proyecto de software — no algo que se añade al final. Una buena documentación reduce la fricción para los nuevos usuarios, ayuda a los operadores con experiencia a aprovechar al máximo cada función y disminuye la barrera de entrada a un hobby que ya tiene una curva de aprendizaje suficientemente pronunciada.

---

## Un pipeline de documentación impulsado por IA

Este manual no se escribe a mano página por página. Es generado por un pipeline personalizado que construí para mantener el ritmo con las versiones de AetherSDR:

1. **Ingesta de fuentes** — con cada nueva versión, el pipeline extrae el código fuente C++ de AetherSDR directamente del repositorio.
2. **Análisis con IA** — un modelo de lenguaje de gran escala analiza cada objeto visible para el usuario expuesto por la aplicación: ventanas, controles, menús, ajustes y comportamientos.
3. **Salida de alta calidad** — el modelo produce documentación estructurada y precisa en inglés natural, describiendo qué hace cada función, cómo usarla y las opciones de configuración relevantes.

El resultado es un manual vivo que evoluciona con el software — no un documento estático que queda obsoleto dos versiones después.

---

## Athena — su asistente de IA

Cada página de este sitio incluye a **Athena**, una asistente de IA que puede abrir en cualquier momento haciendo clic en el botón de chat en la esquina inferior derecha.

Athena funciona con **RAG — Retrieval-Augmented Generation** (generación aumentada por recuperación). Esto es lo que significa en términos simples:

> En lugar de basarse únicamente en lo que un modelo de lenguaje aprendió durante su entrenamiento, RAG primero *recupera* los pasajes más relevantes de una base de conocimiento real — en este caso, la documentación actual — y luego *genera* una respuesta fundamentada en ese contenido.

Esto significa que Athena no inventa funciones que no existen ni describe comportamientos de una versión diferente del software. Sus respuestas están ancladas a la documentación actual de AetherSDR, con enlaces a las fuentes para que pueda verificar todo lo que dice.

En detalle técnico:

- **Base de datos vectorial** — los fragmentos de documentación se vectorizan y almacenan para búsqueda semántica rápida
- **Embeddings de Voyage AI** — embeddings de texto de última generación para mayor precisión en la recuperación
- **Claude (Anthropic)** — el modelo de lenguaje que sintetiza el contexto recuperado en respuestas claras
- **Backend FastAPI** — desplegado en Railway para respuestas confiables y de baja latencia
- **Modo avanzado** — active ⚙️ para buscar también en el código fuente de AetherSDR, no solo en la documentación

Athena mejora continuamente. Con cada iteración se incorporan nueva documentación, mejor ajuste de recuperación y prompts más inteligentes.

---

## Código abierto, donde es posible

Este proyecto se apoya en código abierto en cada capa:

| Componente | Tecnología |
|---|---|
| Sitio de documentación | [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) |
| Renderizado de Markdown en el chat | [marked.js](https://marked.js.org/) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| Almacén vectorial | [ChromaDB](https://www.trychroma.com/) |
| Framework de API | [FastAPI](https://fastapi.tiangolo.com/) |
| Alojamiento | [GitHub Pages](https://pages.github.com/) (documentación) + [Railway](https://railway.app/) (backend) |

---

## La infraestructura tiene costos reales

GitHub Pages aloja la documentación de forma gratuita. Todo lo demás, no:

- **Base de datos vectorial** — embeddings ajustados y almacenamiento persistente para cada versión de AetherSDR
- **Llamadas a la API del LLM** — cada pregunta que responde Athena consume tokens
- **Embeddings de Voyage AI** — la búsqueda semántica de alta calidad requiere una API de embeddings de pago
- **Despliegue en Railway** — backend siempre activo para el asistente

Si esta documentación le resulta útil — si le ahorró una hora de búsqueda en foros, o le ayudó a poner su radio en el aire más rápido — su apoyo contribuye genuinamente a mantener este sistema en funcionamiento y a mejorarlo con el tiempo.

---

## Apoye el proyecto

!!! tip "Cada contribución ayuda"
    Incluso una pequeña contribución compensa los costos de la API y la infraestructura, y motiva mejoras continuas tanto en la documentación como en el asistente.

<div style="text-align:center; margin: 2rem 0;">
  <a href="https://ko-fi.com/lu5dx" class="md-button md-button--primary" target="_blank" rel="noopener" style="margin: 0.5rem;">
    ☕ Invíteme un café
  </a>
  <a href="https://paypal.me/lu5dx599" class="md-button md-button--primary" target="_blank" rel="noopener" style="margin: 0.5rem;">
    💙 Donar por PayPal
  </a>
  <a href="https://github.com/LU5DX" class="md-button" target="_blank" rel="noopener" style="margin: 0.5rem;">
    ⭐ Destacar en GitHub
  </a>
</div>

---

*Pipeline de documentación y asistente de IA desarrollados por [LU5DX](https://github.com/LU5DX).*
*AetherSDR es desarrollado por [ten9876](https://github.com/ten9876/AetherSDR).*
