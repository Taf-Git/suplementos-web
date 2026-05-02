# Suplementos Web — Documentación del Proyecto

## Descripción
Web informativa y comercial sobre suplementos nutricionales. El usuario puede encontrar información por nombre de suplemento o por necesidad. La web no promueve el consumo — informa de forma neutral y basada en evidencia científica.

## Stack técnico actual
- HTML semántico
- CSS (styles.css para estilos globales, suplemento.css para páginas de suplemento)
- Sin frameworks ni JavaScript salvo casos puntuales
- Próximos pasos: React → Next.js

## Herramientas
- Editor: Antigravity (basado en VS Code, agente Gemini integrado)
- Control de versiones: Git + GitHub (usuario: Taf-Git)
- Repositorio: https://github.com/Taf-Git/suplementos-web

## Estructura de archivos
suplementos-web/
├── index.html
├── styles.css
├── suplemento.css
├── README.md
├── PROYECTO.md
└── Suplementos/
    └── ashwagandha.html

## Modelo de contenido — Página de suplemento
Cada suplemento tiene tres niveles de profundidad en una sola página con sistema de acordeón (etiqueta HTML details/summary).

### Nivel básico (fondo verde pastel)
Visible por defecto, sin acordeón.
Secciones:
1. ¿Qué es? — origen, forma de obtención, una línea sobre veganismo
2. ¿Para qué sirve?
3. ¿Cómo se toma? — dosis, formatos
4. ¿Es apta para veganos? — solo si hay matiz relevante
5. ¿Quién no debe tomarla? — contraindicaciones

### Nivel intermedio (fondo amarillo pastel)
Acordeón: "Quiero saber más"
Secciones:
1. Dato curioso
2. Mecanismo de acción
3. Absorción y biodisponibilidad
4. Sinergias y antagonismos
5. Qué dicen los estudios (Autor et al., año — ver estudios)
6. Sellos de calidad
7. Lo que la ciencia aún no tiene claro

### Nivel avanzado (fondo azul pastel)
Acordeón: "Quiero saber mucho más"
Solo ensayos aleatorizados, doble ciego y controlados con placebo.
Cada estudio en su propio div con id (estudio-autor-año).
Cierra con párrafo de contexto crítico.

## Convenciones de código

### HTML
- Un solo h1 por página
- Etiquetas semánticas: nav, header, main, section, footer
- Clases descriptivas: nivel-basico, tarjeta-categoria, categoria-salud
- IDs para estudios: estudio-autor-año (ej: estudio-chandrasekhar-2012)
- ../styles.css y ../suplemento.css desde subcarpetas

### CSS
- styles.css — estilos globales
- suplemento.css — estilos específicos de páginas de suplemento
- Color principal: #1a1a2e
- Color enlace/acento: #2980b9
- Verde básico: #f0faf4
- Amarillo intermedio: #fffbf0
- Azul avanzado: #f0f4ff

### Git
- Commits descriptivos en español
- Rama principal: main
- Flujo: git add . → git commit -m "descripción" → git push

## Decisiones de diseño tomadas
- Una página por suplemento con acordeón nativo HTML details/summary
- Borde izquierdo de color en tarjetas de niveles
- Tarjetas de categoría del index completamente clicables
- Tipografía: Inter (Google Fonts)
- Responsive con media query en 768px

## Perfil de lectores
- Básico: mujer ~45 años, nivel medio-alto, información práctica sin tecnicismos
- Intermedio: adulto 35-55 años, curioso, quiere entender el mecanismo
- Avanzado: profesional que busca evidencia científica primaria

## Tono editorial
- Neutral, sin promover el consumo
- Cálido y cercano incluso en nivel avanzado
- Primera persona del plural al dirigirse al lector
- Conflictos de interés en estudios siempre declarados

## Suplementos publicados
- Ashwagandha (Withania somnifera) — completo en tres niveles

## Suplementos pendientes
- Creatina (siguiente)
- Omega 3
- Magnesio
- Vitamina D

## Organización de chats en el proyecto
- Chat principal: desarrollo web (HTML, CSS, JS, estructura, GitHub)
- Un chat por suplemento: investigación, redacción y revisión de contenido