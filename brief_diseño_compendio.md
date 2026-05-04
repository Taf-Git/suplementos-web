# Brief de diseño · Compendio

> Web informativa enciclopédica sobre suplementación nutricional y deportiva basada en evidencia.

---

## Cómo usar este brief

Este documento es el punto de partida para continuar el diseño de la web **Compendio** en una nueva conversación con Claude. Está acompañado de un archivo JSX funcional (`ficha_creatina_v2.jsx`) que implementa la ficha de la creatina monohidrato como prototipo de referencia. Para arrancar bien la siguiente conversación:

1. Pega este brief al inicio del chat.
2. Adjunta `ficha_creatina_v2.jsx` como referencia visual y técnica.
3. Indica qué pieza quieres iterar (otra ficha de suplemento, la home, una página de categoría, el sistema de búsqueda, etc.).

---

## 1. Contexto y propósito

Web **enciclopédica** (no editorial cronológica) sobre suplementación nutricional y deportiva basada en evidencia. El usuario llega con una duda concreta sobre un suplemento y debe poder resolverla a tres profundidades distintas. Tono buscado: **rigor cálido**. Autoridad científica como base, calidez visual como diferenciador. Inspirada en lo mejor de Examine.com, MySportScience, Stronger by Science y Tufte, evitando la frialdad de los primeros y la densidad inabarcable de los segundos.

## 2. Inspiraciones declaradas

- **Bartosz Ciechanowski** (ciechanow.ski) → para gráficos interactivos integrados en el flujo del texto.
- **Edward Tufte** (tufte-css.html) → para el layout de columna principal + marginalia anclada al párrafo.
- **Quanta Magazine** → para la sensibilidad de "ciencia con calidez editorial".
- **Maggie Appleton** → para el espíritu de mezclar ilustración orgánica con contenido técnico riguroso.
- **MySportScience** → para infografías de mecanismos de acción.
- **Studio Ghibli** → solo como guiño puntual: el kodama como mascota, hojitas decorativas en el hero. Sin invadir la paleta ni la tipografía del cuerpo.

Lo que **se rechaza explícitamente**: estética de tech-startup (gradientes morados, Inter, azules SaaS), formatos blog-cronológico (esto es referencia fija), exceso de acordeones desplegables tipo Examine, longitudes inabarcables tipo Stronger by Science.

## 3. Dirección estética: editorial científico cálido

Papel acuarela cálido como base, tipografía serif característica con eje variable, paleta cerrada de tres acentos terrosos, ilustraciones SVG hechas a mano (no fotografía, no iconos genéricos). El conjunto debe parecerse más a un cuaderno de campo de un naturalista del XIX que a una landing page moderna.

## 4. Tipografía

Tres fuentes de Google Fonts más una cuarta solo para detalles manuscritos puntuales:

- **Fraunces** (display, títulos, encabezados de sección, letras capitulares, etiquetas en tarjetas). Variable font con ejes `opsz`, `wght` y `SOFT`. Se usa con `fontVariationSettings: '"opsz" 144, "SOFT" 30'` en títulos grandes y `"SOFT" 80` en italianas para máxima organicidad. Pesos 300-600.
- **Newsreader** (cuerpo de texto, párrafos, marginalia). Serif transicional muy legible, con itálica preciosa. Tamaño base 18px, line-height 1.65-1.7.
- **JetBrains Mono** (metadatos, números, etiquetas técnicas, números de sección "§ 01", unidades, breadcrumbs). Pesos 400-500. Letter-spacing alto (0.12-0.18em) y mayúsculas en uso decorativo.
- **Caveat** (manuscrita, **uso muy puntual y exclusivo**: solo la fórmula química bajo la ilustración del hero). No se usa en cuerpo, marginalia, ni etiquetas. Es una firma cálida única.

URL completa de carga:
```
https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT@9..144,300..800,0..100&family=Newsreader:opsz,wght,ital@6..72,400..700,0;6..72,400..700,1&family=JetBrains+Mono:wght@400;500&family=Caveat:wght@400;600&display=swap
```

## 5. Paleta de color

