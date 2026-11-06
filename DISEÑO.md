# Camping y alojamiento rural: brief de diseño

Plantilla `alojamiento-naturaleza` creada el 06/11/2026 a partir de `hotel-boutique` con `php artisan plantillas:nueva`
y rediseñada entera a ancho completo. De la base solo queda la estructura técnica (datos, SEO, fichas y varias páginas).
Nace porque la de `alojamiento-rural` «no gusta»: portada de solo texto sobre fondo crema y fotos pequeñas. Este fichero
se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: campings, glampings, casas rurales, apartamentos rurales, albergues y hoteles rurales. Quien entra está
  eligiendo dónde dormir en el campo o la montaña: quiere ver el sitio con fotos grandes, saber qué tipos de estancia hay
  (casa, bungalow, tienda, parcela), qué servicios tiene, qué hacer cerca, cuándo abre y cómo llegar.
- **Qué tiene que conseguir la web**: que consulte disponibilidad (barra de fechas de la portada, formulario de llegada,
  salida y personas, WhatsApp) o que reserve en su motor externo (`enlace_reservas`). Secundario: llamar (barra fija
  del móvil con «Llamar» y «Reservar»).
- **Tono y estilo** (`natural`): luminoso, tranquilo, actual. Sí: las webs de glampings y campings nuevos que enseñan el
  paisaje a pantalla completa y dejan respirar. No: la caja crema con fotos pequeñas de `alojamiento-rural`, ni el lujo
  negro y oro de `hotel-boutique`.
- **Paleta de ejemplo**: primario `#1f3a2e` (verde bosque), acento `#b4582a` (teja; blanco encima: 4,8:1), fondo `#f6f3ec`
  (hueso), texto `#1d2420`. Derivados con `color-mix` en `global.css`: `--bosque-hondo` (pie, cómo llegar), `--salvia`
  (bandas alternas), `--acento-hondo` (botón al pasar), `--acento-texto` (antetítulos sobre claro, AA), `--acento-claro`
  (acento sobre oscuro), `--sobre-oscuro`, `--linea`, `--linea-clara`. Aguanta otros cuatro colores siempre que el
  primario sea oscuro, el acento medio y el fondo claro.
- **Tipografía**: sin fuentes externas. Títulos en la serifa del sistema (Sitka Display en Windows, Iowan Old Style o
  Charter en Apple, Georgia de respaldo), peso normal, redonda y algo apretada; el nombre de la portada enorme (hasta
  9 rem) y el del pie igual. Texto en la sans del sistema (Segoe UI Variable, system-ui). Antetítulos y rótulos en
  mayúsculas pequeñas espaciadas con el acento. Botones de píldora.
- **Motivos propios**: la ventana grande (foto a sangre que toca el borde de la pantalla en portada, «El lugar»,
  servicios, temporada y reservas); la foto de detalle montada en la esquina de la grande con marco del color de fondo;
  píldoras sobre las fotos (tipo y precio de cada alojamiento, distancia de cada lugar); mosaico de borde a borde con
  juntas finas.
- **Ritmo de bandas** (todas de borde a borde, contenido a `max-width: 88rem`):
  portada a pantalla casi completa (foto a sangre, velo de abajo arriba, nombre enorme abajo a la izquierda, lema,
  entradilla, botones, detalles con iconos; en escritorio, barra blanca de fechas montada sobre el borde) → el lugar
  (texto a la izquierda, foto grande a la derecha hasta el borde con la foto de detalle encima) → alojamientos (salvia,
  fichas con foto 4:3 en dos columnas; con número impar, la primera a lo ancho en 21:9) → servicios (bosque: panorámica
  a sangre arriba y rejilla de iconos) → entorno (claro, tarjetas verticales 3:4 con el nombre sobre la foto; carrusel en
  el móvil) → fotos (mosaico de borde a borde, visor al pulsar) → temporada (salvia, foto a sangre + tabla con filetes) →
  opiniones (salvia, tres tarjetas claras) → cómo llegar (bosque hondo, indicaciones + mapa que solo se carga al pulsar)
  → preguntas (claro, titular fijo y acordeón) → reservas (bosque, texto + formulario y foto a sangre al otro lado) →
  contacto (claro, vías en letra grande + formulario en salvia) → pie (bosque hondo, nombre enorme, eslogan y tres columnas).
