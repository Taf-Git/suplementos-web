# Compendio — Documentación del proyecto

> Última actualización: mayo 2026

## Descripción

**Compendio** es una web informativa y comercial sobre suplementos nutricionales. El usuario llega con una duda concreta sobre un suplemento y la resuelve a tres profundidades distintas, filtrando además por categoría (global, deporte, salud, cognición). La web no promueve el consumo — informa de forma neutral y basada en evidencia científica. Monetización por enlaces de afiliados; sin AdSense, por alineación filosófica con la postura editorial neutral.

---

## Dos tracks de trabajo

El repositorio aloja dos cosas distintas. Conviene no mezclarlas.

**Track de producción — Compendio** *(objetivo de publicación)*
Web real basada en Next.js sobre Vercel. Es el track principal y todas las decisiones de diseño, contenido y arquitectura se refieren a este, salvo mención explícita en contrario. La ficha de creatina ya está implementada en JSX y funciona como design system de referencia para las siguientes fichas.

**Track de aprendizaje — `Suplementos/*.html`** *(no se publicará)*
Web sencilla en HTML semántico + CSS sin frameworks. Es el ejercicio personal con el que Toni aprende los fundamentos de desarrollo web. La ficha de ashwagandha en HTML está terminada y vive en `Suplementos/ashwagandha.html`. Sirve como referencia estructural histórica, no como contenido de Compendio.

A partir de aquí todo lo que se documenta es **Compendio**, salvo donde se indique lo contrario.

---

## Stack técnico — Compendio

- **Framework:** Next.js
- **Deploy:** Vercel (desde GitHub)
- **Componentes:** JSX
- **Estado global:** Context API
- **Pipeline de producción de fichas:**
  1. Dossier de Research del suplemento (markdown, generado en chat dedicado)
  2. Contenido editorial estructurado por nivel y categoría (markdown tipo `creatina_contenido_completo.md`)
  3. Componente JSX (replicando la estructura de la ficha de creatina)
  4. Claude Design solo para establecer o iterar el design system la primera vez; Claude Code para implementación

**Regla del pipeline:** el dossier de Research **nunca** se pasa a Claude Design. Riesgo de armonización — que el modelo mezcle fuentes y reintroduzca material descartado. El paso intermedio (md estructurado) es el filtro editorial.

---

## Herramientas

- **Editor:** Antigravity (basado en VS Code, agente Gemini integrado)
- **Control de versiones:** Git + GitHub
- **Usuario GitHub:** `Taf-Git`
- **Repositorio:** https://github.com/Taf-Git/suplementos-web
- **Asistentes Claude:** Claude Pro (Opus), Claude Code, Claude Design

---

## Modelo de contenido — Ficha de suplemento

Cada suplemento es una sola página con dos ejes de filtrado independientes.

### Eje 1 — Nivel (acumulativo)

- **Básico** — contenido esencial, visible por defecto
- **Intermedio** — añade profundización con un par de estudios citados (básico + intermedio como texto continuo)
- **Avanzado** — añade fichas completas de los estudios (básico + intermedio + avanzado como texto continuo)

El toggle de nivel vive en una barra superior sticky permanente. El nivel seleccionado persiste en `window.storage` con clave `[suplemento]:modo`.

### Eje 2 — Categoría (selección exclusiva con multi-select vía chip Global)

- **Global** — siempre visible, independientemente de la categoría seleccionada
- **Deporte / Salud / Cognición** — visibles solo si están seleccionados

Un bloque puede tener múltiples etiquetas de categoría (ej. `salud, cognicion`).

### Arquitectura en el DOM

Las secciones temáticas existen una sola vez. Los bloques etiquetados con `nivel` y `categoria` se apilan dentro de cada sección. El sistema **muestra u oculta** bloques en su posición natural — nunca duplica secciones ni reorganiza la página.

### Regla de degradación

Si una combinación de filtros deja menos del 40% del contenido visible, se muestra el contenido `global` igualmente para evitar páginas vacías.

### Orden de secciones (referencia: ficha de creatina implementada)

1. ¿Qué es?
2. ¿Para qué sirve?
3. ¿Para quién es?
4. Dosis
5. Absorción y biodisponibilidad
6. ¿Todas las formas son iguales? *(en suplementos con sellos comerciales — ashwagandha, por ejemplo — esta sección muta a "Comparativa de sellos")*
7. Sellos de calidad
8. Evidencia científica (estudios)
9. Mitos
10. Lo que la ciencia aún no tiene claro
11. ¿Quién no debe tomarla?

