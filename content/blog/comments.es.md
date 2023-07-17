+++
title = "Añade comentarios a tus publicaciones con giscus, utterances o Hyvor Talk"
date = 2023-07-14
updated = 2023-07-16
description = "Descubre cómo habilitar una sección de comentarios en tus publicaciones usando giscus, utterances o Hyvor Talk, permitiendo la interacción y feedback de los lectores."

[taxonomies]
tags = ["funcionalidad", "tutorial"]

[extra]
giscus = true
quick_navigation_buttons = true
+++

tabi actualmente soporta tres sistemas de comentarios: [giscus](https://giscus.app/es) y [utterances](https://utteranc.es/) y [Hyvor Talk](https://talk.hyvor.com/).

giscus y utterances son proyectos de código abierto que te permiten añadir una sección de comentarios a tu sitio web usando las «issues» (utterances) o «discussions» (giscus) de GitHub. Son perfectos para generadores de sitios estáticos como Zola, ya que permiten a tus lectores interactuar y dejar comentarios en tus publicaciones sin requerir un backend tradicional ni una base de datos.

Al estar basados en GitHub, giscus y utterances requieren que los usuarios tengan una cuenta en dicha plataforma y autoricen la respectiva aplicación. Alternativamente, los visitantes también pueden comentar directamente en la discusión o «issue» correspondiente de GitHub.

Ambas son excelentes herramientas para agregar comentarios a tu blog, pero giscus tiene algunas ventajas:
- Más temas.
- Soporte para reacciones.
- Respuestas a comentarios y vista de conversación.
- Más seguro: utterances requiere habilitar estilos en línea inseguros («unsafe inline styles») para ajustar la altura del frame; giscus no.
- Soporte multilingüe: utterances solo está disponible en inglés; giscus soporta más de 20 idiomas.
- Desarrollo más activo: el último commit de giscus, a fecha de esta publicación, fue hace una dos días. El último commit de utterances fue hace más de un año.

Hyvor Talk es una plataforma de comentarios de pago centrada en la privacidad. Ofrece todas las ventajas de giscus y algunas más, como moderación y detección de spam.

## Configuración

### Sistemas basados en GitHub

giscus y utterances requieren una configuración similar. Primero, visita el sitio web del sistema que quieras habilitar: [giscus.app](https://giscus.app/es) o [utteranc.es](https://utteranc.es/).

Sigue las instrucciones de la sección **Configuración** del sitio web, y elige las opciones que prefieras. Luego, establece los valores que se muestran en la sección **Habilitar giscus/utterances** (el bloque de código `script`) en la sección correspondiente de tu `config.toml`: `[extra.giscus]` o `[extra.utterances]`.

#### giscus

giscus tiene algunos ajustes más que utterances:

```toml
[extra.giscus]
enabled_for_all_posts = false
automatic_loading = true
repo = "tuNombreDeUsuarioDeGithub/tuRepositorio"
repo_id = "TuIDdeRepositorio"
category = "Anuncios"
category_id = "TuIDdeCategoría"
mapping = "slug"
strict_title_matching = 1  # 1 para habilitar, 0 para deshabilitar.
enable_reactions = 1  # 1 para habilitar, 0 para deshabilitar.
comment_box_above_comments = true
light_theme = "noborder_light"
dark_theme = "noborder_dark"
lang = ""  # Deja en blanco para que coincida con el idioma de la página.
lazy_loading = true
```

#### utterances

```toml
[extra.utterances]
enabled_for_all_posts = false
automatic_loading = true
repo = "tuNombreDeUsuarioDeGithub/tuRepositorio"
issue_term = "slug"
label = "💬"
light_theme = "github-light"
dark_theme = "photon-dark"
lazy_loading = true
```

### Hyvor Talk

Configura tu web desde la [consola de Hyvor Talk](https://talk.hyvor.com/console) y rellena las opciones en `config.toml`:

```toml
[extra.hyvortalk]
enabled_for_all_posts = false
automatic_loading = true
website_id = "1234"
page_id_is_slug = true
lang = ""
page_author = ""  # Correo (o correo codificado en base64) del autor.
lazy_loading = true
```

### Ajustes comunes

La opción `enabled_for_all_posts = true` habilitará globalmente el sistema de comentarios correspondiente.

Alternativamente, puedes habilitar los comentarios en publicaciones concretas añadiendo el nombre del sistema (`utterances`, `giscus` o `hyvortalk`) `= true`. Por ejemplo, así habilitarías giscus:

```toml,hl_lines=09-10
+++
title = "Los molinos de viento de mi vida: reflexiones de un escudero"
date = 1605-01-16
updated = 2023-07-17
description = "Mi viaje junto a Don Quijote, enfrentándome a gigantes imaginarios y descubriendo las verdaderas batallas de la vida."

[taxonomies]
tags = ["personal", "reflexiones"]

[extra]
giscus = true
+++
```

Si accidentalmente habilitas más de un sistema, Zola mostrará un error.

Si tu web tiene múltiples idiomas con publicaciones coincidentes (como esta demo), y te gustaría compartir comentarios entre idiomas, debes usar `issue_term = "slug"` (en el caso de giscus y utterances) o `page_id_is_slug = true` (para Hyvor Talk). Esto usará el nombre del archivo Markdown (sin la etiqueta de idioma) como identificador. Todas las demás opciones crearán diferentes secciones de comentarios para cada idioma.


## Ejemplo en vivo

Al final de esta publicación encontrarás el widget de giscus usando los ajustes mostrados [arriba](#giscus).
