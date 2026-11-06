# Plantilla NoExpertise · Camping y alojamiento rural

Web de fotos grandes para campings, casas rurales y bungalows, con alojamientos, entorno y reservas.

- Sectores: camping, casa-rural, glamping, albergue, hotel-rural, apartamentos-rurales. Estilo: natural. Plan mínimo: presencia.
- Secciones: hero, alojamiento, alojamientos, comodidades, entorno, galeria, temporada, opiniones, como-llegar, preguntas, reservas, contacto (y `texto` para apartados nuevos).
- Diseño a ancho completo: verde bosque + teja + hueso; portada a pantalla casi completa con la foto a sangre y el nombre enorme encima, y una barra de fechas que lleva a reservas; «El lugar» con la foto grande hasta el borde y una foto de detalle encima; alojamientos con foto grande y píldoras de tipo y precio; servicios con panorámica a sangre e iconos; entorno en tarjetas verticales (carrusel en el móvil); galería en mosaico de borde a borde con visor; temporada con foto a sangre y tabla; mapa que solo se carga al pulsar; reservas con foto a sangre y formulario de estancia; barra fija del móvil con «Llamar» y «Reservar».
- Campos propios: `alojamiento.firma` y `alojamiento.foto`; `alojamientos.alojamientos` [{nombre, categoria, texto, precio, personas, extras, imagen}]; `comodidades.items` con icono; `entorno.actividades` [{titulo, texto, distancia, imagen}]; `temporada.horario` [{dia, horas}] y `temporada.nota`; `reservas.enlace_reservas` y `reservas.nota`. Detalle en `CLAUDE.md`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`seo.tipo`, `Campground` en el ejemplo) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
- Contenido editable en `site.yaml` (ejemplo: La Vega del Cares, camping ficticio en Arenas de Cabrales); metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Fotos de ejemplo generadas con IA para esta plantilla; imágenes de relleno (`public/placeholders/`) dibujadas para ella, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.alojamientos.alojamientos` con `detalle` tiene su página en `/alojamientos/<slug>/`, y cada uno de `secciones.entorno.actividades`, en `/entorno/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
