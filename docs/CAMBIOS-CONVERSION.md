# Cambios para mejorar conversión (leads de WhatsApp)

> Contexto: campaña de Facebook con 677 visitas a la homepage y solo 1 lead por WhatsApp.
> Fecha de aplicación: 17/08/2026.

## Problemas detectados

1. Todo contacto pasaba por un **modal de 4 pasos** (acción + nivel obligatorios) antes de llegar a WhatsApp → mucha fricción.
2. El **banner de captura aparecía a los 30 s**, cuando la mayoría del tráfico móvil ya se fue.
3. La página no reflejaba el mensaje del anuncio ("Inscripciones abiertas 2026-2027").
4. Peso excesivo de imágenes en móvil (tricia.png 2.1 MB, logo.png 410 KB, galería ~150-215 KB cada una).
5. Sin click-to-call visible en header ni en hero.
6. No había un mensaje de urgencia real (cupo limitado por grupo).

## Cambios realizados

| # | Cambio | Por qué |
|---|--------|---------|
| 1 | Eliminado `ModalWhatsApp.astro` (modal de 4 pasos). | Todos los CTAs llevan directo a WhatsApp con mensaje prellenado; menos fricción = más leads. |
| 2 | Botón flotante `wa-float` verde fijo (abajo derecha) con enlace directo `wa.me`. | WhatsApp es el canal preferido en México; el botón ahora abre la conversación con 1 clic. |
| 3 | Banner `auto-cta` aparece a los **8 s** (antes 30 s) con "Cupo limitado por grupo · Inscripciones abiertas 2026-2027". | Urgencia real y captura cuando el visitante aún está en la página. |
| 4 | Hero: badge "Inscripciones abiertas · Ciclo 2026-2027 · Cupo limitado por grupo" en todas las slides. | Alinea la landing con la promesa del anuncio. |
| 5 | Hero: CTA verde "Escríbenos por WhatsApp" + enlace click-to-call. | Segunda vía de contacto directo. |
| 6 | Header: número de teléfono click-to-call (desktop). | Contacto inmediato sin buscar el footer. |
| 7 | Todos los CTAs de Costos, Características y "Día Montessori" ahora enlazan directo a WhatsApp. | Consistencia en todo el embudo. |
| 8 | Imágenes comprimidas: tricia 2.1 MB → 22 KB (webp), logo 410 → 15 KB, galería ~90% más ligera. Favicon dedicado (favicon.png 64px). | Menor tiempo de carga en móvil = menos rebote. |
| 9 | Eventos GA4: `whatsapp_cta_click` y `banner_cupo_visto`. | Medir el embudo real. |
| 10 | Sección "Conócenos en video" (YouTube): Casa de Niños, Taller I, Taller II y Campamento, con reproducción al hacer clic (no carga iframes de entrada). | Aumenta confianza y tiempo en página; evento GA4 `video_reproducido`. |
| 11 | SEO: `site` + `@astrojs/sitemap` en `astro.config.mjs`, canonical, `robots.txt`, JSON-LD `WebSite`+`School` con geo/horario/`sameAs`, `Article`+`BreadcrumbList` en blog, title "Escuela Montessori en Puebla", `apple-touch-icon`, `theme-color`, headers de caché en Netlify. | Posicionar en el dominio `.com.mx` y evitar contenido duplicado con `netlify.app`. Ver `docs/SEO.md`. |
| 12 | Index más ligero: la **galería se movió a su propia página `/galeria`** (15 fotos con lightbox) y se quitó del index; **Filosofía quedó con 1 sola cita**. | El homepage deja de cargar 15 imágenes y ~56KB de JS; la nueva página es indexable para SEO. |

## Cómo medir el antes/después (GA4)

1. En GA4 → Administración → Eventos: buscar `whatsapp_cta_click` y marcarlo como **evento clave** (conversión).
2. En el anuncio de Facebook usa UTM para aislar el tráfico:
   `?utm_source=facebook&utm_medium=paid&utm_campaign=inscripciones2026`
3. En GA4 → Informes → Adquisición, filtra por la campaña UTM y compara:
   - **Antes:** 677 sesiones → 1 lead (≈0.15%).
   - **Después (meta):** ≥2% de las sesiones en evento clave `whatsapp_cta_click`.
4. El lead real (mensaje recibido) debe contarse en la bandeja de WhatsApp y contrastarse con `whatsapp_cta_click`.

> Nota: sin Meta Pixel no se puede optimizar el anuncio para conversiones, pero GA4 + UTM mide el impacto real de estos cambios. Si más adelante se agrega el Pixel, disparar el evento `Lead` en el clic del botón verde.