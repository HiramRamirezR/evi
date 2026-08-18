# Guía SEO — Educación para la Vida (.com.mx)

Cambios aplicados el 17/08/2026 para posicionar el dominio `educacionparalavida.com.mx`.

## Qué se implementó

1. **`site` + sitemap**: `astro.config.mjs` define el dominio y `@astrojs/sitemap` genera `sitemap-index.xml` en cada build.
2. **Canonical**: todas las páginas emiten `<link rel="canonical">` apuntando al `.com.mx` → evita duplicados si el sitio se abre por `*.netlify.app`.
3. **robots.txt**: permite todo y apunta al sitemap.
4. **Structured data**:
   - Homepage: `WebSite` + `School` (dirección, geo 19.0150943,-98.1835998, horario 8:00-14:00, teléfono, `sameAs` → Facebook).
   - Blog: `Article` + `BreadcrumbList` por post.
5. **Title**: "Escuela Montessori en Puebla | Educación para la Vida" (keyword local).
6. **Extras**: `theme-color`, `apple-touch-icon`, `og:image` 1200×630 con width/height, keywords con "Montessori Puebla".
7. **Netlify**: redirección 301 del subdominio `netlify.app` → `.com.mx` y headers de caché (imágenes/fuentes).
   - ⚠️ Revisa `netlify.toml`: si tu subdominio no es `evi.netlify.app`, cámbialo. Si Netlify ya redirige solo (dominio principal configurado), la regla es redundante pero inofensiva.

## Pasos para ti (Google Search Console)

1. Entra a **https://search.google.com/search-console** con la cuenta de Google que administra el sitio.
2. **Añadir propiedad** → elige **"Prefijo de URL"** → escribe `https://educacionparalavida.com.mx`.
3. Elige el método de verificación **"Tag de HTML"** y copia el meta tag que te da Google.
   - Pégalo en `src/layouts/BaseLayout.astro` dentro de `<head>` (junto a los otros meta). Después del build se publica y quedas verificado. (O usa el método DNS/archivo si prefieres; no necesitas tocar el código.)
4. En GSC → **Sitemaps** → envía `sitemap-index.xml`.
5. En **Resultados de búsqueda** (rendimiento) verás por qué palabras apareces. Las keywords objetivo son: "escuela montessori puebla", "kinder montessori puebla", "primaria montessori puebla", "secundaria montessori puebla".

## Cómo medir (GA4)

- Marca como **eventos clave**: `whatsapp_cta_click`, `banner_cupo_visto`, `video_reproducido`.
- Añade UTM al anuncio de Facebook para aislar campaña:
  `?utm_source=facebook&utm_medium=paid&utm_campaign=inscripciones2026`

## Pendiente (mejoras futuras)

- Verificar el subdominio netlify exacto en `netlify.toml`.
- El video "Día del Padre virtual" (viral) no se embebió en la sección de videos; puede añadirse como contenido de comunidad si se desea.
- Más contenido de blog (Google premia el contenido nuevo y consistente).
- Si se agrega Meta Pixel, disparar evento `Lead` en el clic de WhatsApp.