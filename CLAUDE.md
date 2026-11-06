# Plantilla «Camping y alojamiento rural» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **natural**, a ancho completo (bandas de borde a borde, fotos grandes a sangre).
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga, lo tipa y lo normaliza; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = verde bosque, acento = teja, fondo = hueso, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). Los tonos derivados (`--bosque-hondo`, `--salvia`, `--acento-hondo`, `--acento-texto`, `--acento-claro`, `--sobre-oscuro`, `--linea`, `--linea-clara`) se calculan con `color-mix` en `src/styles/global.css`. El diseño cuenta con un primario oscuro, un acento medio y un fondo claro.
- **Tipografías y aspecto general**: `src/styles/global.css` (serifa del sistema —Sitka, Iowan, Charter, Georgia de respaldo— para títulos; sans del sistema para el texto; antetítulos en mayúsculas pequeñas con el acento; botones de píldora). Bandas `.banda--claro|salvia|bosque|hondo`, filas a sangre `.lugar` y `.partida`, fichas `.estancia`, tarjetas `.lugar-tarjeta`, mosaico `.mosaico`. Fuentes del sistema: no añadas fuentes externas.
- **Cabecera**: `src/components/Header.astro` (fija; transparente sobre la portada y sólida al hacer scroll, con un script pequeño). **Pie**: `src/components/Footer.astro` (nombre enorme, eslogan, tres columnas y, en el móvil, la barra fija «Llamar» / «Reservar»).
- **Imágenes**: en `public/`. Fotos en `public/fotos/` (se generan a partir de `fotos.json`); si una foto de `/fotos/` falta, `Imagen.astro` muestra `/placeholders/<mismo nombre>.svg`. Personas: siempre `/placeholders/persona.svg`, nunca caras generadas.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en serifa y la localidad debajo.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis; esta plantilla es de plan presencia).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `hero.astro` (portada a pantalla casi completa: foto a sangre, nombre enorme, lema, botones y detalles; en escritorio, barra de fechas que lleva a reservas)
- `alojamiento` → `alojamiento.astro` («El lugar»: texto + foto grande hasta el borde con la foto de detalle encima)
- `alojamientos` → `alojamientos.astro` (fichas con foto grande en dos columnas)
- `comodidades` → `comodidades.astro` (servicios e instalaciones: panorámica a sangre + rejilla de iconos)
- `entorno` → `entorno.astro` (tarjetas verticales con foto; carrusel en el móvil)
- `galeria` → `galeria.astro` (mosaico de borde a borde con visor)
- `temporada` → `temporada.astro` (foto a sangre + tabla de temporada y horarios)
- `opiniones` → `opiniones.astro`
- `como-llegar` → `como-llegar.astro` (indicaciones + mapa que solo se carga al pulsar)
- `preguntas` → `preguntas.astro` (acordeón `details/summary`)
- `reservas` → `reservas.astro` (texto + formulario de estancia, foto a sangre)
- `contacto` → `contacto.astro`
- `texto` → `texto.astro` (apartado genérico para `tipo: texto`: con foto, fila a sangre; sin foto, dos columnas)

## Campos propios de esta plantilla (además del esquema común)
- `hero`: el h1 es `site.yaml → nombre`; `titulo` es el lema de debajo (si es igual que el nombre no se repite). `cta` (sin él, el botón llama), `cta_secundario`, `items` [{titulo, icono}] = detalles con icono. La barra de fechas sale sola si la sección `reservas` está activa.
- `alojamiento`: `texto` (párrafos separados por una línea en blanco), `firma` (quién lo cuenta), `imagen` (foto grande), `foto` (foto de detalle vertical, solo en escritorio), `cta` (enlace con flecha).
- `alojamientos.alojamientos` [{nombre, categoria, texto, precio, personas, extras, imagen}]: `categoria` es el tipo («Casa rural», «Bungalow», «Glamping», «Parcela», «Habitación»). `precio` y `personas` SIEMPRE como cadena (`"desde 95 €/noche"`, `"Hasta 4 personas"`); vacíos = no se pintan. `extras` es UNA cadena separada por comas, nunca una lista. `cta` de la sección opcional (botón al final).
- `comodidades`: `imagen` (panorámica a sangre) e `items` [{titulo, texto, icono}].
- `entorno.actividades` [{titulo, texto, distancia, imagen}]: `distancia` como cadena («A 2 km», «A 40 minutos en coche»).
- `galeria.galeria`: lista de rutas; con 8 fotos el mosaico queda cerrado en escritorio.
- `temporada`: `texto`, `imagen`, `horario` [{dia, horas}] («Camping» · «De Semana Santa a octubre»), `nota`.
- `opiniones.testimonios` [{texto, autor, nota}]: sin estrellas ni puntuaciones.
- `como-llegar`: `texto`, `imagen` (fondo del mapa hasta que se carga), `items` (iconos `coche`, `tren`, `bus`, `avion`) y botón a Google Maps con `contacto.direccion` (texto en `cta.texto`; si `cta.url` tiene una dirección web, se usa esa). El mapa de Google solo se carga si el visitante pulsa «Ver el mapa aquí».
- `reservas`: `texto`, `imagen`, `cta` (WhatsApp o teléfono), `nota` (cancelación, estancia mínima…), formulario con llegada, salida y personas. `enlace_reservas` (opcional): web externa de reservas; si es `https://…`, aparece otro botón (texto en `cta_secundario.texto`).
- Iconos útiles: `rio`, `piscina`, `huella`, `wifi`, `taza`, `ducha`, `cesta`, `lavadora`, `nino`, `tienda`, `caravana`, `enchufe`, `barbacoa`, `fuego`, `montana`, `arbol`, `ruta`, `bici`, `parking`, `coche`, `tren`, `bus`, `avion` (lista completa en `src/components/ui/Icono.astro`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, alojamientos, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Varios valores = una cadena separada por comas (`extras`). Máximo 24 elementos por lista.
5. **Nunca inventes** precios, cifras ni opiniones: si el cliente no los da, déjalos vacíos (los componentes lo soportan).
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`, empezando por una `<section class="banda banda--bosque">` (la cabecera es fija y `main` ya deja su hueco); enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Apartado nuevo**: añade `secciones.<id>` en `site.yaml` con `tipo:` = `texto`, `alojamientos`, `entorno`, `comodidades`, `galeria`, `temporada`… (el diseño que quiera reutilizar). `src/pages/index.astro` lo recoge solo; no lo toques.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (hay cuatro scripts pequeños: cabecera, visor de la galería, mapa bajo demanda y fechas del formulario), bandas de borde a borde, 16 px de margen lateral del texto en móvil (`.contenedor`), botones de 44 px de alto como mínimo y sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `titulo`/`nombre` del elemento); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`; al publicar, la plataforma lo conecta a su envío. Para envío propio, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.alojamientos.alojamientos` → `/alojamientos/<slug>/` (alojamiento) y `secciones.entorno.actividades` → `/entorno/<slug>/` (lugar del entorno).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, capacidad, distancia…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/alojamientos/` ni `src/pages/entorno/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y alojamiento o lugar con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "alojamientos; comodidades" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/alojamientos/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