Cerrada y cálida. Dominantes terrosos, sin azules, sin morados, sin grises puros.

```js
const C = {
  bg:        '#F2EADB',  // crema papel — fondo principal
  bgDeep:    '#E7DCC4',  // crema profundo — separadores, headers tabla
  paper:     '#FAF5E9',  // hoja interior — tarjetas y figuras
  ink:       '#2A2218',  // tinta cálida — texto principal
  inkSoft:   '#5C5040',  // gris-tinta — texto secundario
  inkFaint:  '#9A8C75',  // texto terciario, metadatos
  rule:      '#D4C7A8',  // líneas ornamentales y bordes
  terra:     '#B5532A',  // terracota — acento principal, fosfágeno
  terraSoft: '#E29770',
  ochre:     '#C49237',  // ocre — acento secundario, glucólisis
  ochreSoft: '#E5C87B',
  sage:      '#7A8E63',  // salvia — acento terciario, oxidativo
  sageSoft:  '#B5C49B',
};
```

**Reglas de uso**: terracota se reserva para acentos protagonistas (letrina capitular, marginalia, indicador "ergogénico", barras decorativas, em del título). Ocre para datos numéricos protagonistas y rayos de luz. Salvia para diseños de bordes de estudios y elementos vegetales (hojas). El blanco puro y el negro puro nunca aparecen.

## 6. Estructura: tres niveles de profundidad

Toggle visible y permanente en la barra superior sticky con tres pestañas: **Básico · Intermedio · Avanzado** (con tiempos de lectura indicativos: ~3, ~8, ~18 minutos). Decisión deliberada en contra de Examine: cada nivel **reorganiza la página entera**, no se usan acordeones encadenados. La selección persiste en `window.storage` entre sesiones. En móvil el toggle se mantiene visible y compacto.

## 7. Layout estilo Tufte

CSS Grid de dos columnas: principal de máximo 640px (~65 caracteres por línea, óptimo para lectura) más columna lateral derecha de 280px para marginalia, separadas por 60px de gap. **La marginalia se ancla en grid-row al párrafo que la inspira**, no flota como lista lateral independiente. En móvil (<900px) la marginalia colapsa inline con un fondo crema que la diferencia visualmente del cuerpo. Header sticky con fondo translúcido y backdrop-filter blur. Max-width del contenedor 1180px.

## 8. Elementos clave del diseño

- **Header sticky**: barra superior translúcida con logo + nombre de marca con eyebrow "suplementación basada en evidencia" en JetBrains Mono, y a la derecha el toggle de niveles.
- **Eyebrow del hero**: línea de metadatos en JetBrains Mono pequeño, separada por guiones y bullets, con una etiqueta categórica (ej. "Grupo A · Evidencia robusta") y un indicador con punto de color (● Ergogénico).
- **Título tipo revista**: dos líneas, Fraunces a `clamp(48px, 7vw, 92px)`, segunda palabra en italiana terracota más ligera (font-weight 300) con SOFT alto.
- **Subtítulo conversacional**: italiano, Newsreader 21px, color inkSoft, tono directo y honesto que rompe el formalismo del título.
- **Facts rápidos**: fila horizontal de cuatro datos clave con bordes verticales tenues entre ellos, encabezado en JetBrains Mono uppercase, valor grande en Fraunces y nota en italiana inkFaint. Colapsa a 2 columnas en tablet y 1 en móvil.
- **Letras capitulares**: en color terracota, Fraunces 64px, float left, primera letra de cada sección.
- **Marginalia**: borde izquierdo terracota 2px, etiqueta "Nota al margen" en JetBrains Mono uppercase letter-spaced, título en Fraunces seminegrita, cuerpo en italiana 14.5px inkSoft. Anclada al párrafo correspondiente vía grid-row.
- **Ornamentos separadores**: línea ondulada SVG terminada en dos puntos (terracota grande + salvia pequeño), separa secciones cada ~50px de padding vertical.
- **Encabezados de sección**: número precedido por símbolo § en JetBrains Mono uppercase como eyebrow, seguido de h2 en Fraunces 36px con SOFT 30.
- **Tarjeta de protocolos** (ej. dosis): grid de tres columnas (concepto, valor numérico en JetBrains Mono terracota, nota italiana), header crema profundo, divisorias horizontales tenues.
- **Tarjetas de mitos**: el mito en italiana inkFaint con tachado terracota, la verdad debajo en ink. Comunica visualmente "esto se cae".
- **Tarjetas de estudios** (modo avanzado): borde izquierdo salvia 3px, autor + año + tipo de diseño en JetBrains Mono uppercase, título en Fraunces, resumen propio (no abstract) en cuerpo regular.
- **Componente Tecnico**: spans con fondo crema profundo, padding pequeño y JetBrains Mono al 0.85em para términos técnicos inline (ej. nombres de transportadores, enzimas).
- **Pie**: borde superior fino, dos líneas en JetBrains Mono uppercase con fecha de revisión y versión.