- **Responsive**: móvil primero. A 375 px todo en una columna con 16 px de margen del texto (las fotos tocan el borde),
  portada al 92 % del alto, entorno en carrusel horizontal por pasos, mosaico en dos columnas con la primera grande,
  barra fija abajo con «Llamar» y «Reservar», menú plegable (`details`). Desde 860 px alojamientos en dos columnas; desde
  1024 px las filas foto/texto a sangre, la barra de fechas y la foto de detalle; desde 1180 px menú completo.
- **Cabecera**: fija a todo el ancho; transparente con texto blanco sobre la portada (y sobre la foto de las fichas) y
  hueso al hacer scroll.

## Apartados (en orden) y listas propias

1. `hero`: antetítulo, `titulo` (lema; el h1 es el nombre del negocio), texto, foto, dos botones e `items` (titulo + icono).
2. `alojamiento` («El lugar»): texto en párrafos, `firma`, `imagen` (grande) y `foto` (detalle), `cta` como enlace.
3. `alojamientos`: `alojamientos` [{nombre, categoria, texto, precio, personas, extras, imagen, imagenes, detalle}], `cta`.
4. `comodidades` («Servicios e instalaciones»): `imagen` panorámica e `items` [{titulo, texto, icono}].
5. `entorno`: `actividades` [{titulo, texto, distancia, imagen, imagenes, detalle}].
6. `galeria`: `galeria` (lista de rutas; con 8 fotos el mosaico queda cerrado en escritorio).
7. `temporada`: texto, `imagen`, `horario` [{dia, horas}], `nota`.
8. `opiniones`: `testimonios` [{texto, autor, nota}].
9. `como-llegar`: texto, `imagen` (fondo del mapa), `items` (coche, autobús, avión) y botón a Google Maps.
10. `preguntas`: `preguntas` [{pregunta, respuesta}].
11. `reservas`: texto, `imagen`, `cta`, `cta_secundario`, `enlace_reservas`, `nota` y formulario de estancia.
12. `contacto`: titular, vías de contacto de `site.yaml → contacto` y formulario.
13. `texto` (diseño genérico para apartados nuevos).

`comodidades` no se llama `servicios` a propósito: así el alta de una web nueva no lo rellena con «Lo que hacemos» y los
servicios del negocio (eso son sus alojamientos), y el comprobador no pide ficha por servicio.

## Páginas propias (fichas)
- `alojamientos.alojamientos` → `/alojamientos/<slug>/` (Accommodation) y `entorno.actividades` → `/entorno/<slug>/`
  (TouristAttraction). Misma piel que la portada: foto del elemento a sangre al 74 % del alto con la cabecera
  transparente, migas, tipo, nombre, entradilla y píldoras (precio, capacidad, distancia); `detalle` en párrafos con la
  tabla de datos y una caja bosque para reservar o preguntar; fotos (`imagenes`) a sangre; otras de la misma lista con
  foto grande. Sin foto, la cabecera es bosque.

## Varias páginas
Reparto de `template.yaml`: Alojamientos (`alojamientos; comodidades`) · El entorno (`entorno; como-llegar`) · Reservas
(`temporada; preguntas; reservas; contacto`); Inicio se queda con portada, el lugar, fotos y opiniones. La barra de
fechas de la portada va a la página de reservas con las fechas en la dirección y el formulario las recoge.

## Fotos

24 en `fotos.json` (generadas con IA el 06/11/2026; el comprobador avisa a partir de 16, pero la plantilla vive de las
fotos): portada (vega con río turquesa, bungalows y tiendas bajo los Picos de Europa), casa de piedra con hórreo y su
corredor, salón de la casa, bungalow por fuera y por dentro, tienda safari por fuera y por dentro, parcelas junto al río,
panorámica de la piscina, cuatro del entorno en vertical (garganta, lagos, canoas, pueblo de piedra), otoño en la vega,
siete de galería (hoguera, desayuno, playa de río, estrellas, terraza del bar, parque infantil, hórreo), vista aérea del
valle para el mapa y porche al anochecer para reservas. Sin texto legible, sin logotipos y sin personas.

## Qué no hacer

- Volver a la portada de solo texto, a las fotos pequeñas o a la caja centrada con tarjetas de `alojamiento-rural`.
- Usar el negro y oro, la cursiva garalda, las cúpulas o los arcos de `hotel-boutique`.
- Poner textos fijos en los componentes o inventar precios, cifras u opiniones.
- Cargar el mapa de Google sin que el visitante lo pida (sin cookies ajenas hasta que pulsa).