Detalles tipográficos, paleta, componentes, marginalia, kodama y reglas estéticas: ver `brief_diseño_compendio.md` en la knowledge base. No se duplican aquí.

---

## Criterio editorial *(no negociable)*

- **Solo RCT aleatorizados, doble ciego y controlados con placebo** como evidencia principal. Excepciones (sellos comerciales, estudios fundacionales históricos, brechas reales donde no existe el triple-criterio) **se declaran explícitamente**.
- **Conflictos de interés siempre declarados**, incluso cuando son "ninguno". Esto es especialmente relevante en ashwagandha (Ixoreal/KSM-66, Natreon/Sensoril, Arjuna/Shoden), creatina (AlzChem/Creapure) y magnesio en menor medida.
- **No inventar datos de salud bajo ninguna circunstancia.** Cifras, mecanismos y afirmaciones médicas vienen del dossier de Research del suplemento o de búsqueda verificada. Si surge la duda, decir "no se ha encontrado evidencia" y seguir.
- **Honestidad sobre brechas:** preferible decir "no se ha encontrado un RCT que cumpla los criterios" que rellenar con evidencia más débil.
- **Los metaanálisis se citan como contexto secundario, nunca como estudio principal.**

---

## Perfil de lectores

El perfil concreto se define en el dossier de Research de cada suplemento (el lector de creatina no es el mismo que el de ashwagandha). Como regla general:

- **Básico** — adulto que busca respuesta práctica sin tecnicismos
- **Intermedio** — lector curioso que quiere entender el mecanismo
- **Avanzado** — profesional o lector exigente que quiere los estudios completos con metodología

---

## Tono editorial

- Neutral, sin promover el consumo
- Cálido y cercano incluso en nivel avanzado — rigor con calidez, no manual frío ni venta
- Primera persona del plural al dirigirse al lector
- Transparencia sobre brechas, conflictos de interés y limitaciones

---

## Estado de las fichas — Compendio

| Suplemento   | Estado                                   | Materia prima                                      |
|--------------|------------------------------------------|----------------------------------------------------|
| Creatina     | ✅ Implementada (design system de referencia) | `ficha_creatina_v4.jsx`, `creatina_contenido_completo.md` |
| Ashwagandha  | 🔄 Próxima en el roadmap                  | Dossier de Research disponible en el project       |
| Magnesio     | ⏳ Pendiente (va después de ashwagandha)  | Dossier de Research disponible                     |
| Omega-3      | ⏳ Pendiente (va después de magnesio)     | Sin dossier todavía                                |
| Melatonina   | ⏳ Pendiente (va después de omega-3)      | Sin dossier todavía                                |

---

## Materiales en la knowledge base del project

- `PROYECTO.md` — este archivo
- `brief_diseño_compendio.md` — sistema de diseño completo (paleta, tipografía, componentes, marginalia, kodama, reglas que no se rompen)
- `brief_home_compendio.md` — diseño de la home
- `ficha_creatina_v4.jsx` — implementación JSX de referencia (cuarta iteración)
- `creatina_contenido_completo.md` — contenido editorial de creatina estructurado por nivel y categoría
- `Ashwagandha__Evidencia_Científica__Sellos_Comerciales_y_Verdades_Incómodas.md` — dossier de Research de ashwagandha
- `ashwagandha.html` — referencia estructural del **track de aprendizaje**, no contenido de Compendio
- Dossiers de Research de magnesio, omega-3, melatonina y otros suplementos — se suben al project según se necesiten

---

## Organización de chats en el project

- **Chat principal** — desarrollo técnico de Compendio (JSX, Next.js, GitHub, decisiones de arquitectura). Es donde se hace la implementación de cada ficha.
- **Un chat por suplemento** — investigación, redacción y revisión del dossier de Research y del contenido editorial estructurado.
- **Chats dedicados al track de aprendizaje** — HTML/CSS, fundamentos, ejercicios. Separados para no contaminar el contexto del proyecto de producción.

---

## Convención de Git

- Commits descriptivos en español
- Rama principal: `main`
- Flujo: `git add .` → `git commit -m "descripción"` → `git push`