## 9. Gráficos interactivos (patrón Ciechanowski)

Patrón replicable para cualquier mecanismo de acción: figura inserta en el flujo del texto con sangrado negativo de 20px laterales, fondo paper, borde rule. Cada figura lleva:

- **Caption con eyebrow** "Figura N · Interactiva" en JetBrains Mono y título en Fraunces.
- **Pista de uso** discreta a la derecha del caption ("mueve el cursor →").
- **El gráfico SVG en sí** con colores de la paleta (no más de 3 dominantes).
- **Slider personalizado** con thumb terracota.
- **Lectura dinámica** debajo del slider: tres "píldoras" con valores numéricos en tiempo real, indicador del sistema dominante, y un párrafo italiano que **reescribe su contenido según el valor del slider**, contextualizando el dato (no solo describiendo).

El primer ejemplo concreto es el gráfico de áreas apiladas de los tres sistemas energéticos (fosfágeno, glucólisis, oxidativo) en función de la duración del esfuerzo, con el slider barriendo de 1 a 120 segundos. Esta misma estructura sirve para representar farmacocinéticas, dosis-respuesta, ventanas de saturación, etc.

## 10. Ilustraciones SVG hechas a mano

Estilo: línea suelta, trazos de 1.1-1.4px, esquinas redondeadas con `strokeLinejoin="round"`, colores planos sin gradientes complejos (excepto el halo del hero). Forma orgánica preferida sobre geométrica. **Nunca usar fotografía, librerías de iconos genéricos, ni stock**.

**El hero de cada suplemento** sigue una composición fija:

1. Halo radial cálido de fondo (radialGradient ochreSoft → terraSoft transparente).
2. Rayos de luz cálida en ocre (7 líneas con opacidad 0.4) saliendo del centro.
3. La estructura química o conceptual del suplemento (en creatina: la molécula simplificada con átomos como discos cálidos, terracota y salvia para destacar grupos funcionales clave).
4. Cuatro hojitas en verde salvia flotando en las esquinas (forma de gota con vena central).
5. Dos gotitas de rocío en crema-papel suspendidas (sin azul, para mantener la paleta cálida).
6. **El kodama** asomándose en la esquina inferior izquierda.
7. La fórmula química o etiqueta identificativa en Caveat manuscrita en la parte inferior.

## 11. El kodama como hilo conductor 🌱

**El detalle de marca más importante de todo el sistema**. Un pequeño espíritu del bosque (cuerpo y cabeza ovaladas en crema-papel, ojos negros con un destello blanco, brazos cortos curvados) que **aparece en cada ficha de suplemento en una postura diferente, observando o reaccionando al contenido de esa ficha en concreto**.

Es una pequeña broma silenciosa con el lector. Quien visita una ficha no lo nota. Quien visita tres empieza a buscarlo. Quien visita diez ya lo busca primero. Crea apego silencioso a la marca sin restarle un milímetro de rigor al contenido. Es esencialmente lo que hace que la web tenga "alma" sin volverse infantil.

**Ideas iniciales de poses por suplemento** (a ampliar):

| Suplemento     | Postura del kodama                                       |
|----------------|----------------------------------------------------------|
| Creatina       | Mirando con curiosidad la molécula (postura inicial)     |
| Cafeína        | Muy despierto, ojos muy abiertos, alerta                 |
| Melatonina     | Durmiendo, pequeñas zzz alrededor                        |
| Magnesio       | Estirando un brazo como aliviando un calambre            |
| Omega-3        | Con una pequeña ola o pez al lado                        |
| Vitamina D     | Tomando el sol con los ojos cerrados                     |
| Beta-alanina   | Con cara de "me hormiguea" (paresthesia es su efecto)    |
| Proteína whey  | Con un pequeño biberón o cuchara                         |
| Bicarbonato    | Con cara incómoda y una mano en la barriga (efectos GI)  |
| Ashwagandha    | Meditando                                                |

Mantener siempre el mismo estilo de dibujo (las mismas proporciones, los mismos ojos), variando solo postura y un único elemento contextual mínimo. Nunca debe ocupar más del 15% del área del hero. Siempre en una esquina, nunca en el centro. Nunca debe hablar al usuario, nunca aparece fuera del hero.

## 12. Persistencia y comportamiento

- Preferencia de nivel (básico/intermedio/avanzado) persiste en `window.storage` con clave `[suplemento]:modo`.
- El gráfico interactivo se inicializa en un valor representativo del rango óptimo del suplemento (en creatina: 8 segundos).
- Sin animaciones de scroll, sin auto-play, sin pop-ups. La única "animación" es el cambio dinámico de la lectura bajo el slider del gráfico.
- Compatible con Windows, macOS, Android e iOS. Sin librerías browser-específicas.

## 13. Reglas que no se rompen

- Nunca pedir al usuario que clique para ver información esencial. Los acordeones no son la solución a la profundidad: el toggle de tres niveles lo es.
- Nunca usar más de tres colores de acento en una misma vista.
- Nunca un párrafo de cuerpo más ancho que ~65 caracteres.
- Nunca azules cool ni morados. La paleta es cálida.
- Nunca fotografía. Siempre ilustración SVG hecha a mano.
- Nunca emojis en el cuerpo del contenido (sí en metadatos puntuales decorativos como el ●).
- Nunca el kodama hablando.

---

## Próximos pasos sugeridos

Cuando arranques la nueva conversación, estas son piezas naturales por las que continuar (en orden recomendado):

1. **Página índice de suplementos** (la home funcional). Cuadrícula o lista de fichas con la clasificación AIS por evidencia (Grupo A/B/C/D) como criterio principal de organización. Cada item con el kodama en su postura representativa como avatar miniatura.
2. **Sistema de navegación entre fichas**: breadcrumb superior + relacionados al pie de cada ficha (ej. "si te interesa la creatina, también te interesará…"). Mantener calidez editorial, no algoritmo opaco.
3. **Componente "Cuándo NO suplementar"**: tarjeta dedicada por ficha con contraindicaciones y poblaciones que no se benefician. Falta crítica en casi toda la competencia.
4. **Tres o cuatro fichas más** para validar que el sistema escala (recomendación: cafeína, melatonina, omega-3, magnesio — son distintos en mecanismo, evidencia y formato de gráfico interactivo).
5. **Página "Sobre la metodología"**: explica clasificación AIS, niveles de evidencia, cómo se eligen los estudios, conflictos de interés. Aporta credibilidad institucional.
6. **Buscador**: probablemente la pieza más diferenciadora si se hace bien. Búsqueda por suplemento, por objetivo (rendimiento, recuperación, sueño…), por evidencia, por deporte.
7. **Sistema de citas y referencias**: footnotes que abren popover lateral con la referencia completa al estudio, sin sacar al usuario de la página.

---

## Recurso adjunto

`ficha_creatina_v2.jsx` — Implementación funcional de referencia. Contiene:

- Toggle de tres niveles con persistencia.
- Layout Tufte completo con marginalia anclada.
- Gráfico interactivo de sistemas energéticos.
- Hero con molécula, hojas, halo cálido y kodama.
- Tarjetas de protocolos, mitos y estudios.
- Estilos responsivos para móvil y tablet.

Es el punto de partida tangible para iterar el resto.
